# What Is the Cumulative Layout Shift?

Google announced a new metric for its search engine ranking named Cumulative Layout Shift (CLS). We need to be complient with that, since it can effect our SEO ranking enormously.
The big requirement is that the websites must have a visual stability while rendering

The CLS is an unexpected shifting of web page elements while the page is rendering. 

![](layout-instability.gif)

Besides advertising, this concerns factors like videos, images and in general content which is loaded asynchronously.


# What we have done so far?

On our current development version of the adlib, we implemented CLS-placeholder for all concerning ad placements which for example results in a superbanner now having the space of a billboard. Ads that are smaller than the biggest possible format will now have a sticky-scroll feature to take a positive effect out of the additional available space.

Our implemented solution has a default styling which can be customized to specific needs, such as font family, positioning and colors. You can find more information about this below.


# What adjustments are required?

We are currently testing this feature with our adlib but in the near future it will be controlled directly by the adSSetup configuration on each page. So to get this all working, we need you to update your adSSetup object. 

There is a [new part](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#5-placeholder-settings) of the adSSetup:




# Example


```
placeholder: {
   disablePlaceholders: false,
   default: {	
      "border-color": "#EEEDE8",
      "background-color": "#F9F9F7",
      "admarkPosition": "bottom right",
      “color": "#BCBCBC",
      "font-size": "12px",
      "font-family": "Tahoma"
   },
   mrec: { 
      "bgColor": "#FCBFFF"
   }
}

```


# In Detail

### Disable Placeholders

`disablePlaceholders: false`

*You can set this parameter true on pages, were no CLS placeholder should be visible, such as special sponsorships and so on.*

### Default placeholder styling & admark positioning

```
default: {	
   "border-color": "#EEEDE8",
   "background-color": "#F9F9F7",
   "admarkPosition": "bottom right",
   “color": "#BCBCBC",
   "font-size": "12px",
   "font-family": "Tahoma"
},

```

*With these parameters you can control the css styling of the placeholder. "admarkPosition" handles the position, where the admark will be rendered - possible inputs are:*


![](/assets/admarkPosition.png)


*If you need a cls placeholder without an admark, you can hide it with the option "admarkPosition":"hidden".*


## Optional: Customize individual slots

*In case you need to configure a specific slot separately, you can create another object with the name of the respective slot next to the "default" object. In this object you can then insert the properties from the "default" object that you would like to overwrite with your own values.*


```
placeholder: {
   default: {	
      "border-color": "#EEEDE8",
      "background-color": "#F9F9F7",
      "admarkPosition": "bottom right",
      "color": "#BCBCBC",
      "font-size": "12px",
      "font-family": "Tahoma"
   },
   mrec: {
      "color": "#333333",
      "admarkPosition": "center center"
   },
   billboard: {
      "color": "#ffffff",
      "background": "#00bfff",
      "border-color": "#ff0000"
   },
},

```


# Sample of an updated adSSetup object

Here you can see the syntax for an updated adSSetup object sample. 

![](/assets/sample_cls_adssetup.png)
