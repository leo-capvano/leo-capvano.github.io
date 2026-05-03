# Leo Capvano Portfolio

Enhanced Minima theme portfolio built with Jekyll, SCSS, and GitHub Pages. Features a GitHub-inspired dark theme with responsive card-based project layout.

## Features

- **GitHub-Inspired Dark Theme**: Custom color palette (#0d1117 dark background, #f0883e orange accents, #58a6ff blue accents)
- **Responsive Design**: Fully responsive layout optimized for desktop, tablet, and mobile devices
- **Card-Based Projects**: Project cards with hover glow effects and organized layout
- **Tech Stack Section**: Interactive tech tag display with 2-column responsive grid
- **CSS-Only Implementation**: Clean Minima theme overrides using SCSS (no HTML modifications)
- **Fast & Lightweight**: Static site generated with Jekyll, deployed on GitHub Pages

## Quick Start - Local Development

### Prerequisites

- Ruby 3.0 or higher
- Bundler (usually installed with Ruby)
- Git

### Installation & Local Testing

1. **Clone the repository** (if you haven't already):
   ```bash
   git clone https://github.com/leo-capvano/leo-capvano.github.io.git
   cd leo-capvano.github.io
   ```

2. **Install dependencies**:
   ```bash
   bundle install
   ```

3. **Start the development server**:
   ```bash
   bundle exec jekyll serve
   ```

4. **Open in browser**:
   - Navigate to `http://localhost:4000`
   - The site will auto-reload when you make changes

### Local Verification Checklist

After starting the development server, verify the following:

#### Visual Elements
- [ ] Dark background color (#0d1117) is visible
- [ ] Orange section headers are present
- [ ] Blue project title accents are visible
- [ ] Project cards have a subtle border
- [ ] Tech tags appear in a grid layout
- [ ] Footer with social links is at the bottom

#### Responsive Design
- [ ] **Desktop** (1024px+): 2-column tech grid, full spacing
- [ ] **Tablet** (768px-1023px): Adjusted spacing and typography
- [ ] **Mobile** (<768px): 1-column tech grid, touch-friendly padding

Test using browser DevTools:
```
DevTools → Toggle device toolbar (Ctrl+Shift+M or Cmd+Shift+M)
```

#### Performance
- [ ] Page loads within 2 seconds
- [ ] No console errors (open DevTools: F12)
- [ ] CSS file loads successfully (check Network tab)
- [ ] All images load without errors

#### Content Verification
- [ ] "About" section displays correctly
- [ ] "Featured Projects" section shows 2-3 highlighted projects
- [ ] "All Projects" section lists all projects
- [ ] "Technology" section displays tech tags
- [ ] "Contact" section with email and social links present

## Automated Local Verification

Run these commands to verify the build without manual inspection:

```bash
# Verify dependencies are installed
bundle --version

# Build the site
bundle exec jekyll build

# Check that CSS was compiled
test -f _site/assets/main.css && echo "✓ CSS compiled successfully"

# Verify dark theme colors in compiled CSS
grep -q "#0d1117" _site/assets/main.css && echo "✓ Dark background color found"
grep -q "#f0883e" _site/assets/main.css && echo "✓ Orange accent color found"
grep -q "#58a6ff" _site/assets/main.css && echo "✓ Blue accent color found"

# Verify component styles
grep -q "project-card" _site/assets/main.css && echo "✓ Project card styles found"
grep -q "tech-grid\|grid-template-columns" _site/assets/main.css && echo "✓ Tech grid styles found"

# Verify responsive breakpoints
grep -q "@media.*max-width: 767px" _site/assets/main.css && echo "✓ Mobile responsive styles found"
```

### Expected Output

```
bundle 2.x.x
✓ CSS compiled successfully
✓ Dark background color found
✓ Orange accent color found
✓ Blue accent color found
✓ Project card styles found
✓ Tech grid styles found
✓ Mobile responsive styles found
```

## Production Verification

### Live Site Verification

The site is deployed to GitHub Pages at: **https://leo-capvano.github.io**

Verify the production deployment:

```bash
# Check site is accessible
curl -I https://leo-capvano.github.io 2>&1 | head -5

# Verify HTML structure
curl -s https://leo-capvano.github.io | grep -q "site-title" && echo "✓ HTML structure verified"

# Verify CSS is served
curl -s https://leo-capvano.github.io/assets/main.css 2>&1 | wc -l

# Verify dark theme colors in production CSS
curl -s https://leo-capvano.github.io/assets/main.css | grep -q "#0d1117" && echo "✓ Dark theme active in production"
curl -s https://leo-capvano.github.io/assets/main.css | grep -q "#f0883e" && echo "✓ Orange accents active in production"
curl -s https://leo-capvano.github.io/assets/main.css | grep -q "#58a6ff" && echo "✓ Blue accents active in production"
```

### GitHub Pages Build Status

Monitor the automated build:

1. Go to: https://github.com/leo-capvano/leo-capvano.github.io/actions
2. Check the latest workflow run
3. Look for the "pages build and deployment" workflow
4. Verify it shows a ✓ green checkmark

### Production Verification Checklist

After pushing changes, verify:

- [ ] GitHub Actions "pages build and deployment" workflow succeeds (green checkmark)
- [ ] Site loads at https://leo-capvano.github.io (HTTP 200)
- [ ] CSS file is served (check Network tab in DevTools)
- [ ] Dark theme colors are visible
- [ ] All sections render correctly
- [ ] Responsive design works on mobile/tablet
- [ ] No 404 errors in console

## Project Structure

```
.
├── _config.yml                 # Jekyll configuration
├── _sass/
│   └── minima/
│       ├── custom-variables.scss   # SCSS design tokens (colors, spacing, fonts)
│       └── custom.scss             # Component styling (hero, cards, grid, etc.)
├── assets/
│   └── main.scss               # SCSS entry point
├── index.md                    # Site content (Markdown)
├── Gemfile                     # Ruby dependencies
├── Gemfile.lock                # Locked dependency versions
└── _site/                      # Build output (auto-generated)
```

## Customization

### Colors

Edit `_sass/minima/custom-variables.scss`:

```scss
// Main colors
$color-dark-bg: #0d1117;      // Main background
$color-orange: #f0883e;       // Accents & CTAs
$color-blue: #58a6ff;         // Links & highlights
$color-text: #e6edf3;         // Main text
```

### Typography

```scss
// Fonts
$font-family-base: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
$font-family-mono: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, monospace;
```

### Spacing

```scss
// Spacing scale
$spacing-xs: 0.25rem;
$spacing-sm: 0.5rem;
$spacing-md: 1rem;
$spacing-lg: 1.5rem;
$spacing-xl: 2rem;
```

### Responsive Breakpoints

Edit the media queries in `_sass/minima/custom.scss`:

```scss
// Tablet (768px - 1023px)
@media (max-width: 1023px) { }

// Mobile (<768px)
@media (max-width: 767px) { }
```

## Troubleshooting

### Build Fails with Ruby Version Error

**Error**: `Gem::Requirement` or similar Ruby version error

**Solution**:
```bash
# Check installed Ruby versions
rbenv versions

# Install Ruby 3.x (using rbenv or Homebrew)
brew install ruby@3.3
rbenv install 3.3.0

# Set local Ruby version
rbenv local 3.3.0
bundle install
```

### CSS Not Updating

**Problem**: Changes to SCSS files don't appear after rebuild

**Solution**:
1. Stop the development server (Ctrl+C)
2. Clear the build cache:
   ```bash
   rm -rf _site/
   ```
3. Restart the development server:
   ```bash
   bundle exec jekyll serve
   ```

### Site Not Loading Locally

**Problem**: `http://localhost:4000` shows connection refused

**Solution**:
1. Verify the server is running (should see "Server running at http://localhost:4000/")
2. Check port 4000 isn't in use:
   ```bash
   lsof -i :4000
   ```
3. Kill existing process if needed:
   ```bash
   kill -9 <PID>
   ```
4. Restart the server

### GitHub Pages Build Fails

**Problem**: GitHub Actions workflow shows ✗ red X

**Solution**:
1. Check the workflow logs: https://github.com/leo-capvano/leo-capvano.github.io/actions
2. Look for SCSS compilation errors
3. Verify `Gemfile.lock` is committed
4. Try rebuilding locally first to catch errors early

## Performance Metrics

### Local Build Time
- ~1-2 seconds for initial build
- <1 second for incremental rebuilds (with `jekyll serve`)

### CSS File Size
- **Compiled CSS**: ~11 KB (minified by GitHub Pages)
- **Network**: <50 KB (with gzip compression)

### Page Load
- **First Contentful Paint (FCP)**: <1s
- **Largest Contentful Paint (LCP)**: <2s

## Deployment

### Automatic Deployment

Changes are automatically deployed when you push to the `main` branch:

```bash
git add .
git commit -m "Your commit message"
git push origin main
```

GitHub Actions will automatically:
1. Build the Jekyll site
2. Compile SCSS to CSS
3. Deploy to GitHub Pages
4. Update the live site at https://leo-capvano.github.io

### Manual Verification

Check deployment status:

```bash
# View latest builds
gh run list --repo leo-capvano/leo-capvano.github.io

# View specific run details
gh run view <run-id>
```

## Development Workflow

### Making Changes

1. **Edit files** (content or styling):
   ```bash
   # Edit content
   nano index.md
   
   # Edit styles
   nano _sass/minima/custom-variables.scss
   nano _sass/minima/custom.scss
   ```

2. **View changes locally**:
   - Server auto-reloads (watch for console output)
   - Refresh browser to see changes

3. **Test responsiveness**:
   - DevTools device toolbar (F12 → toggle device toolbar)
   - Test at multiple breakpoints

4. **Commit and push**:
   ```bash
   git add .
   git commit -m "feat: add new feature"
   git push origin main
   ```

### Common Development Tasks

**Update project information**:
- Edit the project cards in `index.md`
- Add new project section or update descriptions

**Change colors**:
- Update `$color-*` variables in `_sass/minima/custom-variables.scss`
- All usages automatically update

**Add new tech tag**:
- Add to the technology section in `index.md`
- Use the `.tech-tag` class in Markdown or HTML

**Adjust spacing/typography**:
- Update `$spacing-*` or `$font-size-*` variables
- Affects all components globally

## Resources

- **Jekyll Documentation**: https://jekyllrb.com/docs/
- **Minima Theme**: https://github.com/jekyll/minima
- **GitHub Pages**: https://pages.github.com/
- **Sass/SCSS Guide**: https://sass-lang.com/guide

## Support

For issues or questions:

1. Check this README's troubleshooting section
2. Review GitHub Issues: https://github.com/leo-capvano/leo-capvano.github.io/issues
3. Consult Jekyll documentation

## License

This portfolio is based on the [Minima](https://github.com/jekyll/minima) theme and is available under the same license.

---

**Last Updated**: May 3, 2026  
**Status**: ✓ Live on GitHub Pages
