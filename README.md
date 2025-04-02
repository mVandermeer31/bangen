# bangen

> ascii banners with gradients, effects, and a live terminal editor.

![app banner](demo/app_banner.gif)

[![mit license](https://img.shields.io/badge/license-mit-7c3aed?style=flat-square)](LICENSE)
[![python](https://img.shields.io/badge/python-3.11+-06b6d4?style=flat-square)](pyproject.toml)
[![release](https://img.shields.io/github/v/release/programmersd21/bangen?style=flat-square)](https://github.com/programmersd21/bangen/releases/latest)

live tui · 30 composable effects · multi-stop gradients · presets · `txt` / `png` / `gif` export · screensaver mode

---

## quick look

```bash
bangen "system ready" --font slant --gradient "#7c3aed:#06b6d4" --effect glow --effect wave
```

![screenshot](demo/screenshot.png)

---

## install

```bash
git clone https://github.com/programmersd21/bangen.git
cd bangen
python -m venv .venv
source .venv/bin/activate
pip install -e .
```

or via aur:

```bash
yay -S bangen-bin
```

thanks to [@dominiquini](https://github.com/Dominiquini) for aur help.

or grab a prebuilt binary from [releases](https://github.com/programmersd21/bangen/releases/latest).

requires python `3.11+`. pillow ships in the base install.

---

## use

launch the editor:

```bash
bangen
```

render from the cli:

```bash
bangen "hello"
bangen "hello" --font slant --gradient "#ff00ff:#00ffff"
bangen "hello" --effect wave --effect glow --effect pulse --speed 1.5 --amplitude 2.0
```

export:

```bash
bangen "hello" --export-txt banner.txt
bangen "hello" --export-png banner.png
bangen "hello" --effect wave --effect glow --export-gif banner.gif --gif-duration 3 --gif-fps 20
```

screensaver:

```bash
bangen "hello" --screensaver
```

animate in the terminal (great for `wipe` / `typewriter`):

```bash
bangen "hello" --effect wipe --animate --animate-duration 5
```

---

## tui keys

| key      | does                        |
|----------|-----------------------------|
| `↑↓`     | move                        |
| `←→`     | tweak                       |
| `enter`  | edit / toggle               |
| `ctrl+v` | paste in text fields        |
| `e`      | export dialog               |
| `l`      | load preset                 |
| `s`      | save preset                 |
| `a`      | auto-size info              |
| `c`      | changelog                   |
| `i`      | report issue                |
| `q`      | quit                        |

press `e` in the tui for the exporter: toggle `gif` / `png` / `txt`, edit the path, tweak `duration` / `fps`, live progress included.

---

## cli

```bash
bangen --version
bangen --help

# discover
bangen main --list-effects
bangen main --list-fonts
bangen main --list-presets

# presets + ai
bangen "hello" --preset cyberpunk
bangen "system" --preset matrix
bangen "hello" --preset-file ./my_preset.json
bangen "hello" --ai "retro crt hacker title"

# sizing (on by default, disable with --no-auto-size)
bangen "hello" --auto-size --export-gif banner.gif --gif-duration 3 --gif-fps 20
```

exports show a live bar with percent, elapsed, eta, and stage.

---

## effects

30 effects in 5 tiers. order matters — they compose top to bottom.

| tier       | effects                                                                     |
|------------|-----------------------------------------------------------------------------|
| motion     | `wave` `vertical_wave` `bounce` `scroll` `drift` `shake`                   |
| visual     | `gradient_shift` `pulse` `rainbow_cycle` `glow` `flicker` `scanline`       |
| temporal   | `typewriter` `fade_in` `wipe` `stagger` `loop_pulse`                       |
| distortion | `glitch` `chromatic_aberration` `noise_injection` `melt` `warp` `fragment` |
| signature  | `matrix_rain` `fire` `electric` `vhs_glitch` `neon_sign` `wave_interference` `particle_disintegration` |

favorite stacks:

| vibe     | stack                                        |
|----------|----------------------------------------------|
| cyberpunk| `glitch` + `chromatic_aberration` + `pulse`  |
| neon     | `glow` + `pulse`                             |
| matrix   | `matrix_rain` + `typewriter`                 |
| retro    | `scanline` + `flicker`                       |
| fire     | `fire` + `melt`                              |
| electric | `electric` + `glow`                          |

```python
banner.apply(build_effect("wave", config=cfg))
banner.apply(build_effect("chromatic_aberration", config=cfg))
banner.apply(build_effect("pulse", config=cfg))
```

---

## gradients + presets

colon-separated hex stops, horizontal or vertical:

```text
#ff00ff:#00ffff
#ff0000:#ffff00:#00ff00
```

```bash
bangen "hello" --gradient "#ff00ff:#00ffff" --gradient-dir vertical
```

presets live in `~/.bangen/presets/*.json` — save from the tui with `s`, or from the cli with `--save-preset name`:

```json
{
  "name": "my_preset",
  "font": "ansi_shadow",
  "gradient": "#ff00ff:#00ffff",
  "gradient_direction": "horizontal",
  "effects": ["wave", "glow", "pulse"],
  "effect_config": {
    "wave": { "speed": 1.8, "amplitude": 2.0, "frequency": 0.7 },
    "pulse": { "speed": 1.2, "min_brightness": 0.55 },
    "glow": {}
  }
}
```

---

## layout

```text
bangen/
├── effects/      # motion, visual, temporal, distortion, signature
├── export/       # txt, png, gif
├── gradients/    # multi-stop rgb engine
├── presets/      # built-ins + user store
├── rendering/    # pyfiglet engine, banner pipeline, auto-size
├── cli/          # typer commands, screensaver
├── ai/           # prompt → style suggester
└── tui/          # live editor, export + preset dialogs
```

---

## star history

<a href="https://www.star-history.com/#programmersd21/bangen&Date">
  <picture>
    <source
      media="(prefers-color-scheme: dark)"
      srcset="https://api.star-history.com/svg?repos=programmersd21/bangen&type=Date&theme=dark"
    />
    <source
      media="(prefers-color-scheme: light)"
      srcset="https://api.star-history.com/svg?repos=programmersd21/bangen&type=Date&theme=light"
    />
    <img
      alt="star history chart"
      src="https://api.star-history.com/svg?repos=programmersd21/bangen&type=Date"
    />
  </picture>
</a>

---

## license

mit. see [LICENSE](LICENSE).
