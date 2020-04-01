# **Framen.io Spring AdLib Integration**

**Version 1.0**

With this you can see how to integrate DOOH Devices with the Spring AdLib. 

## Header Integration

Please implement the following script in the header of your page application


### **Placement Configuration (adSSetup)**

```html
    <script>
        adSSetup = {
            "view": "dooh",
            "partners": true,
            "adPlacements": ["fullscreen", "slotted"],
            "adSlotSizes": {
                "fullscreen": [{
                    "minWidth": 1,
                    "sizes": [[16, 9]] // this will be used for diagonally screens, switch to [9, 16] for upright
                }],
                "slotted": [{
                    "minWidth": 1,
                    "sizes": [[300, 250], [300, 300], [250, 250], [320, 160], [300, 150], [320, 50], [320, 75], [320, 80], [320, 100], [300, 100], [300, 50], [300, 75]]
                }]
            },
            "pageName": "coworking",
            "target": `country=germany;
                       city=berlin;
                       company=wework;
                       title=Display WeWork SonyCenter;
                       address=Kemperplatz 1 Mitte 10785 Berlin;
                       zipcode=10785;
                       categories=office,coworking;
                       zipCode=10785;
                       price=500;
                       audiencesize=1000;
                       precontentcategorie=food;
                       postcontentcategorie=office;
                       tags=green,fun,collaboration;
                       id=ee4e441e-9669-4937-93bb-be018092316d;
                       lat=52.5114566;
                       long=13.371533116173417;
                       orientation=vertical;
                       height=1080;
                       width=1920;`
        }
    </script>
```

## Description of adSSetup

- View: It is the type of device, in this case it is DOOH "Digital-Out-Of-Home"
- adPlacements: It controls the type of placements in the app. For Framen.io we have two kind of placemens, please use at least one placement type:
    - fullscreen: for fullscreen ads and fullscreen video ads. Please use the Size [16, 9] for diagonal screens and [9, 16] for vertical aligned screens.
    - slotted: For IAB Display Ads, please use IAB Sizes: [[300, 250], [300, 300], [250, 250], [320, 160], [300, 150], [320, 50], [320, 75], [320, 80], [320, 100], [300, 100], [300, 50], [300, 75]]
- pageName: please use the main category, they must be static! Please provide us the exactly main category list.
- target: this is used for the targeting:
    - country
    - city
    - company: name of the enterprise where the device is running
    - title
    - address
    - zipcode
    - price: please in cents e.g. 5 Euro would be 500. 
    - audiencesize: the estimated size of the audience
    - precontentcategorie: the content type before the ad
    - postcontentcategorie: content type after the ad. 
    - tags
    - id: UID od the Device, important for FC
    - lat: latitude 
    - long: longitude
    - orientation: the orientation of the display
    - height
    - width 


### **AdLib**

Please add the following script immediate after the adSSetup

```html
<script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/framen.js"></script>
```

This `js` contains the whole Ad Library. Every website will get its own `js` from Axel Springer.

## Body Integration

### Fullscreen Video Container
Please put the following `div` on the page, where the fullscreen ad will be showed

```html
<div id="fullscreen"></div>
```

### IAB Ad Container
Please put the following `div` on the page, where the  ad will be showed

```html
<div id="slotted"></div>
```


## Help

If you have some question don't hesitate to contact us:


__Ad Technology Team__
  adtechnology@axelspringer.de
  