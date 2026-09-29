# desktop-fonts

Desktop font stack for OpenCharly images — JetBrains Mono, Liberation, and Nerd
Fonts symbols.

The `desktop-fonts` candy installs three font families from each distro's
packages, system-wide:

- **JetBrains Mono** — the monospace coding font used by waybar and swaync.
- **Liberation** — the serif/sans/mono web-font family Chrome falls back to for
  sans rendering.
- **Nerd Fonts symbols** — the icon glyph set that provides waybar and swaync
  icon glyphs.

Each font ships as an installed OS package, so its presence is verifiable by
querying the package database; cross-distro package names (Arch `ttf-*` vs
Fedora `*-fonts`) are resolved per-distro via `package_map`.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `desktop-fonts` |
| Packages (fedora) | `jetbrains-mono-fonts`, `liberation-fonts`, `nerd-fonts` (via the `che/nerd-fonts` COPR) |
| Packages (arch) | `ttf-jetbrains-mono`, `ttf-liberation`, `ttf-nerd-fonts-symbols`, `ttf-nerd-fonts-symbols-mono` |
| Service / port | none |

On Fedora, `liberation-fonts` is a **virtual** package — dnf resolves it to
`liberation-sans-fonts` (and sibling `-serif-fonts` / `-mono-fonts`), so the
`plan:` check queries the real installed name.

## How to use it

The layer is included by the desktop metalayers; it is not typically added
directly. To compose it explicitly, pin this repo in a box's `candy:` list:

```yaml
my-desktop:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-desktop-fonts:v2026.239.1629'
```

The candy's `plan:` asserts the JetBrains Mono, Liberation, and Nerd Fonts
packages are installed (via `package_map`), so a missing font family fails the
checks.

## Layout

- `charly.yml` — the `desktop-fonts:` candy entity (the per-distro `package:`
  arms, the `copr:` repo, and the `check:` assertions) and the embedded
  `desktop-fonts-skill:` skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:desktop-fonts`
- Consumers: `/charly-selkies:sway-desktop`, `/charly-selkies:selkies-desktop-layer`
- Users: `/charly-selkies:waybar`, `/charly-selkies:swaync`
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
