---
name: github-codex-key
description: Use when working with GitHub from Codex or another coding agent, including testing SSH auth, cloning, pulling, pushing, setting git remotes, or retrieving a configured public SSH key.
---

# GitHub Codex Key

Use an SSH key dedicated to coding-agent GitHub operations. Keep the private key
local, never print it, and only share the `.pub` public key when configuring
GitHub.

## Recommended Key Paths

Choose a local key path and keep it consistent. For example:

- Private key: `~/.ssh/<agent_github_key>`
- Public key: `~/.ssh/<agent_github_key>.pub`
- SSH host config: `~/.ssh/config`

These names are examples. If you publish or share this skill, do not include
machine-specific paths, account names, or private key contents.

## Retrieve Public Key

When the user asks for the key to add to GitHub, show only the public key:

```bash
cat ~/.ssh/<agent_github_key>.pub
```

## Test GitHub Authentication

Use:

```bash
ssh -T git@github.com
```

A successful authentication usually prints a message like:

```text
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```

The command may still exit nonzero because GitHub does not provide shell access.

## Git Remote Usage

Prefer SSH remotes:

```bash
git clone git@github.com:OWNER/REPO.git
git remote set-url origin git@github.com:OWNER/REPO.git
git pull
git push
```

If Git does not pick the configured identity, force it for one command:

```bash
GIT_SSH_COMMAND="ssh -i ~/.ssh/<agent_github_key> -o IdentitiesOnly=yes" git push
```

## If Auth Fails

1. Confirm the key files exist.

```bash
ls -l ~/.ssh/<agent_github_key> ~/.ssh/<agent_github_key>.pub
```

2. Confirm `~/.ssh/config` has an entry similar to:

```sshconfig
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/<agent_github_key>
  IdentitiesOnly yes
```

3. Add the public key to GitHub.

GitHub Settings -> SSH and GPG keys -> New SSH key

4. Retest with `ssh -T git@github.com`.

## Safety Rules

- Never print, paste, upload, commit, or summarize private key contents.
- Never commit `.ssh/`, tokens, `.env`, or credential helper files.
- Use repository-specific deploy keys only when that access model is intended.
