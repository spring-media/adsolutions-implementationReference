🚧 Work in Progress 🚧


# Relaunch Requirements - Page Structure (Inner/Outer Wrapper)

## Goal

The goal for this document is for you to learn what to keep in mind when planning a relaunch for a website with an active Adlib integration.
The AdLib requires correct selectors for inner and outer wrappers to properly center and position special formats (e.g. Fireplace, Wallpaper, Sitebar, ...).

## Why Inner/Outer Wrapper?

The AdLib uses the wrapper structure to:
- **Determine page width** (for responsive ads)
- **Center content** (for special formats)
- **Position ads correctly** (outside/inside content)

## Typical Page Structure

```html
<body>
  <!-- OuterWrapper: Entire page container -->
  <div id="page" class="page-wrapper">
    
    <!-- Navigation (outside InnerWrapper) -->
    <nav class="main-navigation">...</nav>
    
    <!-- Superbanner (outside InnerWrapper) -->
    <div id="superbanner"></div>
    
    <!-- InnerWrapper: Content area -->
    <div id="content" class="content-wrapper">
      
      <article>
        <h1>Article Title</h1>
        <p>Content...</p>
        
        <!-- Mrec (inside InnerWrapper) -->
        <div id="mrec"></div>
      </article>
      
    </div>
    
    <!-- Sky (outside InnerWrapper, but inside OuterWrapper) -->
    <div id="sky"></div>
    
  </div>
</body>
```

## InnerWrapper Selector

### Definition
The **InnerWrapper** is the main content area of the page (usually `<main>`, `#content`, `.content-wrapper`).
While the content is often centered per default, one of the biggest reasons for this selector construct are cases where the inner wrapper is not centered, so we can detect where to place certain ad elements.

### Requirements
- ✅ **Fixed width** (e.g., 1000px, 1200px) or **max-width**
- ✅ **Contains article content**
- ❌ **NOT** `<body>` as selector


### Superbanner Placement
**Important:** Superbanner must be **outside** the InnerWrapper!

```html
<!-- ✅ CORRECT -->
<div id="page">
  <div id="superbanner"></div>  <!-- Outside -->
  <div id="content">
    <article>Content...</article>
  </div>
</div>

<!-- ❌ WRONG -->
<div id="page">
  <div id="content">
    <div id="superbanner"></div>  <!-- Inside -->
    <article>Content...</article>
  </div>
</div>
```

**Important:** Superbanner must be exactly as wide as the InnerWrapper to correctly center special formats (Fireplace, Wallpaper).

## OuterWrapper Selector

### Definition
The **OuterWrapper** is the outermost container of the page (usually `#page`, `.page-wrapper`, `#root`).

### Requirements
- ✅ **Wraps entire page**
- ✅ **Contains inner and outer wrapper**
- ❌ **NOT** `<body>` as selector

### Why not `<body>`?

**Problem:** `<body>` often has no fixed width and cannot be used for centering.

```html
<!-- ❌ WRONG -->
<body>  <!-- No wrapper -->
  <nav>...</nav>
  <div id="superbanner"></div>
  <article>Content...</article>
</body>

<!-- ✅ CORRECT -->
<body>
  <div id="page">  <!-- OuterWrapper -->
    <nav>...</nav>
    <div id="superbanner"></div>
    <div id="content">  <!-- InnerWrapper -->
      <article>Content...</article>
    </div>
  </div>
</body>
```

## Complete Example

```html
<!DOCTYPE html>
<html>
<head>
  <script>
    window.adSSetup = {
      view: "d",
      partners: true,
      adPlacements: ["superbanner", "sky", "mrec"],
      pageName: "home_index",
      adSlotSizes: {
        superbanner: [{ minWidth: 1, sizes: [[728, 90], [728, 600], [1000, 600]] }],
        sky: [{ minWidth: 1, sizes: [[160, 600], [300, 600]] }],
        mrec: [{ minWidth: 1, sizes: [[300, 250], [300, 600]] }]
      }
    };
  </script>
  <script src="https://www.asadcdn.com/adlib/pages/{publisher}.js"></script>
  
  <style>
    #page {
      width: 100%;
      max-width: 1400px;
      margin: 0 auto;
    }
    #content {
      width: 1000px;
      margin: 0 auto;
    }
  </style>
</head>
<body>
  <div id="page">
    <nav>Navigation</nav>
    <div id="superbanner"></div>
    <div id="content">
      <article>
        <h1>Article</h1>
        <p>Content...</p>
        <div id="mrec"></div>
      </article>
    </div>
    <div id="sky"></div>
  </div>
</body>
</html>
```

## Acceptance Criteria

- [ ] InnerWrapper selector defined (not `<body>`)
- [ ] OuterWrapper selector defined (not `<body>`)
- [ ] InnerWrapper has fixed width or max-width
- [ ] Superbanner outside InnerWrapper
- [ ] Sky outside InnerWrapper
- [ ] Mrec inside InnerWrapper

## Troubleshooting

**Special formats not centered**
- Check: Does the InnerWrapper has a fixed width?
- Check: Has one of the selectors changed?
- Check: Is the Superbanner outside the InnerWrapper?

**Ads overlap content**
- Check: Are there Z-index conflicts?
