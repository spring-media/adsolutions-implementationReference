
## Pagenames

**What are Pagenames?**

> With every impression on your page, you use a combination of pagename and keywords, to explain to the adserver, where the impression is generated. 
> For each existing pagename, there has to be an existing pendant as `placement group` in the adserver. This placement groups are like containers which include the `placements`.
> 
> The placements are the pendants to the ad slots you create in your page layout to deliver ads in. 



## Keyword Targeting

**What is Keyword Targeting?**

> You can use keywords as targeting when booking a campaign in xandr, so that this campaign is only served on pages, where this specific keyword is defined.
> This can be used to further specify pages, for example when your newspage has the channel "sport" and child channels for all different kind of sports - these could be defined via keywords on the page, while using the same pagename for all of them.

**Reporting**<br>
_Keep in mind, that this keywords need to exist in the adserver if you like to report the impressions from this child channels._



## Example: What happens in an impression?

Imagine you are visiting the website 'example-newspage.com' with your phone and you as a user are clicking into an article.
While the article is loading, the adlib collects the information from the adSSetup:


```javascript
adSSetup: {
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
   ...
   target: "economics",
   view: "m"
}
```

With this information, the adlib knows, that the publisher is `example-newspage.com`. 
Since you are visiting the page with your phone, we know that the platform is mobile `mew` and the pagename as defined in the adSSetup is `news_story`.
So now we know that we have to ask the adserver for the placement group `example-newspage.com-mew-news_story`.<br>

In the next step, the adlib looks into the adSSetup and checks what placements are ordered in `adSSetup.adPlacements`. These placements must exist in the placement group.
Since there are two placements `banner`and `mrec`, we are now looking into `adSSetup.adSlotSizes`, to see which formats are allowed for these two placements.

With these informations are we now creating the ad call.<br>


**Granularity with targtings**<br>
> To prevent the need to create many placements and placement-groups in the adserver, every time a website gets a new channel, we can use the combination with keywords.

In the above example we have a `target` with the value "economics". This allows us on the one hand to report impressions for the complete placement group  `example-newspage.com-mew-news_story`,
but on the other hand we can use this target to specify our report to filter the impressions for the keyword "economics".<br>

Therefore we can use different keywords to create a very broad spectre for different channel types to report on, while using a very basic set of placement groups in the adserver itself. 


