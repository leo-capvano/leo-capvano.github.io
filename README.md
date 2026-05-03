# Leo Capvano Portfolio

GitHub-inspired dark theme portfolio built with Jekyll, SCSS, and GitHub Pages.

## Quick Start

```bash
# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# Open http://localhost:4000
```

## Local Verification

```bash
# Build and verify CSS compiled
bundle exec jekyll build

# Check dark theme colors
grep "#0d1117" _site/assets/main.css && echo "✓ Dark theme found"
grep "#f0883e" _site/assets/main.css && echo "✓ Orange accents found"
grep "#58a6ff" _site/assets/main.css && echo "✓ Blue accents found"

# Verify component styles
grep "project-card" _site/assets/main.css && echo "✓ Project cards found"
grep "tech-grid" _site/assets/main.css && echo "✓ Tech grid found"
grep "@media.*max-width: 767px" _site/assets/main.css && echo "✓ Mobile responsive found"
```

## Production Verification

Site deployed at: **https://leo-capvano.github.io**

```bash
# Check site is live
curl -I https://leo-capvano.github.io

# Verify dark theme in production
curl -s https://leo-capvano.github.io/assets/main.css | grep "#0d1117" && echo "✓ Live theme verified"
```

Check build status: https://github.com/leo-capvano/leo-capvano.github.io/actions

## Project Structure

```
_sass/minima/
  ├── custom-variables.scss    # SCSS variables (colors, spacing, fonts)
  └── custom.scss              # Component styles
assets/main.scss              # SCSS entry point
index.md                      # Site content
```

## Customization

Edit `_sass/minima/custom-variables.scss` to change:
- Colors: `$color-dark-bg`, `$color-orange`, `$color-blue`
- Fonts: `$font-family-base`, `$font-family-mono`
- Spacing: `$spacing-*` variables

## Troubleshooting

**Ruby version error**: Install Ruby 3.x
```bash
brew install ruby@3.3
rbenv local 3.3.0
```

**CSS not updating**: Clear cache and rebuild
```bash
rm -rf _site/
bundle exec jekyll serve
```

**GitHub Pages build fails**: Check Actions tab for error details and verify Gemfile.lock is committed
