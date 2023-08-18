# iFrame library for advertising in chat widgets

This code is meant to do everything to include ads into a chat conversation. To enable it you need to include the following code into your page:

```
<script type="text/nmtSetup" data-module="chatAds">
{
  appid: '123456789ABCDE',
  adUnitId: '1234',
  propertyId: '5678',
  endpoint: 'https://bing-ads-proxy.melonbits.com/bing-ads/api/v1/ads/chat',
  market: 'de-de', // country and language the chat is running in
  domBaseId: "chatAd", // id of the dom element where the ad should be placed
  products: ['TextAds', 'ProductAds'], // products to be requested
  dynamicSlots: false, // use true for 1 ad per viewport
  answersForSlot: 3 // count of answers before ad when not using dynamicSlots
}
</script>
<script type="text/javascript" src="https://www.asadcdn.com/adlib/extensions/corsFrameChatCalls.js"></script>
```

After the library is loaded and registered, make sure you trigger it once a new chat starts or the user switches between them using:

```
/* conversationId should be the id of the actual chat */
let conversationId = "a5d82531-015a-46d0-9547-47602fe9b03e";
ASCDP.chatAds.startChat(conversationId);
```

## Contact

__Team AdTechnology__
  [adtechnology@axelspringer.com](mailto:adtechnology@axelspringer.com)

