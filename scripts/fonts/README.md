# Fonts

Subsetted [JetBrains Mono](https://github.com/JetBrains/JetBrainsMono) — SIL Open Font Licence 1.1.
See `OFL.txt` for the full licence text.

| File | Characters | Size | Used by |
|---|---|---|---|
| `jbmono-ramp.woff2` | ` .\`:-=+*cs#%@` (13 chars) | ~1.3 KB | `ascii.svg` |
| `jbmono-head.woff2` | Letters used in section headings | ~1.4 KB | `hd-*.svg` |
| `jbmono-400.woff2` | Basic Latin, regular weight | ~4.5 KB | stat SVGs |
| `jbmono-600.woff2` | Basic Latin, semibold weight | ~4.5 KB | stat SVGs |

These are inlined as base64 data URIs inside each SVG.
External font URLs do not work in `<img>`-loaded SVGs — browsers refuse to
fetch subresources for image documents.

To regenerate the subsets yourself (requires `fonttools`):

```bash
pip install fonttools brotli

# ramp subset — only the 13 characters the portrait uses
pyftsubset JetBrainsMono-Regular.ttf \
  --text=' .`:-=+*cs#%@' \
  --flavor=woff2 --layout-features='' --no-hinting \
  -o scripts/fonts/jbmono-ramp.woff2

# heading subset — only the letters the headings spell out
pyftsubset JetBrainsMono-SemiBold.ttf \
  --text='aboutstckprejigh' \
  --flavor=woff2 --layout-features='' --no-hinting \
  -o scripts/fonts/jbmono-head.woff2

# full basic latin (for data graphics), both weights
pyftsubset JetBrainsMono-Regular.ttf \
  --unicodes='U+0020-007E' \
  --flavor=woff2 --layout-features='' --no-hinting \
  -o scripts/fonts/jbmono-400.woff2

pyftsubset JetBrainsMono-SemiBold.ttf \
  --unicodes='U+0020-007E' \
  --flavor=woff2 --layout-features='' --no-hinting \
  -o scripts/fonts/jbmono-600.woff2
```
