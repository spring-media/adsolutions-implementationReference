# Performance improvements Ad Solutions

## goldenekamera.de

We were working hard to improve the performance and the loading time of the ads and of our external libraries.

For this, the publisher only has to make the following small changes.

## Step 1
### **_Required_** - New Version of the AdLib

Please replace the old AdLib JS-Url:

```html
https://acdn.adnxs.com/as/1h/pages/goldenekamera.js
```

With the following AdLib JS-Url:

```html
https://www.asadcdn.com/adlib/pages/goldenekamera.js
```

*Please make this change until the 15th march 2019*

## Step 2
### **_Strong Recommended_** - Please add dns-prefetch- and preconnect for the ad-domains in HEAD

```html
<link rel="dns-prefetch" href="//www.asadcdn.com"/>
<link rel="preconnect" href="//www.asadcdn.com"/>
```

## Step 3
### **_Required_** article flag in the adsetup

Please add the following flag in the adSSetup JUST on article pages

```html
adSSetup

isArticle: true, // it shows us if the page is an article

```
[See documentation](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md)

## Help

If you have some questions don't hesitate to contact us:

__Carlos Bracho__

Head of Ad Technology
Spring Media

Tel: +49 30 2591 76784
Mobile: +49 151 44619807
carlos.bracho@axelspringer.de

__Rene Baudisch__

Ad Technology Manager
Spring Media

Tel: +49 30 2591 76731
rene.baudisch@axelspringer.de

__Ad Technology Team__
adtechnology@axelspringer.de
