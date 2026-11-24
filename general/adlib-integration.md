## Introduction

This document describes the necessary steps for integrating online advertisements on desktop and mobile websites for Axel Springer.
This means to:

* setting up a config object fitting the designated url
* register an optional event handler for ad-loads
* load the adlib

### the adConfig object

```typescript
type views = "d" | "m";
type admarkPositions = "top left" | "top center" | "top right" |
    "center left" | "center center" | "center right" |
    "bottom left" | "bottom center" | "bottom right";

declare class AdConfig {
    "adPlacements": string[]; //~ add all placements you will for sure use for the page impression
    "adSenseConfig": any; //~
    "adSlotSizes": AdSlotSizeSettings; //~ define sizes for all slots, can be adjusted later
    "apiBaseUrl"?: string; //~
    "appid"?: string; //~
    "autoStart": boolean; //~ if set to false adlib waits for "startAdvertising" event, so you can e.g. check subscription state before
    "branch"?: string; //~ used for development purpose, use on advice only
    "branchPath"?: string;
    "contentType"?: string; //~
    "gaiaSetup"?: any; //~
    "hasPageAdMi"?: boolean; //~ if set to false adlib will not do adcalls, but process partner integrations
    "hasPageAdTms"?: boolean; //~ if set to false adlib will not do adcalls, but process partner integrations
    "hasVideoPlayer"?: boolean; //~ if set to false adlib will not do adcalls, but process partner integrations
    "iabTax"?: object; //~
    "isArticle"?: boolean; //~
    "pageName": string; //~ represents the section of the page like "news_story", "videoarticle", "homepage", "home_index"...
    "partners"?: boolean; //~
    "paulSetup"?: any; //~
    "partnerIntegrations"?: any; //~
    "pid": string; //~
    "placeholder"?: PlaceholderSettings; //~ configure appearance of placeholder to override default
    "prebidSetup"?: any; //~
    "pub"?: PubAccountConfig; //~
    "siteName": string; //~ normally similar to the domain but without country code, e.g "bild", "welt", "politico_eu"
    "target": string; //~ used to enable more granular targeting, e.g. "sports=soccer;teams=fcb,bvb;"
    "tms"?: TMSConfig; //~
    "view": views; //~ represents the renderingtype of the product. For mobile use "m", for desktop use "d", while desktop is meant to have whitespace around the content wrapper
    "xstreamSetup"?: any; //~
    "zone"?: string; //~
}

interface AdSlotSizeSettings {
    "minWidth": number, //~ always start at least by 1, you may then add additional breakpoints
    "sizes": [[number, number] | 'fluid'] // a definition represents an adformat, adformats may render in sizes different to those requested
}

interface AdSenseConfig {
    "adsense_test_mode": 'on' | '', //~ always start at least by 1, you may then add additional breakpoints
    "page_url": string; // a definition represents an adformat, adformats may render in sizes different to those requested
}

interface TMSConfig {
    "pubPlacements": [], //~
    "siteId": string, //~
    "tea": any //~
}

interface PubAccountConfig {
    "adPlacements": [], //~
    "adSlotSizes": AdSlotSizeSettings; //~ define sizes for all slots, can be adjusted later
    "memberId": string, //~
    "publisherId": string, //~
    "tea": any //~
}

interface PlaceholderConfig {
    "admarkPosition"?: admarkPositions;
    "after"?: string; //~ full cssString to use as ::after pseudo
    "background-color"?: string; //~ css conform expression
    "before"?: string; //~ full cssString to use as ::before pseudo
    "border"?: string; //~ css conform expression
    "border-color"?: string; //~ css conform expression, using 0,0,0,0 will remove border
    "color"?: string; //~ css conform expression
    "custom"?: string; //~ full cssString to use instead adlib configs
    "disable"?: boolean; //~ css conform expression
    "fontFamily"?: string; //~ css conform expression
    "fontSize"?: string; //~ css conform expression
    "markerText"?: string; //~ will be used as value for content property
}

interface PlaceholderSettings {
    "default": PlaceholderConfig;
    "disablePlaceholders": boolean;
    [key: string]: PlaceholderConfig | any; //~ keys matching adPlacements should be used
}
```

### example integration for a widget

```html
<script type="text/javascript">
        const n = "widget", adConfig = {
            siteName: "",
            pageName: "demo_story",
            adPlacements: [],
            adSlotSizes: {},
            target: "widget=kaufberater;"
        };

        adConfig.adPlacements.push(n, n + "_2", n + "_3", n + "_4", n + "_5", n + "_6", n + "_7", n + "_8");
        adConfig.adSlotSizes.widget = [{
            "minWidth": 1,
            "sizes": [[427, 23], "fluid"]
        }];

        window.addEventListener('adInfo', function (event) {
            if (!event.detail.hasAd) {
                // example for reacting on an ad response
                event.detail.adSlot.style.background = "lightred";
            }
        });

        ((t,b,p)=>{({addPlaceholder:function(a){let r=0,o=0,n=p,t=this.getWinWidth(),d={"728x600":["100%",90],"1000x600":["100%",90],"1000x300":[300,300],"993x90":[970,90],"320x480":[300,300],"300x600":[300,600],"640x360":["100%","auto"],"16x9":["100%","auto"],"1x1":[0,0],"2x2":[0,0],"3x3":[0,0],"4x4":[0,0],"5x5":[0,0],"500x1000":[0,0],"1000x1000":[0,0],"290x79":[0,0],"427x23":[0,0]};if(a&&!/sky|betad/.test(a)&&n.adSlotSizes[a]&&!b.getElementById("plhcss_"+a)){n.adSlotSizes[a].forEach(e=>{e.sizes.forEach(e=>{var t,i;"string"==typeof e||(t=e.join("x"),/640x360|16x9|9x16/.test(t))||"1000x300"===t&&"d"===n.view||("100%"===(i=(d[t]||e)[0])?o="100%":Number.parseInt(i)>o&&(o=Number.parseInt(i)),i=(d[t]||e)[1],Number.isNaN(i)?r="100%":Number.parseInt(i)>r&&(r=Number.parseInt(i)))})});var l=n.placeholder.disablePlaceholders||n.placeholder[a]?.disable||!1;if(0<r&&!l){let i="";if(n.placeholder[a]?.custom)i=n.placeholder[a].custom;else if(n.placeholder[a]||n.placeholder.default){var l=(o+"px").replace("%px","%"),s=(r+"px").replace("%px","%"),h=n.placeholder[a]||n.placeholder.default,c=h["border-color"];let e="border: "+(h.border||"solid 1px "+c)+";";if("banner"!==a&&t!==o||(e=`border-top: solid 1px ${c}; border-bottom: solid 1px ${c};`),i=`#${a} {margin:auto;left:0;right:0;min-width:${l};min-height:${s};background: ${h["background-color"]};${e}box-sizing: border-box;position: relative;} #${a} > div {margin-top:-1px;margin-left:-1px;}`,h.after&&(i+=`div#${a}::after `+h.after),h.before)i+=`div#${a}::before `+h.before;else if(-1===h.admarkPosition?.indexOf("hidden")){c=h.admarkPosition.split(" ");let e=(c[0]||"bottom")+": 1px;",t=(c[1]||"right")+": 5px;";"center"===c[0]&&(e="top:0;bottom:0;"),"center"===c[1]&&(t="left:0;right:0;text-align: center;"),i+=`#${a}::before {content: "${h.markerText||"ANZEIGE"}";margin: auto;position: absolute;${e+t}color: ${h.color};font-size: ${h["font-size"]};height: ${h["font-size"]};line-height: ${h["font-size"]};font-family: ${h["font-family"]};}`}}i&&((l=b.createElement("style")).id="plhcss_"+a,l.innerText=i,b.getElementsByTagName("head")[0].appendChild(l))}}},getWinHeight:function(){return Number.isNaN(this.metaWidth)?!this.isMobile&&(b.documentElement?.clientHeight||b.body?.clientHeight)||t.innerHeight:this.metaWidth/t.screen.width*t.innerHeight},getWinWidth:function(){return Number.isNaN(this.metaWidth)?this.isMobile?t.outerWidth:b.body?.clientWidth||b.documentElement?.clientWidth||t.innerWidth:this.metaWidth},init:function(){var e=b.querySelector("meta[name=viewport]");e&&"m"===p.view&&(e=/width=(\d+)/i.exec(e.getAttribute("content")))&&(this.metaWidth=Number.parseInt(e[1])),globalThis.asadlibLoaded?(this.mergeConfig(),p.adPlacements.forEach(e=>globalThis.ASCDP.adS.renderAd(e,p.adSlotSizes[e]))):(t.location.search.substring(1).split("&").forEach(e=>{e=e.split("=");"adlibBranch"===e[0]&&(p.branch=e.slice(1).join("=")),p.hasOwnProperty(e[0])&&(p[e.shift()]=e.join("="))}),p.branch=p.branch||"master","master"===p.branch&&50<=Math.floor(100*Math.random())&&(p.branch="abtest"),p.branchPath="https://www.asadcdn.com/adlib/beta/branches/"+p.branch+"/","master"===p.branch?p.branchPath="https://www.asadcdn.com/adlib/":"development"!==p.branch&&"beta"!==p.branch||(p.branchPath="https://www.asadcdn.com/adlib/beta/"),p?.siteName||(console.log("In order to load the adlib for your domain, please add 'siteName' property to the adConfig. Adlib will use supply and not generate adCalls."),p.hasPageAdMi=!1),p.placeholder&&p.adPlacements.forEach(e=>{this.addPlaceholder(e)}),!1!==p.autoStart?this.startLib():t.addEventListener("startAdvertising",this.startLib,{once:!0}))},mergeConfig:()=>{Object.keys(p).forEach(e=>{""!==p[e]&&("object"==typeof p[e]?"adSlotSizes"!==e&&p[e].length?ASCDP.pageSet[e]=[...ASCDP.pageSet[e],...p[e]]:ASCDP.adS.slotSizeMap[e]=p[e]:"target"===e?ASCDP.pageSet.targetString+=";"+p[e]:ASCDP.pageSet[e]=p[e])})},startLib:()=>{var e,t,i;window.ASCDP||(e=b.createElement("script"),t=b.createElement("script"),i=b.querySelector("script").parentNode,p.siteName=p.siteName||"supply",e.type="text/adConfig",e.innerText=JSON.stringify(p),t.async=!0,t.src=p.branchPath+`pages/${p.siteName}.js`,i.appendChild(e),i.appendChild(t))},isMobile:/Mobi|Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent),metaWidth:0}).init()})(window,document,adConfig);
    </script>
</head>
```

