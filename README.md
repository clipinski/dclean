# dclean

Cross‑platform (Linux and macOS) Docker cleanup utility that removes:
- All containers (running or stopped)
- All volumes (including named volumes)
- All images
- Builder cache

Warning: This is destructive and irreversible.

## Requirements
- Docker CLI available on PATH
- Docker daemon reachable for most operations

## Installation

### Linux
Make the script executable:
```bash
chmod +x /path/to/dclean/dclean
```

Install to your PATH (choose one):
```bash
# User install (no sudo)
mkdir -p ~/.local/bin
ln -sf /path/to/dclean/dclean ~/.local/bin/dclean
# Ensure ~/.local/bin is in PATH (uncomment your shell):
# bash:
# echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
# zsh:
# echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
```

```bash
# System-wide (requires sudo)
sudo ln -sf /path/to/dclean/dclean /usr/local/bin/dclean
# Or copy
sudo cp /path/to/dclean/dclean /usr/local/bin/dclean
```

Verify:
```bash
dclean help
```

### macOS
Make the script executable:
```bash
chmod +x /path/to/dclean/dclean
```

Install to your PATH (choose one):
```bash
# System-wide (recommended)
sudo ln -sf /path/to/dclean/dclean /usr/local/bin/dclean
# Or copy
sudo cp /path/to/dclean/dclean /usr/local/bin/dclean
```

```bash
# Optional: user install (add ~/.local/bin to PATH)
mkdir -p ~/.local/bin
ln -sf /path/to/dclean/dclean ~/.local/bin/dclean
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
```

Verify:
```bash
dclean help
```

## Usage
```bash
dclean                 # same as 'dclean all'
dclean all             # containers → volumes → images → cache
dclean containers      # stop and remove all containers (force)
dclean volumes         # remove all volumes
dclean images          # remove all images (force)
dclean cache           # prune builder cache
```

Examples:
```bash
dclean
dclean all
dclean containers
dclean images
dclean volumes
dclean cache
```

## Behavior and Safety
- Designed to be destructive for a clean slate
- Empty-result handling prevents errors like:
  - `docker: 'docker rm' requires at least 1 argument`
- Uses chunking with `xargs -n 100` to avoid long argument lists
- Avoids GNU-only flags so it works on macOS and Linux
- Falls back to `docker system prune -f` if `docker builder prune -f` fails

## License
MIT — see `LICENSE`.


