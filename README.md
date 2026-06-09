# my rmpc config

This repo contains my personal config for [rmpc](https://github.com/sonodima/rmpc), a terminal client for MPD. I wanted something simple, comfortable to use, clean-looking, and a little nicer with a visualizer at the bottom.

<div align="center">
  <img src="/rmpc.png" alt="rmpc screenshot" width="900" />
</div>

## What's inside

- `config.ron` — my main rmpc configuration.
- `themes/` — custom themes. Right now I use `pinkblueish`.

## My setup

This config is made for Linux and assumes this kind of setup:

- `rmpc` as the music client
- `mpd` as the music daemon
- `cava` for the visualizer
- MPD running on `127.0.0.1:6601`
- no MPD password

If your MPD setup is different, edit this part in `config.ron`:

```ron
address: "127.0.0.1:6601",
password: None,
```

## Installing rmpc on Linux

### 1. Install the main dependencies

At minimum, you need `mpd` and `rmpc`. `cava` is optional, but my config uses it for the visualizer, so I recommend installing it too.

### Arch Linux / Other Arch-based distros

```bash
sudo pacman -S mpd cava
```

For `rmpc`, install it from the AUR:

```bash
yay -S rmpc
```

or use the git version:

```bash
yay -S rmpc-git
```

## Using this config

Clone this repo into your rmpc config directory:

```bash
git clone https://github.com/kuenobaikbanget/my-rmpc.git ~/.config/rmpc
```

If you already have an existing `~/.config/rmpc` directory, back it up first:

```bash
mv ~/.config/rmpc ~/.config/rmpc.bak
git clone https://github.com/kuenobaikbanget/my-rmpc.git ~/.config/rmpc
```

## MPD + Cava note

The visualizer in this config reads from this FIFO file:

```text
/tmp/mpd.fifo
```

Make sure your MPD config has a FIFO output like this:

```conf
audio_output {
    type            "fifo"
    name            "Visualizer feed"
    path            "/tmp/mpd.fifo"
    format          "44100:16:2"
}
```

If you do not want to use the visualizer, you can remove or ignore the `Cava` pane in `config.ron`.

## Running it

Start MPD first:

```bash
systemctl --user enable --now mpd
```

Then run rmpc:

```bash
rmpc
```

## Why I made it like this

I wanted a terminal music player setup that feels clean but still useful. The queue is at the top, the visualizer sits at the bottom, and the other tabs are there for albums, artists, playlists, directories, and search.

The keybinds are also adjusted around how I usually navigate, so this config might feel a little personal. Feel free to fork it, tweak it, or just take the parts you like.
