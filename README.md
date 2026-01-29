# Mac Mini Server Setup

A script to set up a macOS machine for running [Moltbot](https://github.com/VoltAgent/moltbot) and other automation services.

Forked from [thoughtbot/laptop](https://github.com/thoughtbot/laptop), optimized for headless/server use.

## What This Fork Changes

| Original (thoughtbot) | This Fork |
|-----------------------|-----------|
| Heroku CLI + Parity | Removed (not needed) |
| PostgreSQL + Redis | Optional (uncomment if needed) |
| Ruby via asdf | Optional (uncomment if needed) |
| ImageMagick, Poppler | Optional (uncomment if needed) |
| — | **Added:** `gog` CLI for Google integration |
| — | **Added:** `htop`, `ripgrep`, `fd`, `jq`, `yq` |
| — | **Added:** `rclone` for backups |
| — | **Added:** Server-optimized macOS settings |

## Requirements

- macOS Sequoia (15.x), Sonoma (14.x), Ventura (13.x), or Monterey (12.x)
- Apple Silicon or Intel

## Install

### 1. Download and run the script

```sh
curl --remote-name https://raw.githubusercontent.com/hsztul/laptop/master/mac
sh mac 2>&1 | tee ~/laptop.log
```

### 2. Set up your laptop.local (optional but recommended)

```sh
curl --remote-name https://raw.githubusercontent.com/hsztul/laptop/master/laptop.local.example
mv laptop.local.example ~/.laptop.local
# Edit ~/.laptop.local to customize, then re-run:
sh mac 2>&1 | tee ~/laptop.log
```

## What It Sets Up

### Core Tools
- [Homebrew](http://brew.sh/) — Package manager
- [Git](https://git-scm.com/) — Version control
- [GitHub CLI](https://cli.github.com/) — GitHub API from terminal
- [Zsh](http://www.zsh.org/) — Shell
- [fzf](https://github.com/junegunn/fzf) — Fuzzy finder
- [tmux](http://tmux.github.io/) — Terminal multiplexer

### Search & Navigation
- [ripgrep](https://github.com/BurntSushi/ripgrep) — Fast search
- [fd](https://github.com/sharkdp/fd) — Fast find
- [The Silver Searcher](https://github.com/ggreer/the_silver_searcher) — Code search
- [tree](http://mama.indstate.edu/users/ice/tree/) — Directory listing

### Development
- [asdf](https://github.com/asdf-vm/asdf) — Version manager
- [Node.js](http://nodejs.org/) — Required for Moltbot
- [jq](https://stedolan.github.io/jq/) / [yq](https://github.com/mikefarah/yq) — JSON/YAML processing
- [Watchman](https://facebook.github.io/watchman/) — File watching

### Moltbot-Specific
- [gog](https://github.com/steipete/gog) — Google services CLI (Gmail, Calendar)
- [Rosetta 2](https://developer.apple.com/documentation/apple-silicon/about-the-rosetta-translation-environment) — Apple Silicon compatibility

### Server Tools
- [htop](https://htop.dev/) — Process monitor
- [rclone](https://rclone.org/) — Cloud storage sync

## laptop.local.example

The included `laptop.local.example` adds:

**Apps:**
- 1Password + CLI
- iTerm2, Warp
- Raycast
- Tailscale (critical for secure Moltbot access)
- Cursor, Claude, ChatGPT
- Obsidian
- Starship prompt

**Server Settings:**
- Disable sleep on power adapter
- Auto-restart on freeze/power failure
- Moltbot security hardening (mDNS disabled)
- Useful shell aliases

## Post-Install: Moltbot Setup

After running the laptop script:

```sh
# 1. Install Moltbot
npm install -g moltbot@latest

# 2. Run onboarding wizard
moltbot onboard

# 3. Set up Google integration
gog auth credentials ~/path/to/client_secret.json
gog auth add your@email.com

# 4. Configure Tailscale
open /Applications/Tailscale.app
tailscale up

# 5. Verify security
moltbot security audit --deep
```

See [moltbot-ideas.md](https://github.com/hsztul/laptop/blob/master/docs/moltbot-setup.md) for the full secure setup guide.

## Customization

Edit `~/.laptop.local` to add your own packages. Functions like `fancy_echo` and `append_to_zshrc` are available.

```sh
# Example: Add Python via asdf
add_or_update_asdf_plugin "python" "https://github.com/asdf-community/asdf-python.git"
install_asdf_language "python"
```

## Debugging

Check `~/laptop.log` for errors. [Open an issue](https://github.com/hsztul/laptop/issues) if needed.

## Credits

Based on [thoughtbot/laptop](https://github.com/thoughtbot/laptop). Original license applies.
