# portfolio

Static portfolio site for [www.jflab.cz](https://www.jflab.cz).

## Project structure

```text
portfolio/
├── .github/          # GitHub workflows/settings
├── .well-known/
│   └── security.txt  # Security contact (RFC 9116)
├── 404.html          # Themed error page
├── LICENSE           # License file
├── README.md         # This file
├── index.html        # Main page content
├── static/
│   ├── favicon.svg   # Site icon
│   └── styles.css    # Site styling
```

No build step, no JavaScript frameworks, no external assets except the
Credly badge images — plain HTML and CSS deployed to GitHub Pages.
