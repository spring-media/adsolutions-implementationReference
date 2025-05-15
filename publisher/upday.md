# upday - Ad Integration Guide

Welcome to the Ad Integration documentation for upday.

In this document, you will learn how to implement AdLib on upday.com to ensure optimal ad delivery and monetization.

---

## Table of contents

- [Basic Setup](#basic-setup)
   - [1. Include the AdLib](#1-include-the-adlib)
   - [2. Configure AdSSetup](#2-configure-adssetup)
      - [AdSSetup.adSlotSizes - Desktop](#adssetupadslotsizes---desktop)
      - [AdSSetup.adSlotSizes - Mobile](#adssetupadslotsizes---mobile)
   - [3. Provide Ad Slots](#3-provide-ad-slots)
- [Help](#help)

---

## Basic Setup

There are only three critical steps for a basic ad integration:

### 1. Include the AdLib

AdLib is the core component for ad delivery. It must be included in the **header** of the website, **as high as possible**, but **below the CMP stub**.

```html
<html>
<head>
    <title>Upday</title>
    <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/upday.js"></script>
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
        adPlacements: [ ... ], // see below
        adSlotSizes: { ... }, // see below
        placeholder: { ... },
        colorBg: true,
        bgClick: true,
        hasVideoPlayer: false,
        isArticle: true,
        pageName: "Newsite_WebINT",
        target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;" // important: set context relevant values and key-values here; should be specific for every article
    }
</script>
```

**Important**: Please make sure that parameter target contains all relevant content keywords...

For a detailed explanation of `adSSetup` parameters, see [this reference](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/adSSetup-in-detail.md).

#### AdSSetup.adSlotSizes - Desktop

```javascript
adSSetup = {
    "adPlacements": ["googletag-desktop-div-gpt-ad-desktoparticle-1", "googletag-desktop-div-gpt-ad-desktoparticle-2", "googletag-desktop-div-gpt-ad-desktoparticle-3", "googletag-desktop-div-gpt-ad-desktoparticle-4"],
    "adSlotSizes": {
        "googletag-desktop-div-gpt-ad-desktoparticle-1": [{ "minWidth": 1, "sizes": [[300,600], [300,300], [300,250]], [300,75]], [320,160], [320,75], [320,50] }],
        "googletag-desktop-div-gpt-ad-desktoparticle-2": [{ "minWidth": 1, "sizes": [[300,600], [300,300], [300,250]], [300,75]], [320,160], [320,75], [320,50] }],
        "googletag-desktop-div-gpt-ad-desktoparticle-3": [{ "minWidth": 1, "sizes": [[300,600], [300,300], [300,250]], [300,75]], [320,160], [320,75], [320,50] }],
        "googletag-desktop-div-gpt-ad-desktoparticle-4": [{ "minWidth": 1, "sizes": [[300,600], [300,300], [300,250]], [300,75]], [320,160], [320,75], [320,50] }]
    }
}
```

#### AdSSetup.adSlotSizes - Mobile

```javascript
adSSetup = {
    "adPlacements": ["googletag-mobile-div-gpt-ad-mobilearticle-1", "googletag-mobile-div-gpt-ad-mobilearticle-2", "googletag-mobile-div-gpt-ad-mobilearticle-3", "googletag-mobile-div-gpt-ad-mobilearticle-4"],
    "adSlotSizes": {
        "googletag-mobile-div-gpt-ad-mobilearticle-1": [{ "minWidth": 1, "sizes": [[300,600], [300,300], [300,250]], [300,75]], [320,160], [320,75], [320,50] }],
        "googletag-mobile-div-gpt-ad-mobilearticle-2": [{ "minWidth": 1, "sizes": [[300,600], [300,300], [300,250]], [300,75]], [320,160], [320,75], [320,50] }],
        "googletag-mobile-div-gpt-ad-mobilearticle-3": [{ "minWidth": 1, "sizes": [[300,600], [300,300], [300,250]], [300,75]], [320,160], [320,75], [320,50] }],
        "googletag-mobile-div-gpt-ad-mobilearticle-4": [{ "minWidth": 1, "sizes": [[300,600], [300,300], [300,250]], [300,75]], [320,160], [320,75], [320,50] }]
    }
}
```

---

### 3. Provide Ad Slots

Ad containers must be provided for each requested ad placement.

```html
<div id="mrecWrapper">
    <div id="mrec"></div>
</div>
```

Once completed, your **basic AdLib integration is live**.

---

## Help

If you have any questions, contact the **Ad Technology Team**:

📧 **adtechnology@axelspringer.de**
