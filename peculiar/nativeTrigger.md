# custom feature: nativeResponse - size 427x23
This is an option to let a publisher or third party decide to render content based on the information of an adserver 
(in this case a SPRING administrated Xandr seat) or also just count and get clickTags.

Therefore the publisher will setup a dedicaed adslot like all the others but just include the size 427x23.
The size 427x23 is vanity for "hasAd".

When the adserver has finished loading the adlib will analyse the response and tell the publishers page 
additional information he can use for rendering on his side as e.g. there will be advertiserIds or the name of the Xandr lineitem.

For regular toplevel integration this is done the same as described here:
[LoadHandler Reference](../publisher-loadHandler-reference.md)

### Some of the information transmitted and useable in coordination to the marketer would be:

Property | Type 
--- | --- 
adSlot.detail.advertiserId | *string*
adSlot.detail.campaignId | *string*
adSlot.detail.lineItemId | *string*
adSlot.detail.lineItemCode | *string*
adSlot.detail.insertionId | *string*
adSlot.detail.clickThrough | *string*

The main difference to a normal ad is that the booked creative will not render anything,
but it will be counted as an impression in the adserver and provides a pixel for click counting. 

The admanagement still has the possibility to book campaigns for their adverstisers
while the publisher/party may map the ids or other selectors to his renderer.

### A suitable situation would be:

The marketer books a campaign for advertiserA (1234) und advertiserB (5678).
When the adcall is done and advertiserA gets delivered the adserver counts an impression for him.
Also the integration sends the data as described, the rendering can happen.

Because the marketers bookings have the same conditions the adserver also delivers 50/50 of both advertisers.
If you change condition by adding key/value targeting, duration or else you may alter that.
Using target may be useful for pages like "special" using the same group or separating sport events like:
                                
DFB-Pokal
Champions League
Europa League
Nationalmannschafts-Spiele


### <Code\>
The following code will show an adaptable loadHandler implementation using an example adslot "inpage_2":

```
<script>
    window.addEventListener("adInfo", function(adSlot) {
        if (adSlot.detail.id === "inpage_2" && adSlot.detail.hasAd) {
            // check with partner has been delivered
            if (adSlot.detail.lineItemCode.indexOf("advertiser A") > -1) {
                // recognised "advertiserA" 
                publisherframework.renderPartner("advertiserA");
            }
        } else {
            // do nothing
        }
    }, false);
</script>
```

If you do not provide an adslot directly within the regular adSSetup integration,
this shows a way to do an onDemand adRequest:

```
<script>
    var hasAdDiv = document.createElement('div');
    hasAdDiv.id = "inpage_2"
    document.body.appendChild(hasAdDiv);
    adSSetup.adSlotSizes.inpage_2 = [{minWidth:1, sizes: [[427,23]]}];
    ASCDP.adS.renderAd('inpage_2');
</script>
```

Without an integration of the adlib and while using singleTag adcalls (ttj) 
we will not have the option to provide information by triggering an event.
The adcall itself has to be done in a separate iframe und ensure any kind of document.write
stays there and does not harm the page/widget.

The following code shows a rudimental example to work with that environment as well.

```<script>
var renderPartner = function(event){
    if (window.hasAd) {
        window.parent.publisherframework.renderPartner();
    }
};

document.write("<script src='https://ib.adnxs.com/ttj?member=7823&inv_code=welt.de-desktop-sonstiges_story-inpage&size=427x23'></script>");
document.write("<script>renderBetPartner();</script>");
</script>
```

If this doesn't offer all the stuff needed for your integration or have some other hints or questions
don't hesitate to contact us:


__Carlos Bracho__
 
  Head of Ad Technology
  SPRING
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de
  