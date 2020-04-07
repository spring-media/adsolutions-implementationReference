# **Integration - Online Desktop & Mobile Advertisement**

Version: 2.0
Contact: [Ad Technology Team](mailto:adtechnology@axelspringer.de)

# Introduction


This document describes the necessary steps for integrating online advertisements on desktop and mobile websites for Axel Springer. 
The delivery of ads utilizes a "One Call" function, which have to be included in the `<head>` part of the websites. This will receive the booked campaigns and will let them in the background for lately rendering. The Ad Placements are `<div>`'s which have to be placed in the wished position for the ad. All Advertisements can be managed via Appnexus.

__Important__
> Please note that our library must be inserted as early as possible in the `<head>` of the website. The bidding process has to start as soon as possible. **Under no circumstances put our Ad Lib in the `<body>` or in the `<footer>`**. 

> Don't try to implement our Ad Library asynchronously, This affects advertising revenue directly. Our files are hosted by [AKAMAI using ION technology](https://www.akamai.com/us/en/products/performance/web-performance-optimization.jsp). It never stops working and if it doesn't work, the whole internet doesn't work :)

# Overview

In the following you will find an overview of the necessary components which must be implemented to deliver and display the advertising media.

This documentation does not work automatically. You need to contact your Media Impact representative first. Each website will receive special documentation according to what has been agreed.


# Ad Integration
## Example Head Integration:


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

    <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/framen_dooh.js"></script>

```

## Description of adSSetup

### View: 
It is the type of device, in this case it is DOOH "Digital-Out-Of-Home"

__Available Views:__

view | Description
------------ | -------------
d | Content cell 2
m | Content column 2
amp | Content cell 2
doch | Content column 2

### Partners
It controls the Partner connection. It is strongly recommended to leave it as "true". If you think it should be "false" please contact us.

### adPlacements: 
Here are the Placements that have to be integrated into the website. Placement has to be understood as an ad-slot. The information that Placements have to be integrated will be received from your Media Impact representative.

>IMPORTANT! Only the Placements that are going to be shown on the "body" page have to be integrated in the "head". It is strictly prohibited to integrate more placements than are shown.

>Also please ensure you add the elements mainly in order they will appear in the website, 
 because the adserver will fill the first elements of each size with the must valueable campaigns.

#### Common used adPlacements
__For Desktop:__

Placement |
--- |
*superbanner* | 
*sky* | 
*billboard* | 
*mrec* |
*inpage* | 

__For Mobile:__

Placement |
--- | 
*banner* | 
*mrec* | 
*inpage* |

### adSlotSizes
Here the Sizes that are supported by each placement will be defined.

__Example for sky placement__

```
		"sky": [{
			"minWidth": 1,
			"sizes": [[9,9],[160,600],[120,600],[300,600],[500,1000],[1000,1000]]
		}],
```

> IMPORTANT ! Please Implement the Size [9,9] in each placement approved for programmatic

[Here you can find the Size's Cheatsheet](link zu den Sizes und Beispiele)

### pageName: 
Please use the main category, they must be static! Please provide us the exactly main category list.

__We recommend the following schema for pageName:__

    - Home Site --> "home_index"
    - Channel, e.g. sport --> "sport_index"
    - Sub-Channel e.g. soccer --> "sport.soccer_index"
    - Article e.g. soccer article --> "sport.soccer_story"

>Before implementing pageNames, talk to your representative on Media Impact to know how deep is this classification.

### target: Every editorial keyword or custom target
>You can use stand alone keywords with semicolon `;` separately

>Key/values are also supported. `key=value1,value2;`

>Please ensure to end the line with a semicolon

__target: this is used for the targeting:__

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

Please add the following script immediate after the adSSetup.
>Every Publisher will get it's own AdLib for the every platform.

> Don't try to implement our Ad Library asynchronously, This affects advertising revenue directly. Our files are hosted by [AKAMAI using ION technology](https://www.akamai.com/us/en/products/performance/web-performance-optimization.jsp). It never stops working and if it doesn't work, the whole internet doesn't work :)


```html
<script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/framen_dooh.js"></script>
```

This `js` contains the whole Ad Library. Every website will get its own `js` from Axel Springer.