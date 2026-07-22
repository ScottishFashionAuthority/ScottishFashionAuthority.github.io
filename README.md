# Scottish Fashion Authority

Landing site for the **Scottish Fashion Authority** — championing Scotland's
fashion industry through stories, events and networking.

- **Live site:** https://www.scottishfashionauthority.com/
- **Hosting:** GitHub Pages (custom domain via `CNAME`)

## Structure

| File | Purpose |
|------|---------|
| `index.html` | Single-page "coming soon" landing page (self-contained HTML/CSS/JS) |
| `og-image.png` | 1200×630 social share preview image |
| `og-image.svg` | Editable source for the social preview image |
| `robots.txt` | Crawler directives |
| `sitemap.xml` | Sitemap for search engines |
| `CNAME` | Custom domain configuration |

## Regenerating the social preview image

Edit `og-image.svg`, then render it to PNG with headless Chrome:

```bash
cat > _ogtmp.html <<'HTML'
<!DOCTYPE html><html><head><meta charset="utf-8">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,600;1,400&family=Jost:wght@500&display=swap" rel="stylesheet">
<style>html,body{margin:0;padding:0}body{width:1200px;height:630px;overflow:hidden}svg{display:block}</style>
</head><body><!--SVG--></body></html>
HTML
python3 -c "html=open('_ogtmp.html').read().replace('<!--SVG-->',open('og-image.svg').read());open('_ogtmp.html','w').write(html)"
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless --disable-gpu --hide-scrollbars --force-device-scale-factor=1 \
  --window-size=1200,630 --default-background-color=00000000 \
  --screenshot="og-image.png" --virtual-time-budget=4000 "file://$PWD/_ogtmp.html"
rm -f _ogtmp.html
```
