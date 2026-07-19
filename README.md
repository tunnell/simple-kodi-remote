# skr - Simple Kodi Remote

A terminal-based remote control for Kodi with vim-style keys and multi-tap seek.

## Screenshot

```
╔══════════════════════════════════════╗
║          SIMPLE KODI REMOTE          ║
╠══════════════════════════════════════╣
║                                      ║
║               [ ^ ] i                ║
║       h [ < ]  [OK]a  [ > ] l        ║
║               [ v ] d                ║
║                                      ║
║    p Prev    k/spc Play    Next n    ║
║                                      ║
║      ,< Seek<<        >>Seek >.      ║
║                                      ║
║          - Vol-      Vol+ +          ║
║                                      ║
║          s Stop      Mute m          ║
║                                      ║
║      b/bksp Back      Home g         ║
║                                      ║
╚══════════════════════════════════════╝
                [q] Quit

  Last command [14:32:05]: Seek +16s
```

## Installation

### Arch Linux (AUR)

```bash
yay -S skr
```

### Manual

```bash
git clone https://github.com/tunnell/simple-kodi-remote.git
cd simple-kodi-remote
chmod +x skr
sudo cp skr /usr/local/bin/
```

## Configuration

Optional: `~/.config/skr/config`

```ini
# Kodi host to control
host=localhost
# Multi-tap seek window in seconds (see below)
seek_window=0.4
```

## Keybindings

| Key           | Action                       |
|---------------|------------------------------|
| Space / k     | Play / Pause                 |
| s             | Stop                         |
| h / Left      | Navigate left                |
| l / Right     | Navigate right               |
| Up / i        | Navigate up                  |
| Down / d      | Navigate down                |
| Enter / a     | Select                       |
| Backspace / b | Back                         |
| Home / g      | Home screen                  |
| p             | Previous                     |
| n             | Next                         |
| + / =         | Volume up                    |
| - / _         | Volume down                  |
| m             | Mute                         |
| > / .         | Seek forward (multi-tap)     |
| < / ,         | Seek backward (multi-tap)    |
| q             | Quit                         |

### Multi-tap seek

Each additional tap within the seek window (default 0.4s) doubles the seek
amount: 1 tap = 2s, 2 taps = 4s, 3 = 8s, 4 = 16s, and so on for as long as
the burst continues. The status line shows the pending amount and tap count
live (`Seek +16s (tap 4)...`); the seek is sent as a single exact-second
jump once you stop tapping. Adjust the window with `seek_window` in the
config file.

Volume and navigation keys are hold-safe over SSH: keystrokes buffered
while a command is in flight are dropped, so holding a key stops acting
as soon as you release it.

## Requirements

- zsh
- kodi-eventclients (provides `kodi-send`)
- ncurses

## License

GPLv3 - see [LICENSE.md](LICENSE.md)
