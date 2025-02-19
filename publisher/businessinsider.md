# Business Insider - Ad Integration Guide

> ⚠️ **Caution:** The required `.js` file for this integration has not yet been created. This will be created together during the integration phase.

Welcome to the Ad Integration documentation for Business Insider!

In this document, you will learn how to implement AdLib on BusinessInsider.com to ensure optimal ad delivery and monetization.

---

## Table of contents

- [Strategy](#strategy)
   - [Removing Internal Ad Components](#removing-internal-ad-components)
   - [Pagename Structure](#pagename-structure)
   - [Programmatic Advertising](#programmatic-advertising)
- [Basic Setup](#basic-setup)
   - [1. Include the AdLib](#1-include-the-adlib)
   - [2. Configure AdSSetup](#2-configure-adssetup)
      - [AdSSetup.adSlotSizes - Desktop](#adssetupadslotsizes---desktop)
      - [AdSSetup.adSlotSizes - Mobile](#adssetupadslotsizes---mobile)
   - [3. Provide Ad Slots](#3-provide-ad-slots)
- [Help](#help)

---

## Strategy

### Removing Internal Ad Components

To integrate AdLib correctly on BusinessInsider.com, **all internal ad components must be removed**. All ad placements and delivery should run through AdLib. To facilitate this transition, **we require full access** to analyze and configure the ad setup appropriately.

### Pagename Structure

AdLib will automatically support the existing pagename structure. No changes are required, as AdLib will handle pagename assignment and mapping within the ad server.

### Programmatic Advertising

Ensure that the `partners` flag in `adSSetup` is set to `true`, as this setting will activate all programmatic advertising, including Magnite and Amazon TAM. If you do not wish to use this setting, it is okay for us; we can activate programmatic across the entire website.

---

## Basic Setup

There are only three critical steps for a basic ad integration:

### 1. Include the AdLib

AdLib is the core component for ad delivery. It must be included in the **header** of the website, **as high as possible**, but **below the CMP stub**.

```html
<html>
<head>
    <title>Business Insider</title>
    <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/businessinsider.js"></script>
</head>
<body>
    <div class="your-content">...</div>
</body>
</html>
```

**Important**: Do **not** load AdLib asynchronously, as this can cause [cumulative layout shifts](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) and revenue loss.

---

### 2. Configure AdSSetup

The `adSSetup` object acts as a configuration for ad delivery.

```html
<script type="text/javascript">
    adSSetup = {
        view: "d",
        partners: true,
        adPlacements: ["superbanner", "sky", "mrec"],
        adSlotSizes: { ... },
        placeholder: { ... },
        colorBg: true,
        bgClick: true,
        hasVideoPlayer: false,
        isArticle: true,
        pageName: "news_story",
        target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;"
    }
</script>
```

For a detailed explanation of `adSSetup` parameters, see [this reference](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/adSSetup-in-detail.md).

#### AdSSetup.adSlotSizes - Desktop

```javascript
adSSetup = {
    "adPlacements": ["superbanner", "sky", "mrec", "mrec_btf"],
    "adSlotSizes": { 
        "superbanner": [{ "minWidth": 1, "sizes": [[728, 90], [728, 600]] }], 
        "sky": [{ "minWidth": 1, "sizes": [[160, 600], [120, 600], [300, 600]] }],
        "mrec": [{ "minWidth": 1, "sizes": [[300,250]] }],
        "mrec_btf": [{ "minWidth": 1, "sizes": [[300,250]] }],
    }
}
```

#### AdSSetup.adSlotSizes - Mobile

```javascript
adSSetup = {
    "adPlacements": ["mrec", "mrec_btf"],
    "adSlotSizes": { 
        "mrec": [{ "minWidth": 1, "sizes": [[320,160], [300,300], [300,250]] }],
        "mrec_btf": [{ "minWidth": 1, "sizes": [[320,160], [300,300], [300,250]] }],
    }
}
```

---

### 3. Provide Ad Slots

Ad containers must be provided for each requested ad placement.

```html
<div id="superbannerWrapper">
    <div id="superbanner"></div>
</div>
```

Once completed, your **basic AdLib integration is live**.

---

## Help

If you have any questions, contact the **Ad Technology Team**:

📧 **adtechnology@axelspringer.de**