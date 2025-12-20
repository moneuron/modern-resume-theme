# Bootstrap CSS Optimization Guide

This guide explains how to identify and extract only the Bootstrap CSS rules that are actually used by this theme, allowing you to create a custom, lightweight CSS file instead of loading the entire Bootstrap library.

## Current Bootstrap Usage

This theme currently loads Bootstrap 3.3.5 from CDN:
```html
<link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" rel="stylesheet" crossorigin="anonymous">
```

However, the theme only uses a small subset of Bootstrap's features, primarily the **grid system**.

## Bootstrap Classes Used in This Theme

The theme uses the following Bootstrap classes:

### Grid System
- `container` - Fixed-width container
- `row` - Grid row wrapper
- `clearfix` - Clear floats

### Column Classes
- `col-xs-*` - Extra small devices (phones, <768px)
  - `col-xs-8`, `col-xs-12`
- `col-sm-*` - Small devices (tablets, ≥768px)
  - `col-sm-4`, `col-sm-6`, `col-sm-8`, `col-sm-9`
- `col-md-*` - Medium devices (desktops, ≥992px)
  - `col-md-3`, `col-md-4`, `col-md-9`, `col-md-10`, `col-md-12`
- `col-lg-*` - Large devices (large desktops, ≥1200px)
  - `col-lg-3`
- `col-print-12` - Print-specific column class

## Method 1: Using Browser DevTools to Identify Used CSS

### Step-by-Step Instructions

1. **Build and serve the site locally**
   ```bash
   bundle install
   bundle exec jekyll serve
   ```

2. **Open the site in your browser**
   - Navigate to `http://localhost:4000`

3. **Open Browser DevTools**
   - Chrome/Edge: Press `F12` or `Ctrl+Shift+I` (Windows/Linux) or `Cmd+Option+I` (Mac)
   - Firefox: Press `F12` or `Ctrl+Shift+I` (Windows/Linux) or `Cmd+Option+I` (Mac)
   - Safari: Enable Developer menu in Preferences, then press `Cmd+Option+I`

4. **Use the Coverage Tool (Chrome/Edge)**
   - Open DevTools
   - Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (Mac) to open the Command Menu
   - Type "Coverage" and select "Show Coverage"
   - Click the reload button in the Coverage panel
   - Look for `bootstrap.min.css` in the list
   - Click on it to see which CSS rules are actually used (shown in green) vs unused (shown in red)

5. **Inspect Individual Elements**
   - Right-click on any element on the page
   - Select "Inspect" or "Inspect Element"
   - In the Styles panel, you can see all CSS rules applied to that element
   - Rules from Bootstrap will be labeled with the stylesheet name `bootstrap.min.css`

6. **Filter Bootstrap Rules**
   - In the Styles panel, you can click on the stylesheet name to view the full file
   - Used rules will be highlighted or marked
   - You can copy these rules to your custom CSS file

### Using Firefox's Inspector

1. Open DevTools (`F12`)
2. Go to the Inspector tab
3. Select any element
4. In the Rules panel, you'll see all CSS rules applied
5. Look for rules coming from `bootstrap.min.css`
6. Click the stylesheet link to view the full file
7. Firefox shows line numbers for each rule - note which ones are applied

## Method 2: Extract Only Required Bootstrap CSS

Based on the analysis, here are the Bootstrap components actually used:

### Required Bootstrap CSS Rules

Create a new file `_sass/bootstrap-grid.scss` with only the necessary Bootstrap grid CSS:

```scss
// Bootstrap 3 Grid System - Extracted Rules Only
// Based on Bootstrap 3.3.5

// Container
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 15px;
  padding-right: 15px;
}

@media (min-width: 768px) {
  .container {
    width: 750px;
  }
}

@media (min-width: 992px) {
  .container {
    width: 970px;
  }
}

@media (min-width: 1200px) {
  .container {
    width: 1170px;
  }
}

// Row
.row {
  margin-left: -15px;
  margin-right: -15px;
}

.row:before,
.row:after {
  content: " ";
  display: table;
}

.row:after {
  clear: both;
}

// Clearfix
.clearfix:before,
.clearfix:after {
  content: " ";
  display: table;
}

.clearfix:after {
  clear: both;
}

// Common column styles
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1,
.col-xs-2, .col-sm-2, .col-md-2, .col-lg-2,
.col-xs-3, .col-sm-3, .col-md-3, .col-lg-3,
.col-xs-4, .col-sm-4, .col-md-4, .col-lg-4,
.col-xs-5, .col-sm-5, .col-md-5, .col-lg-5,
.col-xs-6, .col-sm-6, .col-md-6, .col-lg-6,
.col-xs-7, .col-sm-7, .col-md-7, .col-lg-7,
.col-xs-8, .col-sm-8, .col-md-8, .col-lg-8,
.col-xs-9, .col-sm-9, .col-md-9, .col-lg-9,
.col-xs-10, .col-sm-10, .col-md-10, .col-lg-10,
.col-xs-11, .col-sm-11, .col-md-11, .col-lg-11,
.col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 15px;
  padding-right: 15px;
}

// XS columns (mobile first, always applied)
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4,
.col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8,
.col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}

.col-xs-8 {
  width: 66.66666667%;
}

.col-xs-12 {
  width: 100%;
}

// SM columns (tablets and up)
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4,
  .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8,
  .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }

  .col-sm-4 {
    width: 33.33333333%;
  }

  .col-sm-6 {
    width: 50%;
  }

  .col-sm-8 {
    width: 66.66666667%;
  }

  .col-sm-9 {
    width: 75%;
  }
}

// MD columns (desktops and up)
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4,
  .col-md-5, .col-md-6, .col-md-7, .col-md-8,
  .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }

  .col-md-3 {
    width: 25%;
  }

  .col-md-4 {
    width: 33.33333333%;
  }

  .col-md-9 {
    width: 75%;
  }

  .col-md-10 {
    width: 83.33333333%;
  }

  .col-md-12 {
    width: 100%;
  }
}

// LG columns (large desktops and up)
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4,
  .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8,
  .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }

  .col-lg-3 {
    width: 25%;
  }
}

// Print columns
@media print {
  .col-print-12 {
    width: 100%;
    float: left;
  }
}
```

## Method 3: Using PurgeCSS (Automated Approach)

For a more automated approach, you can use PurgeCSS to automatically remove unused CSS:

### Installation

```bash
npm install -D purgecss
```

### Configuration

Create a `purgecss.config.js` file:

```javascript
module.exports = {
  content: [
    './_layouts/**/*.html',
    './_includes/**/*.html',
    './_site/**/*.html',
  ],
  css: [
    'https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css'
  ],
  output: './_sass/bootstrap-purged.css'
}
```

### Run PurgeCSS

```bash
npx purgecss --config ./purgecss.config.js
```

This will create a new CSS file with only the Bootstrap rules that are actually used.

## Implementation Steps

Once you've extracted the necessary Bootstrap CSS:

1. **Create the custom Bootstrap file**
   - Create `_sass/bootstrap-grid.scss` with the extracted rules (shown above)

2. **Import it in your main SCSS file**
   - Add `@import "bootstrap-grid";` to `_sass/modern-resume-theme.scss`

3. **Remove the Bootstrap CDN link**
   - Edit `_includes/head.html`
   - Remove or comment out the Bootstrap CDN link:
   ```html
   <!-- <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" rel="stylesheet" crossorigin="anonymous"> -->
   ```

4. **Test your site**
   - Build and serve the site locally
   - Check all pages and responsive breakpoints
   - Ensure the layout looks identical to before

## Benefits of This Approach

- **Reduced file size**: Bootstrap 3.3.5 full CSS is ~120KB minified. The grid-only version is ~10-15KB
- **Faster page load**: Smaller CSS file means faster download and parsing
- **Better performance**: Less CSS for the browser to process
- **More control**: You have the exact CSS rules in your codebase
- **No external dependencies**: No reliance on CDN availability

## Maintenance Notes

- If you add new Bootstrap classes to your HTML, remember to add the corresponding CSS rules to your custom file
- Keep track of which Bootstrap version you're extracting from for consistency
- Test thoroughly after making changes, especially on different screen sizes

## Alternative: Modern CSS Grid

For new projects, consider replacing Bootstrap's grid system with modern CSS Grid or Flexbox, which are now well-supported in all browsers and don't require any framework.
