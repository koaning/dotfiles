# dotfiles

Personal dotfiles for macOS. Zsh config, utility commands via [just](https://github.com/casey/just), and a few helper scripts.

## What's in here

- `.zshrc` - shell config (oh-my-zsh, powerlevel10k, auto-venv activation, etc.)
- `.justfile` - global utility commands accessible via the `kmd` alias
- `juststuff/rich-ls.py` - a rich-powered directory tree viewer

## Prerequisites

Install these first:

```sh
# Shell
brew install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
brew install powerlevel10k
brew install zoxide

# Dev tools
brew install just
brew install uv
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
curl -fsSL https://pixi.sh/install.sh | bash

# Optional
pip install marimo  # for shell completions
```

## Installation

```sh
# Clone to ~/dotfiles
git clone git@github.com:koaning/dotfiles.git ~/dotfiles

# Symlink zsh config
ln -sf ~/dotfiles/.zshrc ~/.zshrc

# Configure powerlevel10k (on first shell launch, or manually)
p10k configure

# Reload
source ~/.zshrc
```

The `.zshrc` sets up a `kmd` alias that points to the justfile:

```sh
alias kmd='just --justfile ~/dotfiles/.justfile'
```

## Usage

Run `kmd` to see all available commands:

```
kmd              # list commands
kmd serve        # start a local HTTP server on port 8000
kmd serve 3000   # ...or on a custom port
kmd myip         # show your public IP
kmd extract f.gz # extract any archive format
kmd freeport 8080 # kill whatever is using port 8080
kmd diskusage    # show disk usage for current directory
kmd tree         # directory tree (respects .gitignore)
kmd tree 3       # tree with depth 3
```

## Maintenance

```sh
# Pull latest changes
cd ~/dotfiles && git pull

# Reload shell config
source ~/.zshrc

# Run tests
uvx --with rich --with typer --with pathspec pytest juststuff/rich-ls.py
```
