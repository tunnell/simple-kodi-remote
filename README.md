# skr - Simple Kodi Remote

A **hardened**, terminal-based remote control for Kodi with vim-style keys and
multi-tap seek. Unlike other terminal remotes, `skr` drives Kodi purely through
`kodi-send` (the send-only EventServer protocol) — Kodi's HTTP/JSON-RPC web
server can stay disabled.

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
              [q/esc] Quit

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

| Key           | Action                          |
|---------------|---------------------------------|
| Space / k     | Play / Pause                    |
| s             | Stop                            |
| h / Left      | Navigate left                   |
| l / Right     | Navigate right                  |
| i / Up        | Navigate up                     |
| d / Down      | Navigate down                   |
| Enter / a     | Select                          |
| Backspace / b | Back                            |
| Home / g      | Home screen                     |
| p             | Previous (playlist/episode)     |
| n             | Next (playlist/episode)         |
| + / =         | Volume up                       |
| - / _         | Volume down                     |
| m             | Mute                            |
| > / .         | Seek forward (multi-tap)        |
| < / ,         | Seek backward (multi-tap)       |
| q / Esc / ^C  | Quit                            |

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

## Why kodi-send? (hardening)

Every other terminal remote for Kodi we're aware of —
[kodi-control](https://github.com/KenKundert/kodi-control),
[kodi-cli](https://github.com/JavaWiz1/kodi-cli)
([both](https://github.com/nawar/kodi-cli) of them),
[kodictl](https://github.com/vdloo/kodictl),
[kodi-controller-cli](https://github.com/hash-bang/kodi-controller-cli),
[kodi-command-line](https://github.com/chbarts/kodi-command-line) — speaks
JSON-RPC over HTTP, which requires enabling Kodi's web server: a listening
TCP service with credentials and a queryable API (library contents, even
filesystem browsing). `skr` instead drives Kodi exclusively through
`kodi-send` and the [EventServer](https://kodi.wiki/view/EventServer)
protocol:

- **No web server** — leave *Allow remote control via HTTP* disabled
- **Send-only UDP** — there is no response channel; even a fully
  compromised client can only inject input events, never read data back
- **Localhost-scoped** — enable only *Allow programs on **this** system to
  control Kodi*, run `skr` on the Kodi box over SSH, and the only
  network-exposed control surface is sshd

The trade-off: with no query channel, `skr` cannot display player state
(now playing, seek position) — the status line shows the last command
*sent* instead. That's the price of send-only, and the point.

As far as we know, `skr` is the only interactive TUI remote for Kodi that
works this way.

## Requirements

- zsh
- kodi-eventclients (provides `kodi-send`)
- ncurses

## License

GPLv3 - see [LICENSE.md](LICENSE.md)
