# Integration - Appnexus Accelerated Mobile Pages


## Basic single ad
```html
<amp-ad width=300 height=250
  type="appnexus"
  data-member="7823"
  disablePsa="true"
  data-code="mywebsite.de-amp-ressort_story-mrec"
  >
</amp-ad>
```
### Notes
- The standard size for Ads on AMP ist 300x250 (mrec), if you need extra sizes please contact us.
- data-member has an static value, please don't change it. 
- Please don't forget to send us a fallback ad in order to avoid white spaces on you AMP Site. If you don't have any fallback ad please change disablePsa="true" to disablePsa="false", after doing it you will get fallback ads from Appnexus.
- data-code is a combination of the following information:
    - Website --> mywebsite.de
    - amp --> it is the platform, please don't change it
    - ressort_story --> it is the adlevel "Vertaggung" from you CMS. It is the same value used for the other platforms. 
    - Placement --> actually we just use the placement "mrec" for AMP, if you need of them please contact us.


### Help

If you have some question don't hesitate to contact us:


__Timo Nolte__
 
  Head of AdSolutions
  Corporate Digital Platforms

  Tel: +49 30 2591 78009
  Mobile: +49 151 22334646 
  timo.nolte@axelspringer.de


__Carlos Bracho__
 
  Senior Ad Technology Lead 
  Corporate Digital Platforms
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de
  