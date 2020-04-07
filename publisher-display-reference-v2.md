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

