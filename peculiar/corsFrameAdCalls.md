# pageSet propagation service

This script is meant to be integrated in third party iframes to get pageInfo like pageName, target, view and so on given by the parent frame.
It is written threeway integrational so it can be used for popups, friendly iframes (fif) and cross-origin frames.

It will generate an object "pageInfo" holding the ASCDP.pageSet and 
one holding a mob-call url for display and a ptv-call url for video named "adcallURIs"  

```
var pageInfo, adcallURIs, fif = !1, w = window;
var displaySizes = [[300,250],[320,50]];
var slot = "mrec";
var vwidth = "";
var vheight = "";

try {
    window.top.document.domain;
    w = window.top;
    fif = !0;
} catch(e) {}

var urlParams = function() {
    var p, params = {};
    if (location.search) {
        location.search.substr(1).split('&').forEach(function (e) {
            p = e.split('=');
            params[p[0]] = decodeURIComponent(p[1]);
        });
    }
    return params;
}();

var parsePageInfo = function(msg) {
    pageInfo = msg.data.data;
    adcallURIs = getAdCallURIs();
    renderAdFrame(adcallURIs.display);
};

var getAdCallURIs = function() {
    var targetString = "";
    for (var targetKey in pageInfo.target) {
        if (pageInfo.target.hasOwnProperty(targetKey)) {
            targetString += "kw_" + targetKey + "=" + pageInfo.target[targetKey] + "&";
        }
    }
    var adcallSrcDisplay = "https://ib.adnxs.com/mob?member=7823&inv_code=bild.de-" + (pageInfo.view === "d" ? "desktop" : "mew") + "-spiele.partner1_story-" + slot +
        "&kw_contId=" + slot +
        "&size=" + displaySizes[0].join('x') +
        "&promo_sizes=" + displaySizes.join('%').replace(/,/g, 'x').replace(/%/g,',') +
        "&promo_alignment=[center]&psa=0" +
        "&cb=" + Math.round(Math.random() * 10000000000000) +
        "&kw_btf=false&" + targetString;

    var adcallSrcVideo = "https://ib.adnxs.com/ptv?member=7823&inv_code=bild.de-" + (pageInfo.view === "d" ? "desktop" : "mew") + "-spiele.partner1_video-preroll" +
        "&vplaybackmethod=3" +
        "&vwidth=" + vwidth +
        "&vheight=" + vheight +
        "&cb=" + Math.round(Math.random() * 10000000000000) +
        "&referrer=" + encodeURIComponent(w.location.href) +
        "&" + targetString;

    return {
        display: adcallSrcDisplay,
        video: adcallSrcVideo
    };
};

var renderAdFrame = function(url){
    var adFrame = document.createElement('iframe');
    adFrame.src = 'about:blank';
    adFrame.id = "div_utif_" + slot;
    adFrame.scrolling = 'no';
    adFrame.frameBorder = 0;
    adFrame.width = 320;
    adFrame.height = 250;
    adFrame.style.display = "block";
    document.querySelector('#' + slot).appendChild(adFrame);
    var frameHTML = '<!doctype html><html><head><title></title></head><body style="margin:0;padding:0">'+
        '<script type="text/javascript" src="' + url + '"><\/script></body></html>';
    if (navigator.userAgent.indexOf('MSIE') === -1 && navigator.userAgent.indexOf('Opera') === -1) {
        adFrame.contentDocument.write(frameHTML);
        adFrame.contentDocument.close();
    } else {
        if (document.domain !== location.hostname) {
            adFrame.src = 'javascript:var d=document.open();d.domain="'+document.domain+'";void(0);';
        }
        adFrame.contentWindow.contents = frameHTML;
        adFrame.src = "javascript:window['contents']";
    }
};

if (urlParams.pageName) {
    pageInfo = {
        pageName: urlParams.pageName || 'sonstiges_story',
        target: urlParams.target ? JSON.parse(urlParams.target) : {},
        view: urlParams.view || "d"
    };
    adcallURIs = getAdCallURIs();
    renderAdFrame(adcallURIs.display);
} else if (!fif) {
    (window.addEventListener) ? document.addEventListener("message", function(msg){parsePageInfo(msg);}, false) : document.attachEvent("onmessage", function(msg){parsePageInfo(msg);});
    window.top.postMessage('sendPageSet:;:canvas-game','*');
} else {
    pageInfo = window.top.ASCDP.pageSet;
    adcallURIs = getAdCallURIs();
    renderAdFrame(adcallURIs.display);
}
```

Here's a table of what the script is providing:

declarations | type | used for | comment
--- | --- | --- |--- 
w | *DOM element* | reference to the topmost window object | 
fif | *boolean* | fif will be false for cross-origin frames | 
displaySizes | *array* | contains arrays of allowed adformat sizes eg. [728,90], [300,250], [320,50]
slot | *string* | the adSlot container id e.g. `superbanner`, `billboard_btf` ... | you will put this container where the display ad shall be rendered
vwidth | *string* | width of the videoplayer | may be empty, also regarding responsvice players
vheight | *string* | height of the videoplayer | may be empty, also regarding responsvice players
pageInfo | *object* | reference to ASCDP.pageSet information from parent | 
urlParams | *string* | will hold all url query params | 
adcallURIs | *object* | yes | {display: *adcallSrcDisplay*,video: *adcallSrcVideo*}
parsePageInfo | *function* | will be registered and used in cross-origin frames |
getAdCallURIs | *function* | produces the urls that are safed in object adcallURIs | 
renderAdFrame | *function* | generates an iframe, appends it to the div#*slot* and renders the display ad inside | you may changed this whole process, it just demonstrates how it works

## Usage

You may use the given urls in other ways or even have to, if you need assistance please feel free to contact us 

__Team AdTechnology__
  [adtechnology@axelspringer.de](mailto:adtechnology@axelspringer.de)

