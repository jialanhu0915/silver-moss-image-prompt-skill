# Vendored upstream script

This directory contains an unmodified copy of OpenMOSS's Layout prompt compiler.

- Upstream repository: <https://github.com/OpenMOSS/MOSS-Image>
- Upstream file: [`skills/moss-image-prompt-enhancer/scripts/compile_prompt.py`](https://github.com/OpenMOSS/MOSS-Image/blob/52b87fca23acedc399d062d593bec388aee9926a/skills/moss-image-prompt-enhancer/scripts/compile_prompt.py)
- Pinned upstream commit: `52b87fca23acedc399d062d593bec388aee9926a`
- Local copy: `vendor/openmoss/compile_prompt.py`
- License: Apache-2.0. The repository's `LICENSE` is byte-identical to the upstream [`LICENSE`](https://github.com/OpenMOSS/MOSS-Image/blob/52b87fca23acedc399d062d593bec388aee9926a/LICENSE) at the pinned commit.
- SHA-256 of the copied script: `203B7B10A2E2781F022868E2B1DF7D62271C97E283303CD717700DCC8779FF09`

The compiler uses only the Python standard library. It validates and converts a pixel-coordinate draft; it does not validate visual placement or generate images.

## Updating

1. Review the upstream change and license at a specific upstream commit.
2. Replace the local copy without local edits; update the pinned commit and SHA-256 above.
3. Compile the draft in `examples/layout.md` and confirm the emitted JSON matches the documented result.
4. Update `NOTICE.md` and `CHANGELOG.md` if the provenance or behavior changes.
