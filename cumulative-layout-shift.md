**Table of Contents**  

- [What Is the Cumulative Layout Shift?](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#what-is-the-cumulative-layout-shift)
- [What we have done so far?](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#what-we-have-done-so-far)
- [What adjustments are required?](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#what-adjustments-are-required)
	- [Example](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#example)
	- [In Detail](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#in-detail)
		- [Disable Placeholders](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#disable-placeholders)
		- [Default placeholder styling & admark positioning](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#default-placeholder-styling--admark-positioning)
		- [Hide Borders](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#hide-borders)
		- [Optional: Customize individual slots](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#optional-customize-individual-slots)
		- [Disable placeholder on single adslots](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#disable-placeholder-on-single-adslots)
	- [Sample of an updated adSSetup object](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#sample-of-an-updated-adssetup-object)
	- [Note: inactive placeholders on desktop home](#note-placeholders-are-inactive-on-desktop-homes-for-now)
- [Here's what else you may need to keep in mind as a publisher](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#heres-what-else-you-may-need-to-keep-in-mind-as-a-publisher)
- [Working on your own solution?](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#working-on-your-own-solution)
	- [What happens when you disable placeholders on your page?](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#what-happens-when-you-disable-placeholders-on-your-page)
	- [Further resources](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md#further-resources)




# What Is the Cumulative Layout Shift?

Google announced a new metric for its search engine ranking named Cumulative Layout Shift (CLS). We need to be complient with that, since it can effect our SEO ranking enormously.
The big requirement is that the websites must have a visual stability while rendering.

The CLS is an unexpected shifting of web page elements (often but not only while the page is rendering). 

![](assets/layout-instability.gif)

Besides advertising, this concerns factors like videos, images and in general content which is loaded asynchronously. 


# What we have done so far?

On our current development version of the adlib, we implemented CLS-placeholder for all concerning ad placements which for example results in a superbanner now having the space of a billboard. Ads that are smaller than the biggest possible format will now have a sticky-scroll feature to take a positive effect out of the additional available space.

Our implemented solution has a default styling which can be customized to specific needs, such as font family, positioning and colors. You can find more information about this below.


# What adjustments are required?

We are currently testing this feature with our adlib but in the near future it will be controlled directly by the adSSetup configuration on each page. So to get this all working, we need you to update your adSSetup object. 

There is a [new part](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#5-placeholder-settings) of the adSSetup:




## Example


```javascript
placeholder: {
   disablePlaceholders: false,
   default: {
		"border-color": "#EEEDE8",
		"border": "5px dotted blue", // optional, replaces border-color
		"background-color": "#F9F9F7",
		"after": "{content: 'ADVERTISMENT'}", // optional, replace "ANZEIGE" by your own CSS
		"before": "{...}", // optional
		"admarkPosition": "bottom right",
		"color": "#BCBCBC",
		"font-size": "12px",
		"font-family": "Tahoma",
		"clickUrl": "https://adtechnology.axelspringer.com" // optional
	},
	mrec: {
       "background-color": "#FCBFFF"
   }
}

```


## In Detail

### Disable Placeholders

`disablePlaceholders: false`

*You can set this parameter true on pages, were no CLS placeholder should be visible, such as special sponsorships or the home.*




### Default placeholder styling & admark positioning

```javascript
default: {	
	"border-color": "#EEEDE8",
	"border": "5px dotted blue", // optional, replaces border-color
	"background-color": "#F9F9F7",
	"after": "{content: 'ADVERTISMENT'}", // optional, replace "ANZEIGE" by your own CSS
	"before": "{...}", // optional
	"admarkPosition": "bottom right",
	"color": "#BCBCBC",
	"font-size": "12px",
	"font-family": "Tahoma",
	"clickUrl": "https://adtechnology.axelspringer.com" // optional
},

```


*With these parameters you can control the css styling of the placeholder. "admarkPosition" handles the position, where the admark will be rendered - possible inputs are:*


![](/assets/admarkPosition.png)


*If you need a cls placeholder without an admark, you can hide it with the option `"admarkPosition":"hidden"`.*


### Hide Borders

We support the Red-green-blue-alpha (RGBA) model for our placeholders.
RGBA color values are an extension of RGB color values with an alpha channel - which specifies the opacity of the color.

So with that you can (*for example*) set the border-color to be fully transparent / hidden:

`"border-color": "rgba(0,0,0,0)"`



### Optional: Customize individual slots

*In case you need to configure a specific slot separately, you can create another object with the name of the respective slot next to the "default" object. In this object you can then insert the properties from the "default" object that you would like to overwrite with your own values.*


```javascript
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
		"admarkPosition": "center center",
		"clickUrl": "https://adtechnology.axelspringer.com"
	},
	billboard: {
		"color": "#ffffff",
		"background-color": "#00bfff",
		"border-color": "#ff0000",
		"before": "{...}"
	},
},

```

### Disable placeholder on single adslots
You can now disable single placeholders on your page. Just like adding a custom color to specific adslot, you're now able to set the attribute "disable: true".
So this is how it would look like, if you wanted to disable the placeholder for your superbanner:

```javascript
placeholder: {
	disablePlaceholders: false,
	default: {	
		"border-color": "#EEEDE8",
		"border": "5px dotted blue", // optional, replaces border-color
		"background-color": "#F9F9F7",
		"after": "{content: 'ADVERTISMENT'}", // optional, replace "ANZEIGE" by your own CSS
		"before": "{...}}", // optional
		"admarkPosition": "bottom right",
		"color": "#BCBCBC",
		"font-size": "12px",
		"font-family": "Tahoma",
		"clickUrl": "https://adtechnology.axelspringer.com" // optional
	},
	superbanner: { 
		disable: true
	}
}

```




## Sample of an updated adSSetup object

Here you can see the syntax for an updated adSSetup object sample. 

![](/assets/sample_cls_adssetup.png)




## Note: placeholders are inactive on desktop homes for now

You may wonder why there are no placeholders active on the Desktop Homes, even though you have implemented the object correctly.
After a long discussion the decision was made that the placeholders on the desktop homes of the publishers are switched off for now.

The background to this is that Google has only gone live with the Core Web Vitals on mobile and has delayed the go-live for desktop. In addition, the impact on SEO traffic is expected to be lower there.

As soon as something changes or there are other news from Google, we will re-evaluate the situation.





# Here's what else you may need to keep in mind as a publisher

- Be sure that your inpage container is at the end of your page to prevent big CLS placeholders at the front of your page
- Besides ads, other factors can also influence the CLS. Besides larger elements such as images and videos, factors like asynchronously loaded fonts should also be considered
- Check if there is dynamically injected content or content which is waiting for a network response before updating the DOM
- CLS only counts shifts visible in the viewport. If something moves below the fold and the user does not see it, a shift won’t affect CLS 
- Intentional layout shifts won't affect CLS, since the measurement stops for 500ms after every user interaction within the site



# Working on your own solution?

If you're working on your own solution to handle CLS placeholder, there are two points to consider:

1. To disable the placeholder features of the adlib, you need to include the placeholder-object in your adSSetup and set `disablePlaceholders: false` as described above. Otherwise, if no placeholder object is defined in your adSSetup, our adlib may return default values and sets placeholder on its own.
2. If you can't or want include the placeholder object to disable its functions, you need to contact adtechnology@axelspringer.com. We can disable the placeholder feature **globally** for publishers. However, remember that in this case we can no longer bring placeholders to your entire page via our adlib.

If you create the placeholder on your own and wonder about the necessary height of the placeholder, you can simply take a look at the adSSetup object. There you will find the ordered sizes for the respective ads. Take the largest size to build a CLS compliant placeholder.



## What happens when you disable placeholders on your page?

1. Google may punish your site by leading fewer SEO traffic to you when they discover layout shifts
2. No stick to slot effects for bigger placeholders in the viewport
3. No dynamic handling for the size of ready placeholders outside the viewport
4. No dynamic handling for special formats


**What does this mean?** 

*When we have an ad response from the adserver for a specific adslot which is still outside of the viewport, we change it's height to match the delivered ad so there is no unnecessary whitespace*.

*The same goes for some special formats like the Underscroller, we check if the booked size is smaller than the standard ad size and trim the unnecessary whitespace as well*.




## Further resources

- **https://web.dev/cls/**: An article by google, explaining what the cls is about
- **https://web.dev/vitals/**: A guide to identify problems concerning user experience
- **[Pagespeed Insights](https://developers.google.com/speed/pagespeed/insights/)**: A tool to get important metrics and tips how to fix problems on your page
- **[Lighthouse](https://developers.google.com/web/tools/lighthouse/)**: Another automated tool to run audits about performance, seo, ux, ...



## Help

If you have some question don't hesitate to contact us:

__Ad Technology Team__
  adtechnology@axelspringer.de


