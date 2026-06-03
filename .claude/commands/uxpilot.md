# /uxpilot — Extract UXPilot design to standalone HTML

Extract a UXPilot share URL into a clean, standalone HTML file by rendering it with headless Chrome, parsing out the design HTML, and saving it to `screens/`.

## Usage
```
/uxpilot <share-url> [output-filename]
```

**Examples:**
```
/uxpilot https://uxpilot.ai/s/abc123def456
/uxpilot https://uxpilot.ai/s/abc123def456 plugin-page.html
```

- `share-url` must be a public `s/` share link (not a `/p/` project link — those require auth)
- `output-filename` is optional; defaults to `uxpilot-<timestamp>.html`

---

## Steps to execute

### 1. Validate the URL
Check that `$ARGUMENTS` contains a URL matching `https://uxpilot.ai/s/`. If it is a `/p/` URL, stop and tell the user it requires authentication and ask them to generate a public share link instead.

Parse `$ARGUMENTS` — first token is the URL, optional second token is the output filename.

### 2. Render with headless Chrome

Run the following bash command to render the page with JavaScript fully executed and dump the DOM:

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless=new \
  --disable-gpu \
  --no-sandbox \
  --dump-dom \
  --virtual-time-budget=8000 \
  "<URL>?fullscreen=true" 2>/dev/null > /tmp/uxpilot_raw.html
```

Also take a screenshot so you can see the design:
```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless=new \
  --disable-gpu \
  --no-sandbox \
  --screenshot=/tmp/uxpilot_preview.png \
  --window-size=1440,900 \
  --virtual-time-budget=8000 \
  "<URL>?fullscreen=true" 2>/dev/null
```

Read `/tmp/uxpilot_preview.png` to visually confirm the design loaded (not a blank/auth error page). If blank or "No token provided", stop and tell the user the link requires authentication.

### 3. Extract the design HTML

Run this Python script to decode the double-escaped HTML and extract the actual page content:

```bash
python3 - <<'PYEOF'
import html as htmllib, re, sys

with open('/tmp/uxpilot_raw.html', 'r', encoding='utf-8', errors='ignore') as f:
    raw = f.read()

# The design HTML is double-encoded inside the Next.js payload
# Decode twice to get the real markup
decoded = htmllib.unescape(htmllib.unescape(raw))

# Find the <style> block (contains color tokens and animations)
style_match = re.search(r'<style[^>]*>(.*?)</style>', decoded, re.DOTALL)
styles = style_match.group(0) if style_match else ''

# Find <body ...>...</body>
body_match = re.search(r'<body[^>]*>.*?</body>', decoded, re.DOTALL)
body = body_match.group(0) if body_match else ''

# Find Google Fonts links
fonts = ' '.join(re.findall(r'<link[^>]*fonts\.googleapis[^>]*>', decoded))

# Extract <script> blocks that contain page logic (not analytics/trackers)
scripts = []
for m in re.finditer(r'<script(?![^>]*src)[^>]*>(.*?)</script>', decoded, re.DOTALL):
    content = m.group(1).strip()
    # Skip empty, tracker, and UXPilot blocker scripts
    if (content and len(content) > 50
            and 'blockEvent' not in content
            and '_uxpResizeCharts' not in content
            and 'clarity' not in content
            and 'fbq' not in content
            and 'gtag' not in content):
        scripts.append(f'<script>{content}</script>')

with open('/tmp/uxpilot_extracted.json', 'w') as f:
    import json
    json.dump({'styles': styles, 'body': body, 'fonts': fonts, 'scripts': scripts}, f)

print(f"styles: {len(styles)} chars")
print(f"body:   {len(body)} chars")
print(f"scripts: {len(scripts)} blocks")
PYEOF
```

### 4. Build the standalone HTML file

Using the extracted parts, assemble a clean standalone HTML file:

```bash
python3 - <<'PYEOF'
import json, re, html as htmllib

with open('/tmp/uxpilot_extracted.json') as f:
    parts = json.load(f)

styles  = parts['styles']
body    = parts['body']
fonts   = parts['fonts']
scripts = '\n'.join(parts['scripts'])

# Strip UXPilot chrome (toolbar, watermark, cookie banner)
body = re.sub(r'<[^>]*(Made in UX Pilot|uxpilot-badge|cookie|CookieBanner)[^>]*>.*?</[^>]+>', '', body, flags=re.DOTALL|re.IGNORECASE)

# Fix navigation hrefs — UXPilot uses href="#", replace with real routes
# (caller can adjust these after)

html_out = f"""<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Extracted Design</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/all.min.css" crossorigin="anonymous" />
    {fonts}
    {styles}
</head>
{body}
{scripts}
</html>"""

with open('/tmp/uxpilot_standalone.html', 'w') as f:
    f.write(html_out)

print(f"written {len(html_out)} chars")
PYEOF
```

### 5. Save to screens/

Determine the output filename:
- If the user provided a second argument, use that (ensure `.html` extension)
- Otherwise use `uxpilot-<6-char-hash-of-url>.html`

Copy the file:
```bash
cp /tmp/uxpilot_standalone.html screens/<output-filename>
```

### 6. Report back

- Read `/tmp/uxpilot_preview.png` and display it so the user can see the captured design
- Tell the user the file was saved to `screens/<filename>`
- Note any navigation links that are `href="#"` placeholders that may need updating
- Suggest running `open screens/<filename>` to preview it in the browser
