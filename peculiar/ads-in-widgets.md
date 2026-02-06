# Ads in widgets

This guide is meant to provide you an overview and a script example on how the adlib can be used or triggered in an embeddable element.  
Because widgets are meant to be implemented but also can be used as a separate website, it is necessary to detect if there is an already running adlib on the page.  
The following code example therefore is uses the following flow:

* prepare your variables, targets should reflect meta taxonomy
* detect viewport
* check for existing adlib and where it exists
* if exists in the same window, just use it
* if exists in a different window, get the config but still load and proceed in the iFrame
* if no adlib is found the widget as seen as in standalone mode, adlib will be loaded

Please make sure that there is a working cmp accessible in the window this script gets implemented. 

```html
<script>
    (() => {
        const slots = ["widget", "widget_2"], pageName = "news_story", targets = "",
            framed = globalThis === window.top,
            windowWidth = document.documentElement?.clientWidth || document.body?.clientWidth || window.innerWidth;
        let adlibWindow = null, frame = globalThis, view;

        const loadAdLibrary = () => {
            const adlib = document.createElement("script");
            adlib.src = "https://www.asadcdn.com/adlib/pages/bild.js";
            document.head.appendChild(adlib);
        }

        const setSize = () => {
            window.adSSetup.adSlotSizes.widget = [{
                "minWidth": 1,
                "sizes": [[300, 600], [320, 480], [320, 460], [300, 300], [300, 250]]
            }, {
                "minWidth": 727,
                "sizes": [[728, 90], [970, 250], [800, 250]]
            }];
        }

        if (windowWidth >= 728) {
            view = "d";
        } else {
            view = "m";
        }

        while (frame) {
            try {
                if (frame.frames["__asadlibLocator"]) {
                    adlibWindow = frame;
                    break;
                }
            } catch {
            }
            if (frame === window.top) {
                break;
            }
            frame = frame.parent;
        }

        if (adlibWindow === globalThis) {
            setSize();
            slots.forEach(slot => {
                globalThis.adSSetup.adPlacements.push(slot);
                document.dispatchEvent(new CustomEvent('renderAd', {
                    'detail': slot
                }));
            });
        } else if (adlibWindow && framed) {
            window.addEventListener("message", (msg) => {
                if (msg?.data?.message === "pageSet") {
                    window.adSSetup = msg.data.data;
                    window.adSSetup.adPlacements = slots;
                    setSize();
                    loadAdLibrary();
                }
            }, false);
            window.top.postMessage('sendPageSet:;:' + window.name, '*');
        } else {
            globalThis.adSSetup = {
                view: view,
                partners: true,
                adPlacements: slots,
                adSlotSizes: {},
                placeholder: {},
                bgClick: true,
                hasVideoPlayer: false,
                isArticle: true,
                pageName: pageName,
                target: targets
            }

            setSize();
            loadAdLibrary();
        }
    })();
</script>
```

If this doesn't offer all the stuff needed for your integration or you have some other hints or questions
don't hesitate to contact us:

__Ad Technology Team__  
adtechnology@axelspringer.com
