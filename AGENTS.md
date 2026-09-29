# AGENTS.md — layer-desktop-fonts

Standalone candy repo for the `desktop-fonts` layer — JetBrains Mono, Liberation,
and Nerd Fonts symbols, system-wide. The candy lives in `charly.yml` at the repo
root: the per-distro `package:` arms (the `che/nerd-fonts` COPR on Fedora, the
`ttf-*` packages on Arch), the `check:` assertions, and the embedded `skill:`
entity projected into the marketplace corpus as `/charly-selkies:desktop-fonts`.

Canonical files:

- `charly.yml` — the `desktop-fonts:` candy entity and the `desktop-fonts-skill:`
  skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:desktop-fonts` — the owning skill. The font families, the
  per-distro package-name mapping, and the Fedora virtual-package note. Load
  before editing or troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, service declarations). Load before editing any entity field or plan
  step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence: each font
  package installed, resolved through `package_map`. They must stay valid on
  every distro arm they run on. Query the REAL installed name — on Fedora the
  `liberation-fonts` request resolves to `liberation-sans-fonts`.

## Modify this repo

- Edit the `desktop-fonts:` candy entity AND the `desktop-fonts-skill:` skill
  entity in `charly.yml` together. The skill is the projected usage source, so a
  package or distro-arm change not mirrored in the skill leaves the corpus stale.
- Package changes go in the matching `distro:` arm; repository policy (the
  `che/nerd-fonts` COPR) goes in the arm's `copr:` field.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
