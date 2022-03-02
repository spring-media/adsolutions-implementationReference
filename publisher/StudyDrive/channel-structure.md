
# :warning: Work in Progress :warning:
This document is still work in progress and not meant to be used yet! 


--------


# Channel Overview

> This document shows you the varying settings for your adSSetup object for each page type, as discussed in our second workshop "Pagename Structure and Keyword Targeting".


You can have a look into [this document](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/pagename-structure.md), to get a basic understanding on how pagenames & keyword targetings work.


| Pagename          |
|-------------------|
| newsfeed          |
| groups            |
| course            |
| documents_index   |
| documents_page    |
| flashcards_index  |
| flashcards_page   |
| company_profile   |
| user_profile      |
| user_profile_edit |
| notifications     |

<br>

# Placements Overview

> This is an overview of our recommended placements and their associated sizes.

<br>

## Desktop Placements

| Placements<br>_(adSSetup.adPlacements)_ | Sizes<br>_(adSSetup.adSlotSizes)_ |
|---------------|-----------------------|
| billboard     | `[970,250],[800,250]` |
| billboard_btf<br>_Optional: for longer pages_ | `[970,250],[800,250]` |
| course_ad<br>_On course pages_ | `[427,23]` |
| feed_ad <br>_Native Feed Ad_  | `[427,23]` |
| feed_ad_btf, feed_ad_btf_2.   | `[427,23]` |
| sky           | `[160,600],[120,600],[300,600]` |
| mrec          | `[300,250],[300,600]`           |
| mrec_btf      | `[300,250]`           |


<br>

## Mobile Web 

| Placements<br>_(adSSetup.adPlacements)_ | Sizes<br>_(adSSetup.adSlotSizes)_ |
|---------------|------------------------------|
| banner        | `[320,50],[300,75],[320,75],[320,80],[320,100],[320,150],[320,160]` |
| mrec          | `[300,250],[300,300]`                  |
| mrec_btf      | `[300,250],[300,300]`                  |
| course_ad<br>_On course pages_ | `[427,23]` |
| feed_ad <br>_Native Feed Ad_  | `[427,23]`   |
| feed_ad_btf, feed_ad_btf_2, feed_ad_btf_3  | `[427,23]` |


<br>

## Android & iOS Apps

| Placements<br>_(adSSetup.adPlacements)_ | Sizes<br>_(adSSetup.adSlotSizes)_ |
|------------|-------|
| banner     | `[320,50],[300,75],[320,75],[320,80],[320,100],[320,150],[320,160]` |
| mrec       | `[300,250],[250,250],[300,300]` |
| mrec_btf   | `[300,250],[250,250],[300,300]` |


