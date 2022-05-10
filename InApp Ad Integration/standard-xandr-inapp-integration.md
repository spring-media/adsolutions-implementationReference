# Standard Xandr InApp Ad Integration

:grey_exclamation: **Before you start the integration...**
> Since the Ad Integration for Apps is a lot more complex as for web pages, it might be a good idea to evaluate whether the potential advertising revenue justifies the high effort.<br>
> For example: With 10.000 impressions per month, the ad integration is probably not worth the time invested.

<br>

**Table of contents**

 - [General](#general)
 - [Steps to your InApp Xandr Integration](#steps-to-your-inapp-xandr-integration)
      - [SDK Integration - iOS](#sdk-integration---ios)
      - [SDK Integration - Android](#sdk-integration---android)
      - [How to display ads](#how-to-display-ads)
          - [Ad Call Parameters](#ad-call-parameters)
          - [further resources - iOS](#further-resources---ios)
          - [further resources - Android](#further-resources---android)
      - [IDFA & AAID](#idfa--aaid)
      - [Optional: Video Advertising](#optional-video-advertising)
          - [Requirements: VAST](#requirements-vast)
          - [Overview of VAST parameters](#overview-of-vast-parameters)


 



<br>

# General

The InApp Ad Integration is very modular - depending on which features you wish to include.<br>
This document will discuss the standard xandr integration with the minimal setup requirements.

Most of the ad integration has to be done by the app developer, since we can't provide an environment in apps, where the setup can be easily configured.



Like on webpages, you need to provide Ad Slots (placements), where the requested ads can be rendered in.<br>
But other than on webpages, you have to handle ad requests and rendering on your own.

<br>


# Steps to your InApp Xandr Integration


## SDK Integration - iOS

Depending on your used package manager, there are different ways to integrate the Xandr SDK.
On [this Xandr documentation page](https://docs.xandr.com/bundle/mobile-sdk/page/ios-sdk-migration-and-integration.html) you can find detailed instructions on how to accomplish the integration.

You can find the github repository of the xandr-ios-sdk [here](https://github.com/appnexus/mobile-sdk-ios).

<br>


## SDK Integration - Android

As well as for iOS there are different ways to integrate the Xandr SDK for Android. 
Xandr provides here [a great documentation page](https://docs.xandr.com/bundle/mobile-sdk/page/android-sdk-integration-instructions.html), too.

You can find the github repository of the xandr-android-sdk [here](https://github.com/appnexus/mobile-sdk-android).

<br>



## How to display ads

For every Placement a "Bannerview" has to be implemented and requested.<br>
Placements on a page are typically `"banner"` on top of the page, an `"mrec"` as next ad in the content and multiple `"mrec_btf"` in the following content.

:grey_exclamation: _Please deactivate autorefresh of the ads_.


<br>

### Ad Call Parameters

There are different parameters for the standard Xandr integration:


| Parameter                | Description                                | Required |
|--------------------------|--------------------------------------------|----------|
| [placementName]<br>(inventoryCode)          | You can use placementNames instead of ids.<br>The syntax is the following:<br><br>"[publisherName]-[platform]-[pagename]-[position]"<br>The [position] then would be either "banner", "mrec" or "mrec_btf".<br><br>An example could look like this: `inventoryCode = bild.de-ios_phone-news_index-mrec` | yes      |
| [sizes]                  | **Banner Sizes**:<br>320x50 (primary size), 300x75, 320x75, 320x80, 320x100, 320x150, 320x160<br><br>**Mrec & Mrec_btf Sizes**:<br>300x250, 250x250, 300x300       | yes      |
| [publisherId]            | The ID of your publisher in the Xandr Ad Server. The publisherId is important for the adServer to deliver fallback ads in case the placement name is unknown.<br><br>If you don't know this id, you can ask Ad Technology for help.                     | yes      |
| [memberId]            | The ID of your Xandr seat. <br><br>If you don't know this id, you can ask Ad Technology for help.                     | yes      |
| [customKeyword "contId"] | The value would be the current position (e.g. "banner", "mrec" or "mrec_btf")<br><br>For the 2nd and nth mrec_btf, please use "mrec_btf_2", "mrec_btf_3", etc.                                       | yes      |
| Custom Keywords          | You can find more infos on how to use custom keywords<br>via the urls below under "Further resources -iOS/Android"      | yes      |


<br>

:grey_exclamation: Quick note about sizes:
> With sizes you can control which ad formats are ordered from the ad server.<br>
> Sizes are often the same as the proportions of the creatives, But this is not a guarantee, since there are exceptions, especially on the web integrations.<br>
> There are some sizes for special formats like Wallpapers and Double Sitebars. However, this is not relevant for the sizes in App - here the sizes are equal to the proportions of the Creatives.


<br>



### Further resources - iOS


Please have a look into the following documents provided by Xandr:


| Document                 | Description                                | 
|--------------------------|--------------------------------------------|
| [show-banners-on-iOS](https://docs.xandr.com/bundle/mobile-sdk/page/show-banners-on-ios.html) | Describes how to request & render ads | 
| [publisher-id-for-iOS](https://docs.xandr.com/bundle/mobile-sdk/page/publisher-id-for-ios.html) | Describes how to handle the publisherId | 
| [single-request-mode-for-iOS](https://docs.xandr.com/bundle/mobile-sdk/page/single-request-mode-for-ios.html) | Describes the use of customKeyword parameter| 


<br>




### Further resources - Android


Please have a look into the following documents provided by Xandr:


| Document                 | Description                                | 
|--------------------------|--------------------------------------------|
| [show-banners-on-android](https://docs.xandr.com/bundle/mobile-sdk/page/show-banners-on-android.html) | Describes how to request & render ads | 
| [publisher-id-for-android](https://docs.xandr.com/bundle/mobile-sdk/page/publisher-id-for-android.html) | Describes how to handle the publisherId | 
| [single-request-mode-for-android](https://docs.xandr.com/bundle/mobile-sdk/page/single-request-mode-for-android.html) | Describes the use of customKeyword parameter| 



<br>

## IDFA & AAID


The IDFA _(= Identifier for Advertisers)_ on iOS & AAID _(= Google Advertising ID)_ on Android are device identifiers, which allow advertisers to track data to deliver customized advertising.

You can get them natively from the operating system (OS) of each device.<br>

:grey_exclamation: But be sure to check the CMP for allowance for the publisher to store and use personal data, before retrieving and passing them.



<br>

## Optional: Video Advertising

You can skip this module, unless you have video content in your app, where you would like to show `preroll-`, `midroll-` or `postroll ads`.


<br>

### Requirements: VAST

You need a video player that is able to process VAST urls.

> VAST stands for "Digital Video Ad Serving Template".<br>
> You can read more about this standard on the [IAB Techlab](https://iabtechlab.com/standards/vast/).

This is what a VAST url looks like:

`https://ib.adnxs.com/ptv?member=7823&size=1x1&publisher=[publisherId]&inv_code=[placementName]&vplaybackmethod=3&vwidth=[playerwidth]&vheight=[playerheight] &appid=[appid]&gdpr=[gdpr_applies]&gdpr_consent=[gdpr consent string from CMP]`


<br>

### Overview of VAST parameters

This is an overview of our standard VAST parameters.

| Parameter                      | Description                                                                                                         | Required |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------|:--------:|
| [placementName]                | The name of the slot in which the ad will be rendered.                                                              | yes      |
| [appid]                        | This string is used to identify a mobile app running on Android or iOS devices.<br><br>**On Android**, this is the app's package name. It's formatted as follows: `com.example.helloworld`.<br>**On iOS**, this is the app's numeric iOS store ID, auto-generated by the App Store. It's formatted as follows: `123456789`.  | yes      |
| [publisherId]                  | The ID of your publisher in the Xandr Ad Server. <br>If you don't know this id, you can ask Ad Technology for help. | yes      |
| [gdpr]                         | The `gdpr` keyword is part of the european privacy law ["GDPR"](https://gdpr.eu/what-is-gdpr/).<br>This keyword always has the value `0` for users outside the EU, while it has the value `1` for users within the EU. | yes      |
| [gdpr consent string from CMP] | You can get the proper value from the CMP object to append it here as parameter.                                    | yes      |
| Custom Keywords                | Customkeywords can be attached as `&kw_keywordname=value`                                                           | no       |


In case you need more than that - there are a lot of additional parameters. Xandr has a very good overview of the possible values on its documentation for [Target Video Attributes via Query String Parameters](https://docs.xandr.com/bundle/monetize_monetize-standard/page/topics/target-video-attributes-via-query-string-parameters.html).






