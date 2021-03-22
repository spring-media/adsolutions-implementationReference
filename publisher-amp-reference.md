# Implementing AMP springAds Integration

The springAds setup differs a lot from any other AMP ads setup and is orientated by the regular display setup using adSSetup object for defining the environment and ads to be called.

Said that, first you will have to integrate a director amp-ad tag, declaring your ads and targets on page:

```html
<amp-ad height="1"
    type="springAds"
    data-adssetup='{
        "view": "amp",
        "partners": true,
        "adPlacements": ["banner","mrec","mrec_btf","mrec_btf_2"],
        "adSlotSizes": {
            "banner": [{
              "minWidth": 1,
              "sizes": [[320, 50], [9, 9]] // in this example banner is the first slot directly in view and therefore only allows one size (and 9x9 to enable programmatic) because it will not be resized by AMP
            }],
            "mrec": [{
              "minWidth": 1,
              "sizes": [[300, 250], [300, 300], [250, 250], [320, 160], [300, 150], [320, 50], [320, 75], [320, 80], [320, 100], [300, 100], [300, 50], [300, 75], [9, 9]]
            }],
            "mrec_btf": [{
              "minWidth": 1,
              "sizes": [[300, 250], [300, 300], [250, 250], [320, 160], [300, 150], [320, 50], [320, 75], [320, 80], [320, 100], [300, 100], [300, 50], [300, 75], [9, 9]]
            }]
        },
        "pageName": "demo_story",
        "publisher": "adtechnology.axelspringer.com",
        "target": "singleAds;multiAds;you;me;team=adtech,MIT;"
    }'>
</amp-ad>
```
As in normal web the next thing you will need are adslot, so fitting the adPlacements of the adslot you will have to implement these amp-ad-tags:

__IMPORTANT:__

_Unlike regular web \_btf will not dealed as sightloader seperatly since amp already only renders ads when next to the viewport_


```html
[...content...]
<-- static banner for first viewport that is not resizeable -->
<amp-ad width="320" height="50" type="springAds" data-adslot="banner"></amp-ad>
[...content...]
<-- dynamic banner for after first viewport that are allowed to be resized by AMP -->
<amp-ad width="100vw" layout="fluid" type="springAds" data-adslot="mrec"></amp-ad>
[...content...]
<-- dynamic banner for after first viewport that are allowed to be resized by AMP -->
<amp-ad width="100vw" layout="fluid" type="springAds" data-adslot="mrec_btf"></amp-ad>
[...content...]
<-- dynamic banner for after first viewport that are allowed to be resized by AMP -->
<amp-ad width="100vw" layout="fluid" type="springAds" data-adslot="mrec_btf_2"></amp-ad>
[...content...]
```

##  using amp-ads with a cmp

After an exhausting conversation with amp we got them provide a minimal TCData Object to the ad-frames.
You may follow the issue on [github](https://github.com/ampproject/amphtml/issues/30385).

AMP will now inject an __tcfapiLocator iframe but only if the cmp settings intends that.
So please make sure, your cmp settings lists the following line:

```
{
    ...
    exposesTcfApi: true,
    ...
}
```

The adtag then will look like this one:
```
<amp-ad width="100vw" layout="fluid" type="springAds" data-adslot="mrec" data-block-on-consent="_till_responded"></amp-ad>
```

The tcString then will automatically be passed to all relevant technologies the adlib will use or request.

## ads not in adSSetup / infinite scrolling
To inject an adslot you do not know it will surely be inserted into the article on pageload like for infinite scrolling pages you can just ad a new adslot. 
This is meant to trigger auctions and a single adload, so loading will take longer than for elements declared in adSSetup and they cannot be excluded by other campaigns on the same page impression anymore.

```
<-- dynamic banner for after first viewport that are allowed to be resized by AMP -->
<amp-ad width="100vw" height="fluid" type="springAds" data-adslot="mrec_btf_123"></amp-ad>
[...content...]
```


## AMP Story ads (work in progess - available soon)
For AMP Stories the amp-ad will be replaced by an amp-story-auto-ads wrapper.
Also please make sure your page loads this component:
```
<script async custom-element="amp-story-auto-ads" src="https://cdn.ampproject.org/v0/amp-story-auto-ads-0.1.js"></script>
```
The parameters will be still defined the same just in a different way, e.g.:
```
<amp-story-auto-ads>
<script type="application/json">
    {
        "ad-attributes": {
            "type": "springAds",
            "data-adslot": "stories"
        }
    }
</script>
</amp-story-auto-ads>
```

### Teads

Hardcoding method

As we are fully integrated with Google AMP, the Teads AMP tag has the following format when hardcoded:

```html
<amp-ad width=300 height=1 noloading type="teads" data-pid="PAGE_ID" layout="responsive"> 
        <div placeholder></div> 
</amp-ad>
```

The only parameter to update is the data-pid = PAGE_ID field.

AMP Script Parameters:

- width & height = format size – FIXED
- type = "teads" = AMP ID – FIXED
- data-pid = PAGE ID (PID) – MODIFIABLE
- layout = "responsive" = Responsive Template – FIXED

In order to center the player in landscape mode, add the following CSS parameter to the AMP CSS
container (amp-custom):
amp-ad { margin: auto }

AMP Tag location
One of the limits within an AMP environment is the effective sandboxing of all iFrames. This means we are
unable to dynamically select the best location for our player and it is up to you, as a publisher, to insert the
<amp-ad> element in the correct location on the page where the inRead player should be initialized.

(Excerpt from the teads manual)


### Notes
- data-adssetup / JSON:
    - Please don't forget to send us a fallback ad in order to avoid white spaces on you AMP Site. If you don't have any fallback ad please change disablePsa="true" to disablePsa="false", after doing it you will get fallback ads from Xandr.
    - keywords --> if you want to send keywords, please us the object "kw_misc" and place every keyword comma separated.


### Help

If you have some question don't hesitate to contact us:


__Ad Technology Team__
  adtechnology@axelspringer.de
  
