# init_github

## Git Identity
- **Email:** sushant.s.raikar@gmail.com
- **Name:** Sushant Raikar

Always ensure local git config has this email set before committing:
```
git config user.email "sushant.s.raikar@gmail.com"
```

## GitHub PAT (HotSushi account)
- PAT file location: `/Users/sraikar/OSS/github.pat.token`
- The remote origin URL must use this token for authenticated pushes.

To set or refresh the remote URL:
```
TOKEN=$(cat /Users/sraikar/OSS/github.pat.token | tr -d '[:space:]')
git remote set-url origin "https://${TOKEN}@github.com/HotSushi/breatheapp.git"
```

## Rule
Before any `git commit` or `git push` in this repo:
1. Verify `git config user.email` is `sushant.s.raikar@gmail.com` — set it if not.
2. Verify the remote origin URL contains the HotSushi PAT — update it if not.
