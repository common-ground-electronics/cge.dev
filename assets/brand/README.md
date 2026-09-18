# Site brand derivations

`og-default.svg` is the site's default Open Graph card, derived from the brand
template `brand/assets/svg/og-light.svg` (title text replaced per the
template's two-line rule). The brand repo's SVG sources remain the source of
truth for everything else; see `brand/README.md`.

To regenerate `static/images/og.png` after editing (uses the same pinned resvg
renderer and vendored fonts as the brand pipeline; run from the repo root with
the brand repo checked out as a sibling at `../brand`):

```sh
uv run --with resvg-py==0.5.0 python -c "
import resvg_py, pathlib
svg = pathlib.Path('assets/brand/og-default.svg').read_text()
png = resvg_py.svg_to_bytes(svg_string=svg, width=1200, height=630,
                            font_dirs=['../brand/assets/fonts'], skip_system_fonts=True)
pathlib.Path('static/images/og.png').write_bytes(bytes(png))"
```
