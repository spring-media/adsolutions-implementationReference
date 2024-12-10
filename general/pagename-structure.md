# About the pagename structure in Xandr

The goal of this document is to help you come up with a pagename structure for your website and to give you an overview of what to keep in mind. <br>

There are different approaches - some publishers might only have 10 different pagenames, while others might have a thousand. Both cases can totally make sense based on the needs that these publishers have.

<br>

## Table of Contents

1. [General](#general)
   - [Pagenames](#pagenames)
   - [Placements](#placements)
   - [Placement Groups](#placement-groups)
   - [Platforms](#platforms)
2. [Creating placements for a Xandr migration](#creating-placements-for-a-xandr-migration)
   - [Example: Create placements in Xandr](#example-create-placements-in-xandr)
3. [Use key values to reduce number of placement groups](#use-key-values-to-reduce-number-of-placement-groups)
4. [Make inventory bundles with multiple placement groups (content categories)](#make-inventory-bundles-with-multiple-placement-groups-content-categories)
   - [Content Categories](#content-categories)
   - [Example: Using a content category to bundle placement groups](#example-using-a-content-category-to-bundle-placement-groups)
5. [Example: What happens in an impression?](#example-what-happens-in-an-impression)



<br>

## General

<br>

### Pagenames

The pagename is a parameter that you define in the adSSetup object on your page.<br>
It describes from which part of your website the ad request is made. When making an ad request, the pagename and platform info will decide which specific placement is called in Xandr.

<br><br>

### Placements

When making ad requests from your page, part of the ad request will be the placement. The placement refers to one specific ad slot you have on your page.
For every ad slot on your page, you have to have a placement object in Xandr which will have certain settings and configurations.
Also you will be able to report all kinds of performances on the placement itself.

<br>

Our suggested syntax looks like this:

{`publisher`}-{`platform`}-{`pagename`}-{`adslot`}<br>

<br><br>

### Placement Groups

Every placement is part of a placement group.<br>
A placement group is basically the scope of a page or a page type. From the perspective of the ad server, it is basically a container that holds all placements (ad slots) that are available for this particular page. 

<br>

Our suggested syntax looks like this:

{`publisher`}-{`platform`}-{`pagename`}<br>

<br><br>


### Platforms

When we talk about platforms in the context of creating placements, we mean the environment.<br>
The two default platforms are:
 - desktop (computer screens)
 - mew (mobile web screens, no native apps)
    - _mew stands for "mobile enhanced web" and is the established term in the industry for the mobile web environment_
    - _Since usually, there is no web environment in native apps and those ad requests are made a bit different, these are excluded from the mew platform._

<br>

Depending on the publisher, there can be some additional platforms for native apps (iOS, Android, Phone & Tablet)


<br>
<br>

----------

<br>
<br>

## Creating placements for a Xandr migration

We can create all placement group and placement objects in Xandr for you. We just need a list of pagenames and platforms, with a set of default placements per platform. 

<br><br>

### Example: Create placements in Xandr

Lets make an example with the following input:

<br>

**Platform**: desktop<br>
**AdSlots**: mrec, sky, superbanner, billboard

<br>

**Platform**: mew<br>
**AdSlots**: banner, mrec

<br>

**Pagenames**:
 - news_index
 - news_story
 - business_index
 - business_story

<br>

> [!NOTE]  
> _If you are not sure about the slots per platform, we have a default set that we usually create for new publishers._<br>
> _All created objects are optional to use - that means, that just because some placements exist in the ad server, doesn't mean that you have to request them._

<br>
<br>

From this list, we will create the following objects in Xandr:

<br>
<br>



| Placement Group                    | Placements                                                                                                   |
|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| publisher.com-desktop-news_index   | publisher.com-desktop-news_index-mrec<br>publisher.com-desktop-news_index-sky<br>publisher.com-desktop-news_index-superbanner<br>publisher.com-desktop-news_index-billboard |
| publisher.com-desktop-news_story   | publisher.com-desktop-news_story-mrec<br>publisher.com-desktop-news_story-sky<br>publisher.com-desktop-news_story-superbanner<br>publisher.com-desktop-news_story-billboard |
| publisher.com-desktop-business_index | publisher.com-desktop-business_index-mrec<br>publisher.com-desktop-business_index-sky<br>publisher.com-desktop-business_index-superbanner<br>publisher.com-desktop-business_index-billboard |
| publisher.com-desktop-business_story | publisher.com-desktop-business_story-mrec<br>publisher.com-desktop-business_story-sky<br>publisher.com-desktop-business_story-superbanner<br>publisher.com-desktop-business_story-billboard |
| publisher.com-mew-news_index       | publisher.com-mew-news_index-banner<br>publisher.com-mew-news_index-mrec                                        |
| publisher.com-mew-news_story       | publisher.com-mew-news_story-banner<br>publisher.com-mew-news_story-mrec                                        |
| publisher.com-mew-business_index   | publisher.com-mew-business_index-banner<br>publisher.com-mew-business_index-mrec                                |
| publisher.com-mew-business_story   | publisher.com-mew-business_story-banner<br>publisher.com-mew-business_story-mrec                                |

<br>
<br>

----------

<br>
<br>

## Use key values to reduce number of placement groups

If your website structure has potentially a lot of placement groups, which all are of the same type, you might want to think about using keyvalue targets instead of declaring every single object.

So for example, if you have the pagenames:

 - product_keyboards
 - product_screens
 - product_computers
 - product_smartphones
 - product_tv

<br>

You might also just use the pagename "product" and define the type as key value target instead.
Your adSSetup object for this case would look like this:

```javascript
adSSetup = {
  ...
  view: "d",
  pagename: "product",
  target: "producttype=smartphones;"
  ...
}
```

<br>

In the next step, we create the key `producttype` in Xandr. For each different type, we can now create a value in our new key. <br>
The values have two attributes:
 - **value**: _The actual value which will match with the one you write into `adSSetup.target`._
- **label**: _A readable label for the value. This is useful if your values are unreadable ids. Labels can be included in reports._

<br>

This way, if you want to run a campaign specifically on this page, you can just target the placement group `publisher.com-desktop-product` and set an additional keyvalue target to `producttype=smartphones` in Xandr.<br>

Therefore we can use different keywords to create a very broad spectre for different pages to target and report on, while using a very basic set of placement groups in the adserver itself. 

<br>

> [!IMPORTANT]
> One shortcoming of this solution is, that you can not bundle multiple key values as an inventory (content category).
> This is especially relevant if you regularily want to target many key values in your campaigns.

<br>
<br>

----------

<br>
<br>

## Make inventory bundles with multiple placement groups (content categories)

<br>

### Content Categories

A content category is a bundle of placement groups in Xandr. One placement group can be part of multiple content categories.
These content categories can be used as target for a campaign, so that you can just set the target to a content category "products"

<br>
<br><br>

### Example: Using a content category to bundle placement groups

Let us continue with the previous example. Our pagenames are the following:
 - product_keyboards
 - product_screens
 - product_computers
 - product_smartphones
 - product_tv

<br>

If you have all pagenames created as placement groups in Xandr, you can bundle them to content categories.
<br>

For example you could create a new content category with the name "Computer & Accessory". Next you include the placement groups related to the pagenames `product_keyboards`, `product_screens` & `product_computers`.

Now when you want to target these pages, you do not have to search for every single placement group anymore, but instead just apply the new "Computer & Accessory" content category as inventory target in your campaign.

You can also create reports in Xandr for the content category and monitor its performance.<br>
Basically, content categories make handling a lot of placement groups a lot easier.


<br>
<br>

----------

<br>
<br>


## Example: What happens in an impression?

Imagine you are visiting the website 'publisher.com' with your phone and you click on a news article about some economic topic.
While the article is loading, the adlib collects the information from the adSSetup:

<br>

```javascript
adSSetup: {
   view: "m",
   adPlacements: ["banner", "mrec"],
   adSlotSizes: {
        "banner": [{
             "minWidth": 1,
             "sizes": [[320, 50], [320, 75], [320, 80]]
        }],
        "mrec": [{
             "minWidth": 1,
             "sizes": [[300, 250]]
        }],
   },
   pagename: "news_story",
   target: "topic=economics;"
   ...
}
```

<br>

Since you are visiting the page with your phone, we know that the platform is `mew` and the pagename is `news_story`.<br>
So now we know that we have to ask the adserver for the placement group `publisher.com-mew-news_story`.<br>

In the next step, the adlib looks into the adSSetup and checks what placements are ordered in `adSSetup.adPlacements`. These placements must exist in the placement group in Xandr.<br>

Because there are two placements `banner` and `mrec`, we are now looking into `adSSetup.adSlotSizes`, to see which formats are allowed for these two placements.

With these informations are we now creating the ad request and sending it to Xandr.<br>
Xandr will now find a campaign with a matching targeting, based on the keyword, the placement, or the content categories where this placement group is part of.

<br>
