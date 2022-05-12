

# The AdSSetup - in detail

Since the AdSSetup is a very important part of the ad integration on your page, it should be clear, what informations are included and what they mean.



<table>
<thead>
  <tr>
    <th>Attribute</th>
    <th>Explanation</th>
    <th>Sample Value</th>
    <th>Required</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>view</td>
    <td>Decides if the current page is on mobile (m) or desktop (d) viewport</td>
<td>

`"d" | "m"`

</td>
    <td>yes</td>
  </tr>
    
  <tr>
    <td>partners</td>
    <td>Enable programmatic demand</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
    
  <tr>
    <td>adPlacements</td>
<td>

List every ad that you order from the ad server. You can find a visual illustration for the adPlacements [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#ad-placements-overview).

**Important**: Please make sure, that you provide an adSlot for each placement, that you define here.


</td>
<td>

_mobile_
```javascript
[
    "banner",
    "mrec",
    "mrec_btf",
    "mrec_btf_2",
    "mrec_btf_3",
    "inpage"
]
```

_desktop_
```javascript
[
    "superbanner",
    "sky",
    "billboard",
    "mrec",
    "mrec_btf",
    "mrec_btf_2",
    "mrec_btf_3",
    "inpage"
]
```

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>adSlotSizes</td>
    <td>Specify the formats you like to have for each ad that you ordered in the 

`adSSetup.adPlacements`


 <br>

Read more about sizes [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#creative-sizes-reference).

</td>
<td>

```javascript

adSlotSizes: {

    "billboard": [{
        "minWidth": 799,
        "sizes": [[800, 250]]
    }, {
        "minWidth": 969,
        "sizes": [[970, 250], [800, 250]]
    }],

    "mrec": [{
        "minWidth": 1,
        "sizes": [[300, 250], [300, 600]]
    }],

    "mrec_btf": [{
        "minWidth": 1,
        "sizes": [[300, 250], [300, 600]]
    }]
}

```

</td>
    <td>yes</td>
  </tr>
  

  <tr>
    <td>gaiaSetup</td>
<td>

Overwrites adlib gaia defaults. Every property defined here will overwride the matching property defaulted by the adlib. (optional)

</td>
  
<td>

```javascript
gaiaSetup: {
  "startCount": 10,
  "fitSizeToSlot": true,
  "sizes": {
      "m": [[300, 50], [320, 50], [300, 75], [320, 75], [300, 80], [320, 80], [300, 150], [320, 150]],
      "d": [[970, 250], [800, 250], [300, 250]]
   },         
  "matchTagsBefore": [
    "</h2>"
  ],
  "matchTagsAfter": [
    "</div>",
    "</p>"
  ],
  "ads": [
    "teaser",
    "regteaser",
    "liveticker-ad"
  ],
  "resetBy": [
    "sas_.*",
    "ANZEIGE"
  ],
  "except": [
    "<h3>Lesen Sie auch</h3>",
    "video",
    "<img",
    "embed",
    "iframe"
  ],
  "article": [
    "main[role='main']",
    ".hs-liveticker"
  ],
  "textWrapper": [
    "article",
    ".module-liveticker"
  ],
  "wrapperCSS": "margin: 0 0 20px 0;",
  "markerCSS": ".gaiaWrapper:after {
      content: 'Anzeige'; font-size: .75rem; display: block; text-align: center; 
      text-transform: uppercase; color: #999; line-height: 2rem;
   }",
  "wrapperCSSmew": "margin: 0 0 15px 0;",
  "markerCSSmew": ".gaiaWrapper:before {
      display: block; content: 'Anzeige'; letter-spacing: normal; 
      font-family: ffmark,Helvetica Neue,Helvetica,Arial,sans-serif; 
      font-style: normal; font-weight: 200; font-size: 12px; 
      line-height: 16px; display: block; color: #787878; text-align: right;
   }"
}
```
</td>
    <td>yes</td>
  </tr>
  
  
  
  <tr>
    <td>placeholders</td>
<td>

Our answer on Google's CLS. Learn more about that topic and the setup possibilities for the placeholder object [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md).

</td>
<td>

```javascript
placeholder: {
    disablePlaceholders: false,
    default: {	
        "border-color": "#EEEDE8",
        "background-color": "#F9F9F7",
        "admarkPosition": "bottom right",
        "color": "#BCBCBC",
        "font-size": "12px",
        "font-family": "Tahoma"
    },
    mrec: { 
        "background-color": "#FCBFFF"
    }
}
```

</td>
    <td>yes</td>
  </tr>
    
  <tr>
    <td>colorBg</td>
    <td>Allow or deny a change of the background color of your page by the ads</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
    
  <tr>
    <td>bgClick</td>
    <td>Allow or deny the clickability of the background of the page controled by the ads</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>hasVideoPlayer</td>
    <td>enable or disable partnerscripts like headerbiding for video</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>isArticle</td>
    <td>it shows us if the page is an article</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>pagename</td>
    <td>channel / article name from CMS - there has to be an existing pendant as 'Placement Group' in the ad server.</td>
<td>

`news_index` for channel pages and
`news_story` for article pages

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>target</td>
    <td>a list of key/values which are used for targeting</td>
<td>

`"value1;value2;key1=value1,value2;key2=value1,value2;"`

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>iabTax</td>
    <td>explanation</td>
    <td>sample</td>
    <td>no</td>
  </tr>
</tbody>
</table>

