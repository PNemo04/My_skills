---
name: github-ssh-key-push
description: Push a local git repository to GitHub through a dedicated SSH key. Use when GitHub HTTPS push fails, SSH auth is missing, the user needs a public key to paste into GitHub, or a repo must be pushed with GIT_SSH_COMMAND and a specific identity file.
---

# GitHub SSH Key Push

## Safety Rules

- Never print, paste, commit, upload, or summarize the private key file. Only show the `.pub` public key.
- Do not modify unrelated project files to make push easier. In particular, do not compress, rename, or convert screenshots/assets unless the user explicitly asks.
- Use a repository-specific key name when possible, for example `~/.ssh/<repo>_github_ed25519`.
- Prefer `--force-with-lease` over `--force` when replacing an empty GitHub initialization commit.
- Before pushing, run `git status --short` and explain any real uncommitted changes.

## Workflow

1. Confirm the GitHub remote target, preferably SSH form:

```bash
git@github.com:OWNER/REPO.git
```

2. Create a dedicated SSH key only if it does not already exist:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
KEY="$HOME/.ssh/REPO_github_ed25519"
if [ ! -f "$KEY" ]; then
  ssh-keygen -t ed25519 -C "OWNER-REPO" -f "$KEY" -N ""
fi
chmod 600 "$KEY"
chmod 644 "$KEY.pub"
cat "$KEY.pub"
```

Tell the user to add the printed public key in GitHub:

- Title: repository or machine name
- Key type: `Authentication Key`
- Key: the whole single `ssh-ed25519 ...` line

3. After the user confirms the key was added, test authentication with the identity file:

```bash
ssh -i "$KEY" -o IdentitiesOnly=yes -o StrictHostKeyChecking=accept-new -T git@github.com
```

Successful auth usually exits nonzero but prints:

```text
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```

4. Configure the remote and verify local state:

```bash
git remote add origin git@github.com:OWNER/REPO.git 2>/dev/null || git remote set-url origin git@github.com:OWNER/REPO.git
git branch -M main
git status --short
git log --oneline -1 --decorate
```

5. If the GitHub repo contains an initialization commit that is safe to replace, fetch it first:

```bash
GIT_SSH_COMMAND="ssh -i $KEY -o IdentitiesOnly=yes -o StrictHostKeyChecking=accept-new" git fetch origin main
```

6. Push with the dedicated key:

```bash
GIT_SSH_COMMAND="ssh -i $KEY -o IdentitiesOnly=yes -o StrictHostKeyChecking=accept-new" git push -u origin main --force-with-lease
```

Use a normal push instead when the remote is empty or when preserving remote history:

```bash
GIT_SSH_COMMAND="ssh -i $KEY -o IdentitiesOnly=yes -o StrictHostKeyChecking=accept-new" git push -u origin main
```

7. Verify the remote branch:

```bash
GIT_SSH_COMMAND="ssh -i $KEY -o IdentitiesOnly=yes -o StrictHostKeyChecking=accept-new" git ls-remote origin refs/heads/main
```

## Troubleshooting

- `Permission denied (publickey)`: wrong key file, key not added to GitHub, or GitHub account lacks repo access.
- `could not read Username for 'https://github.com'`: remote is HTTPS or no credential helper is available; switch to SSH remote.
- `stale info` with `--force-with-lease`: run `git fetch origin main` and retry after confirming the remote commit is safe to replace.
- If the public key was added as a deploy key with read-only access, enable write access or add it under account SSH keys.
