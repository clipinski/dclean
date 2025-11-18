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
# Symlink (recommended)
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
# Symlink (recommended)
sudo ln -sf /path/to/dclean/dclean /usr/local/bin/dclean

# Or copy
sudo cp /path/to/dclean/dclean /usr/local/bin/dclean
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


