# portfolio

Static portfolio site for [www.jflab.cz](https://www.jflab.cz).

## Project structure

```text
portfolio/
├── .github/          # GitHub workflows/settings
├── .well-known/
│   ├── openpgpkey/   # WKD — PGP key discovery (gpg --locate-keys)
│   └── security.txt  # Security contact (RFC 9116)
├── 404.html          # Themed error page
├── LICENSE           # License file
├── README.md         # This file
├── humans.txt        # The people behind the site
├── index.html        # Main page content
├── robots.txt        # Crawler policy + sitemap pointer
├── sitemap.xml       # Sitemap
├── static/
│   ├── badges/       # Self-hosted certification badge images
│   ├── favicon.svg   # Site icon
│   └── styles.css    # Site styling
```

No build step, no JavaScript frameworks, no external assets — plain
HTML and CSS deployed to GitHub Pages.
