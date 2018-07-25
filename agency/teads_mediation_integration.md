## Appnexus TEADS Mediation

To make TEADS Outstream work within the mediation mechanism we have to do some manual things, because TEADS has to leave the frame of the mediation.
Because of that we have to catch up the callback from TEADS and propagate this information to the mediation frame to invoke the passback when necessary.
To do so we need to know the slot the ad has been delivered through, so we defined these global variables:

Property | Type | example | used for
--- | --- | --- | ---
_tt_position | *STRING* | 'mrec' | ID of the adslot
_tt_selector | *STRING* | '#cb-inread-content' | CSS selector to place player into
_tt_minimum | *NUMBER* | 1 | number of element in returned array from css selecotr (human readable, starting by 1 not 0, will automatically be reduced by 1 by the library script)

First we have to use this code to deliver the TEADS Tag to the webpage:

```
var p = window.top.ASCDP.pageSet, ContId = window.parent.document.body.id;

/* define properties for delivery, we will consultate pageSet for dynamically set these properties */
window.top._tt_position = ContId;
if (((p.view === "d" && p.outstreamId !== "inpage") || (p.view === "m" && p.outstreamIdMobile !== "inpage")) &&
        window.top.document.getElementById(ContId)) {
    window.top._tt_selector = "#" + ContId;
    window.top._tt_minimum = 1;
} else {
    window.top._tt_selector = p.teadsSlot();
    window.top._tt_minimum = p.teadsMinSlot;
}

/* create Teads-Tag */
var tscr = document.createElement('script');
tscr.setAttribute('class', 'teads');
tscr.setAttribute('async', 'true');
tscr.setAttribute('src', 'https://a.teads.tv/page/9597/tag');   // containing TEADS PageId (9597), by pageSet => 'https://a.teads.tv/page/' + teadsslots[p.view][p.siteDomain].pageId + '/tag'
tscr.setAttribute('data-serve', 22536);                         // TEADS PlacementId (22536), by pagSet =>  teadsslots[p.view][p.siteDomain].placementId)
tscr.setAttribute('data-tracking-Click', '${CLICK_URL}');       // for providing clicktracking to our adserver

/* append Tag to something that fits for you */
window.top.ASCDP.adS.adElts[ContId].Cont.parentNode.appendChild(tscr);
```

This Tag will deliver this script hosted on TEADS CDN that uses the defined properties and a predefined callback

```
(function(w, d, s) {
    try {
        d = w.top.document || d;
        w = w.top.document ? w.top : w;
    } catch (e) {}
    var ttag = function() {
        var _tt_slot = window._tt_selector || "article .txt > p"; // here the property will be imported if defined or uses a fallback selector
        var _tt_min = window._tt_minimum || 4; // here the property will be imported if defined or uses a fallback minimum
        w.teads.page(9597).placement(22536, {
            slider: {
                allow_corner_position: false,
                allow_top_position: false
            },
            "callbacks": {
                "AdSkipped": function() {
                    (function() {
                        /* here our passback has to be included */       
                        if (ASCDP && window._tt_position) {
                            ASCDP.adS.passbackCall(window._tt_position, "teads");
                        }
                    })();
                }
            },
            "format": "inread",
            "slot": {
                "btf": false,
                "selector": _tt_slot,
                "minimum": _tt_min
            }
        }).passback(function passback() {
            (function() {
                /* here our passback has to be included */    
                if (ASCDP && window._tt_position) {
                    ASCDP.adS.passbackCall(window._tt_position, "teads");
                }
            })();
        }).serve();
    };
    if (w.teads && w.teads.page) {
        ttag();
    } else if (!w.teadsscript) {
        s.src = '//cdn.teads.tv/media/format/v3/teads-format.min.js';
        s.async = true;
        s.onload = ttag;
        w.teadsscript = d.getElementsByTagName('head')[0].appendChild(s);
    }
})(window, document, document.createElement('script'));
```

Inside the passbackCall method we have to use to _tt_position to inject the appnexus noad.ja into the mediation frame so AST will trigger the passback.
