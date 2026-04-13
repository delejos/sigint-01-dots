# SIGINT-01 // Dotfiles

> Arch Linux + Hyprland — military ops center themed desktop environment

A fully configured Arch Linux setup built around Hyprland with a dark tactical aesthetic: grid-based wallpapers, classified document UI styling, monospace fonts throughout, and a coherent dark blue/cyan color palette across every component.

---

## Stack

| Component | Package |
|-----------|---------|
| Window manager | `hyprland` |
| Bar | `waybar` |
| Lock screen | `hyprlock` |
| Display manager | `greetd` + `tuigreet` |
| Terminal | `kitty` |
| Shell | `fish` + `starship` |
| App launcher | `rofi-wayland` |
| Fetch | `fastfetch` |
| Monitor | `btop` |
| Editor | `neovim` |
| Screenshots | `flameshot` |
| Notifications | `dunst` |
| Wallpapers | custom — generated via Python/Pillow |

---

## Workspaces

Four named persistent workspaces, each with its own wallpaper:

| # | Name | Purpose |
|---|------|---------|
| 1 | ALPHA | Primary terminal / operations |
| 2 | MIKE | General use |
| 3 | DELTA | Development |
| 4 | ECHO | Comms / browser |

---

## Install

> Requires a base Arch Linux install with network access. Run as your normal user (sudo access required for system files and package installation).

```bash
git clone https://github.com/YOUR_USERNAME/sigint-01-dots.git ~/sigint-01-dots
cd ~/sigint-01-dots
chmod +x install.sh
./install.sh
```

The script will:
1. Install all packages via `pacman` and `yay` (AUR)
2. Symlink all configs from the repo into `~/.config/`
3. Generate PNG wallpapers into `~/Wallpapers/`
4. Install system configs (`/etc/greetd/config.toml`)
5. Enable `greetd`, `sshd`, and pipewire user services
6. Set `fish` as your default shell

### sshd_config

The repo includes a hardened `sshd_config` (`PermitRootLogin no`, Protocol 2). To apply it:

```bash
INSTALL_SSHD_CONFIG=1 ./install.sh
```

It is skipped by default so you can review it first.

### Wallpaper source SVGs

SVG source files for the wallpapers are in `wallpapers/`. The install script copies them to `~/Wallpapers/svg/`. The PNG wallpapers used by Hyprland are generated programmatically — see `scripts/generate_wallpapers.py`.

---

## Post-install

- **btop theme** — open btop → `ESC` → Preferences → Color theme → select `sigint-01`
- **Neovim plugins** — run `nvim` and let lazy.nvim sync on first launch
- **Reboot** — greetd replaces your display manager; a reboot is recommended after install

---

## Keybinds

| Keys | Action |
|------|--------|
| `Super + Return` | Open terminal (kitty) |
| `Super + R` | App launcher (rofi) |
| `Super + E` | File manager (thunar) |
| `Super + L` | Lock screen (hyprlock) |
| `Super + Q` | Close window |
| `Super + F` | Fullscreen |
| `Super + V` | Toggle floating |
| `Super + 1-4` | Switch workspace + change wallpaper |
| `Super + Shift + 1-4` | Move window to workspace |
| `Super + Arrow keys` | Move focus |
| `Print` | Screenshot (flameshot) |

---

## Structure

```
.
├── .config/
│   ├── hypr/           # hyprland.conf, hyprlock.conf, wallpaper.sh,
│   │   └── scheme/     # workspace-watcher.sh, color scheme
│   ├── waybar/         # config.jsonc, style.css
│   ├── kitty/          # kitty.conf
│   ├── fish/           # config.fish
│   ├── fastfetch/      # config.jsonc
│   ├── btop/themes/    # sigint-01.theme, caelestia.theme
│   ├── nvim/           # colorscheme + plugins
│   ├── flameshot/      # flameshot.ini
│   └── starship.toml
├── wallpapers/         # SVG source files
├── scripts/            # generate_wallpapers.py
├── system/
│   ├── greetd/         # /etc/greetd/config.toml
│   └── ssh/            # /etc/ssh/sshd_config
└── install.sh
```

---

## Color palette

Dark steel blue base with cyan accents. Defined in `.config/hypr/scheme/current.conf` and mirrored across Waybar, Kitty, btop, and the wallpaper generator.

| Role | Hex |
|------|-----|
| Background | `#131317` |
| Active border | `#2A6080` |
| Accent | `#4AB8C9` |
| Text | `#E5E1E7` |
| Subtext | `#918F9A` |
