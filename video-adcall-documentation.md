# Video Ad Call Documentation

This documentation explains the parameters for Xandr Video Requests.
The video ad call starts with a static url part which is always the same: 
 
`https://ib.adnxs.com/ptv?member=7823`
 
 
## Parameters

| Parameter        | Value           | Note  |
| ------------- |:-------------| :-----|
|    &inv_code=    |    [insert placement name here]      |    *list of placements provided by MI, usually ending in -preroll/-midroll/-postroll*      |
|    &vplaybackmethod=    |     3     |     *fixed value; 3=Click-to-play*     |
|    &kw_vidContentId=    |     [unique video ID]     |     *can be used to target specific content video, or exclude ads for specific video; leave empty if value can't be passed*     |
|    &kw_misc=    |     [additional keywords that can be used for targeting]     |     *leave empty if there are none; note: AdLib interceptor is adding additional values, see below*     |
|    &vwidth=    |    [player width in px]      |          |
|    &vheight=    |    [player height in px]      |          |
|    &kw_vduration=    |     [duration content video in seconds]     |     *leave empty if value can't be passed*     |
|    &referrer=    |     [encoded URL where the ad will be rendered]     |          |


## New GDPR Parameters

| Parameter        | Value           | Note  |
| ------------- |:-------------| :-----|
|    &gdpr=     |         |        |
|    &gdpr_consent=     |         |        |
|    &kw_gdpr_applies=     |         |        |
|    &kw_gdpr_p1=     |         |        |
|    &kw_gdpr_p2=     |         |        |
|    &kw_gdpr_p3=     |         |        |
|    &kw_gdpr_p4=     |         |        |
|    &kw_gdpr_p5=     |         |        |
|    &kw_gdpr_p6=     |         |        |
|    &kw_gdpr_p7=     |         |        |
|    &kw_gdpr_p8=     |         |        |
|    &kw_gdpr_p9=     |         |        |
|    &kw_gdpr_p10=     |         |        |


 
## Example
https://ib.adnxs.com/ptv?member=7823&inv_code=bild.de-desktop-regio_video-preroll&vplaybackmethod=3&kw_vidContentId=70136844&kw_misc=Hannover_regional,Coronavirus,Neuwagen&vwidth=993&vheight=1117&kw_vduration=74&referrer=https%3A%2F%2Fwww.bild.de%2Fvideo%2Fclip%2Fhannover-regional%2Fneuwagen-dicht-an-dicht-keine-fahrzeugauslieferung-wegen-corona-70136844.bild.html
 
 
 
### Additional Parameters for Apps


| Parameter        | Value           | Platform  | Note  |
| ------------- |:-------------| :-----|  :-----|
|   &appid=         |      com.example.helloworld        |   Android    | on Android, this is the app's package name |
|   &appid=         |      123456789        |    iOS   |  On iOS, this is the app's iTunes ID  |
|   &idfa=            |     [the Google advertising identifier]         |   Android    |     |
|   &idfa=            |     [the Apple advertising identifier]         |   iOS    |     |


 
### Additional publisher specific parameters

Some publishers may have some own parameters in relation to publisher specific developments and workflows.
AdTech will consult with publishers if specific parameters are required. Usually the syntax is `"&kw_vid[ParameterName]"`.

#### Examples:

&vidAdBlock=[Schnee Von Morgen Adblock implementation]
&kw_vidWeltLocation=
&kw_vidWeltSmartTvPlattform=


 
### Additional Parameters for server-side integrations

AdTech will consult with publishers if a server-side integration is required.

 
 
| Parameter        | Value             | Note  |
| ------------- |:-------------|:-----|
|      &ip=     |       [IP address of the device making the ad request]         |    Geo targeting will not work without this parameter    |
|      &openudid=     |       [Unique user identifier]         |    Frequency Capping (FC) will not work without this parameter    |
 
 
### Additional Parameters added by AdLib Interceptor for Desktop and MEW:


 
| Parameter        | Value             | Note  |
| ------------- |:-------------|:-----|
|     &size=      |                |           |
|     &publisher=      |                |           |
|     &kw_vidAdaLoadVDC=      |                |           |
|     &kw_amazon_preroll=      |                |           |
|     &kw_amzniid=      |                |           |
|     &kw_1plusX=      |                |           |
|     &kw_premium=      |                |           |
|     &kw_branch=      |                |           |
|     &kw_heidi=      |                |           |
|     &kw_ext_uid_sent=      |                |           |
|     &prebidVideo=      |                |           |
|     &pt5=      |                |           |



 
### Legacy Parameters migration SmartAdServer to Xandr

These legacy parameters are part of the old SmartAdServer integration before the migration to Xandr. 
They are still passed by some publishers.


| Parameter        | Value             | Note  |
| ------------- |:-------------|:-----|
|     &pt0=      |                |           |
|     &pt1=      |                |           |
|     &pt2=      |                |           |
|     &pt3=      |                |           |




## Help

If you have any questions or problem don't hesitate to contact us:

__Ad Technology Team__
  adtechnology@axelspringer.de


