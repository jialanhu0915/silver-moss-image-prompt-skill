# silver-moss-image-prompt-skill

**English** · [简体中文](README_ZH.md)

A prompt-writing skill for [MOSS-Image](https://github.com/OpenMOSS/MOSS-Image). It turns an idea, a reference description or a Danbooru tag dump into a caption the model actually draws, plus a negative prompt and sampling settings.

Three style channels — **photoreal**, **anime**, **hybrid** (2D-in-3D, toon-shaded 3D, mixed media, split-style) — over a style-agnostic technique layer for camera, composition and aesthetics.

## What it is not

- Not an OpenMOSS project. It is a working method written against the official docs (see [NOTICE.md](NOTICE.md)).
- Not a template library. There is no one-click prompt generator here.
- Not an image generator. Plain Markdown, no scripts, no dependencies.

## How it is organized

Skills are loaded when a task matches, so the structure decides what the model actually reads. Each layer holds one kind of knowledge:

| Layer | Directory | Contents | Loaded |
| :--- | :--- | :--- | :--- |
| Routing | `SKILL.md` | decision table, five-step flow, self-check, hard rules | every time |
| Contract | `references/core/` | caption writing, sampling, negatives, in-image text, Layout | first run, then as needed |
| Style | `references/styles/` | photoreal / anime / hybrid, each channel's own decisions only | one at a time |
| Craft | `references/craft/` | camera, composition, aesthetics — style-agnostic | looked up per entry |
| Diagnostics | `references/diagnostics/` | symptom tables, sources and evidence levels | when something breaks |

A typical request loads `SKILL.md`, one contract file and one style file, and opens a craft file only for the specific technique it needs.

Maintenance rule: the reference tables are append-only. Entries may be added or corrected, never removed or merged; only the prose around them gets trimmed.

## Install

Drop the directory into an Agent Skills path. The directory name must match `name` in the frontmatter:

```text
<skills-dir>/silver-moss-image-prompt-skill/SKILL.md
```

Works with any client implementing the [Agent Skills specification](https://agentskills.io/specification). Alternatively, paste `SKILL.md` at the end of a system prompt and keep the rest as a reference manual.

## Layout

```text
SKILL.md                            routing, flow, self-check
DISCLAIMER.md / DISCLAIMER_EN.md    legal notice and user responsibility
references/
├── core/
│   ├── caption.md                  prose deliverable: word order, tags, length, language
│   ├── params.md                   sampling, two presets, resolution table
│   ├── negative.md                 layered negatives
│   ├── text-in-image.md            glyph-size estimation, vertical text, text polluting the subject
│   └── layout.md                   Layout JSON (experimental, off by default)
├── styles/
│   ├── photo.md                    photoreal: opening modules, shadow control, bone structure, stills
│   ├── anime.md                    anime: medium, format wrappers, finish, LoRA
│   └── hybrid.md                   hybrid: 2D-in-3D, toon 3D, mixed media, split-style
├── craft/
│   ├── camera.md                   focal length, shot size, angle, depth of field, frame ratio
│   ├── composition.md              layout, three depth layers, negative space, group shots, accidents
│   └── aesthetics.md               light positions, colour, technique, movements, materials, mood
└── diagnostics/
    ├── troubleshooting.md          symptom → cause → fix
    └── sources.md                  citations, evidence levels, rejected folklore
examples/
├── photo.md                        two photoreal walkthroughs
└── anime.md                        two anime walkthroughs
```

## Three design decisions

**Rules are bound to sampling presets.** The official guide states that turning SLG off makes output look very realistic but may collapse detail. The skill splits accordingly: **Q** (SLG on, 50 steps, ≥1M px, for delivery) and **R** (SLG off, few steps, 0.6M px, for fast iteration). Preset-dependent rules carry `[Q]` / `[R]` tags (untagged ones hold at both), because anti-collapse phrasing overshoots at Q and is mandatory at R.

**Only visible information.** The official captioning spec asks for composition, subjects, actions, setting, colours, lighting and artistic style, and for visible information only. Camera bodies, render engines, software names and artist IDs therefore do little on their own — write the visible result instead. The rule runs through every file.

**Evidence levels, stated up front.** Evidence is graded official, inferred, community, measured or unverified (`sources.md`). Tagged entries are mostly official or inferred; an untagged assertion is the author's unverified working practice, and anything that would need a controlled experiment is marked unverified rather than presented as fact. `sources.md` also lists the widely repeated claims this skill deliberately does not adopt.

## Known limits

- **Layout is off by default.** The official docs mark it experimental; coordinates must be computed by hand and drift across resolutions. `core/layout.md` is a fallback path.
- **Rules are not yet under controlled test.** The technique layer comes from general photography and illustration practice. Claims of the form "this works better on this model" are marked unverified.
- **Three channels only.** Multi-panel comics, poster layout and game HUD are not written up yet; many core and craft entries carry over, but each lacks its own rules.

## Roadmap

- [ ] Same-seed A/B for every unverified claim (template in `sources.md`)
- [ ] Multi-panel comic channel (blocked on Layout stability)
- [ ] Poster and editorial layout channel
- [ ] Game screenshot / HUD channel
- [ ] ComfyUI and Python API field mapping (the official API uses `uncond_skip_layers`; UIs name it differently)

## Credits

- [OpenMOSS/MOSS-Image](https://github.com/OpenMOSS/MOSS-Image) — model, user guide, captioning spec, Layout schema (Apache-2.0). Attribution in [NOTICE.md](NOTICE.md).
- The bilingual terminology tables and the principle that a term must be reduced to a visible fact are compiled from general photography, cinematography and illustration teaching.

Release history is in [CHANGELOG.md](CHANGELOG.md).

## Legal notice

This project is not legal advice and is provided as is. The user bears all legal risk for generated content and its use, and the project does not force a content filter (private deployments decide their own). Sexual content involving minors or childlike-looking characters is an absolute red line. Read [DISCLAIMER_EN.md](DISCLAIMER_EN.md) ([中文](DISCLAIMER.md)) before use.

## License

[Apache License 2.0](LICENSE), matching upstream MOSS-Image. Commercial use, modification and redistribution are permitted, provided the copyright notice, the `LICENSE` file and the attribution in [NOTICE.md](NOTICE.md) are retained, and modified files are marked as changed. No warranty is given; the license includes an express patent grant.
