# Integration - Appnexus Accelerated Mobile Pages


## Basic single ad
```html
<amp-ad width=300 height=250
        type="appnexus"
        data-member="7823"
        data-code="mywebsite.de-amp-ressort_story-mrec"
></amp-ad>
```

## connected ads
```html
<amp-ad width=300 height=250
        type="appnexus"
        data-target="mrec"
        json='{
            "pageOpts": {
                "member": 7823
            },
            "adUnits": [{
                "disablePsa": true,
                "invCode": "mywebsite.de-amp-ressort_story-mrec",
                "sizes": [[300, 250]],
                "keywords": {
                    "misc": ["rock", "pop"]
                },
                "targetId": "mrec"
            },{
                "disablePsa": true,
                "invCode": "mywebsite.de-amp-ressort_story-mrec",
                "sizes": [[300, 250]],
                "keywords": {
                    "misc": ["rock", "pop"]
                },
                "targetId": "mrec_2"
            }]
        }'
></amp-ad>
```
### Notes
- We're using the regular integration of appnexus full md found [here](https://github.com/ampproject/amphtml/blob/master/ads/appnexus.md)
- The standard size for Ads on AMP ist 300x250 (mrec), if you need extra sizes please contact us.
- data-target is the placement name. e.g. for Medium Rectangle should be "mrec" 
- data-code / JSON:
    - member is a static value, please don't change it 
    - Please don't forget to send us a fallback ad in order to avoid white spaces on you AMP Site. If you don't have any fallback ad please change disablePsa="true" to disablePsa="false", after doing it you will get fallback ads from Appnexus.
    - invCode is a combination of the following information:
        - Website --> mywebsite.de
        - amp --> it is the platform, please don't change it
        - ressort_story --> it is the adlevel "Vertaggung" from you CMS. It is the same value used for the other platforms. 
        - Placement --> actually we just use the placement "mrec" for AMP, if you need of them please contact us.
    - sizes ist the size of the ad. Actually ist the same size of the Amp container
    - keywords --> if you want to send keywords, please us the object "kw_misc" and place every keyword comma separated. 
    - targetId has the same value of data-target.


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
  
