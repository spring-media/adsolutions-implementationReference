# Standard Xandr InApp Ad Integration

:grey_exclamation: **Hint**
> Before you start the integration...<br>
> Since the Ad Integration for Apps is a lot more complex as for web pages, it might be a good idea to evaluate whether the potential advertising revenue justifies the high effort.<br>
> For example: With 10.000 impressions per month, the ad integration is probably not worth the time invested.

<br>

**Table of contents**

 - [General](#general)

<br>

# General

**Intro**

> The InApp Ad Integration is very modular - depending on which features you wish to include.<br>
> This document will discuss the standard xandr integration with the minimal setup requirements.

Most of the ad integration has to be done by the app developer, since we can't provide an environment in apps, where the setup can be easily configured.



Like on webpages, you need to provide Ad Slots (placements), where the requested ads can be rendered in.<br>
But other than on webpages, you have to handle ad requests and rendering on your own.

<br>


# Steps to your InApp Xandr Integration

## Video Advertising

You can skip this module, unless you have video content in your app, where you would like to show `preroll-`, `midroll-` or `postroll ads`.


<br>

### Requirements: VAST

You need a video player that is able to process VAST urls.

> VAST stands for "Digital Video Ad Serving Template".<br>
> You can read more about this standard on the [IAB Techlab](https://iabtechlab.com/standards/vast/).

This is what a VAST url looks like:

`https://ib.adnxs.com/ptv?member=7823&size=1x1&publisher=[publisherId]&inv_code=[placementName]&vplaybackmethod=3&vwidth=[playerwidth]&vheight=[playerheight] &appid=[appid]&gdpr=[gdpr_applies]&gdpr_consent=[gdpr consent string from CMP]`


<br>

**Overview of VAST parameters**

| Parameter                      | Description                                                                                                         | Required |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------|----------|
| [placementName]                | The name for the current ad slot, the ad is rendered in                                                             | yes      |
| [appid]                        |                                                                                                                     | yes      |
| [publisherId]                  | The ID of your publisher in the Xandr Ad Server. <br>If you don't know this id, you can ask Ad Technology for help. | yes      |
| [gdpr_applies]                 |                                                                                                                     | yes      |
| [gdpr consent string from CMP] |                                                                                                                     | yes      |
| Custom Keywords                | Customkeywords can be attached as &kw_keywordname=value                                                             | no       |




