# Modern Resume Theme

A modern, responsive resume/CV theme built with Jekyll.

## Features

- Clean, professional design
- Responsive layout that works on all devices
- Easy to customize with YAML configuration
- Support for multiple sections (Projects, Experience, Education, etc.)
- Optimized Bootstrap grid (only the necessary CSS is included)
- Print-friendly styling
- SEO optimized

## Bootstrap Optimization

This theme has been optimized to use only the Bootstrap CSS rules that are actually needed, rather than loading the entire Bootstrap library. This results in:

- **~90% reduction in CSS file size** (from ~120KB to ~10-15KB)
- **Faster page load times**
- **Better performance**
- **No external CDN dependencies**

### How It Works

Instead of loading the full Bootstrap CSS from a CDN:
```html
<!-- OLD: Full Bootstrap (120KB) -->
<link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" rel="stylesheet">
```

This theme now includes only the Bootstrap grid system classes that are actually used, defined in `_sass/bootstrap-grid.scss`. This custom file contains only:
- Container styles
- Row and clearfix utilities
- Column classes (col-xs-*, col-sm-*, col-md-*, col-lg-*)
- Print-specific column classes

### Learn More

For a detailed guide on how to identify and extract only the CSS rules your webpage is using from Bootstrap, see:

**[BOOTSTRAP_OPTIMIZATION.md](BOOTSTRAP_OPTIMIZATION.md)**

This guide includes:
- Step-by-step instructions using browser DevTools
- How to use the Coverage tool to identify unused CSS
- Manual extraction methods
- Automated approaches using PurgeCSS
- Complete implementation steps

## Quick Start

1. Fork this repository
2. Update `_config.yml` with your information
3. Customize the content sections
4. Build and deploy

## Development

```bash
# Install dependencies
bundle install

# Serve the site locally
bundle exec jekyll serve
```

Then open http://localhost:4000 in your browser.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.

## License

This project is licensed under the MIT License.
