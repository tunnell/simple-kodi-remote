# skr - Simple Kodi Remote

A terminal-based remote control for Kodi with keyboard controls and seek support.

## Screenshot

```
+--------------------------------------+
|         SIMPLE KODI REMOTE          |
+--------------------------------------+
|                                      |
|              [ Up ] i               |
|     h [Left]  [OK]  [Right] l      |
|              [Down] d               |
|                                      |
|   p Prev    k/spc Play   Next n   |
|                                      |
|       < <<30s      30s>> >        |
|                                      |
|       - Vol-        Vol+ +        |
|                                      |
|       s Stop        Mute m        |
|                                      |
|     bksp Back        Home g      |
|                                      |
+--------------------------------------+
                [q] Quit

Last command [14:32:05]: Play/Pause
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
host=localhost
```

## Keybindings

| Key           | Action           |
|---------------|------------------|
| Space / k     | Play / Pause     |
| s             | Stop             |
| h / Left      | Navigate left    |
| l / Right     | Navigate right   |
| Up / i        | Navigate up      |
| Down / d      | Navigate down    |
| Enter         | Select           |
| Backspace     | Back             |
| Home / g      | Home screen      |
| p             | Previous         |
| n             | Next             |
| + / =         | Volume up        |
| - / _         | Volume down      |
| m             | Mute             |
| > / .         | Seek forward     |
| < / ,         | Seek backward    |
| q             | Quit             |

## Requirements

- zsh
- kodi-eventclients (provides `kodi-send`)
- ncurses

## License

GPLv3 - see [LICENSE](LICENSE)
