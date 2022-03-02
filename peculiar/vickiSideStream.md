# Vicki: SideStream Player

Vicki is a videoadvertising element that will, once it's loaded, render a fixed videoplayer 
that plays content videos of the publisher interrupted by videoads.

The publisher therefore has the option to configure some things like the button or 
headerbar colors so that the player fits to the publishers appearence.

He may also listen to events the player will propagate to realize his video tracking.
Available events to listen:

```
const videoEvents = ['init', 'play', 'pos', 'pause', 'resume', 'end', 'ad_start', 'ad_play', 'ad_quartile', 'ad_end', 'ad_error', 'ad_pause', 'ad_resume', 'ad_skip', 'ad_fullscreen_on', 'ad_fullscreen_off', 'ad_mute', 'ad_unmute'];
```

The details property of the event object will be a reference to the player.
As an example for autobild.de we realized the data passing to adobe via tealiums utag_data object as shown here:

    /* Aubi to Adobe event */
    const videoEvents = ['init', 'play', 'pos', 'pause', 'resume', 'end', 'ad_start', 'ad_play', 'ad_quartile', 'ad_end', 'ad_error', 'ad_pause', 'ad_resume', 'ad_skip', 'ad_fullscreen_on', 'ad_fullscreen_off', 'ad_mute', 'ad_unmute'];

    for (let i = 0; i < videoEvents.length; i++) {
        var eventName = videoEvents[i];
        document.addEventListener("vicki_" + eventName, function (e) {
            let player = e.detail && e.detail.player_ ? e.detail : false;
            let eventtype = e.type.replace("vicki_", "");
            let title = e.detail.srcData.title;
            let linkurl = e.detail.srcData.clickUrl;
            let titlematch = title.match(/(.*)\s-\s(.*)\s/) || [];
            let mediakicker = titlematch[1] || "";
            let mediaHeadline = titlematch[2] || "";
            let videoId = (linkurl.match(/([0-9]+)\./) || ["undefined", 0])[1];
            let trackData = {
                "event_name": "video",
                "event_action": eventtype,
            }
            if (player && player.plays === "vast") {
                trackData["event_label"] = player.thirdQuartileDone ? "75" : player.midPointDone ? "50" : player.firstQuartileDone ? "25" : "0"; //nur bei ad_quartiles notwendig
            } else {
                if (eventtype === "end") {
                    trackData["event_action"] = "eof";
                }
                if (eventtype === "timeupdate" && player.currentTime()%10 === 0) {
                    trackData["pos"] = "pos";
                    trackData["event_label"] = player.currentTime(); //nur bei pos notwendig
                }
                trackData["event_data"] = {
                    "media_id": videoId,
                    "media_type": "video",
                    "media_player": "vicki",
                    "media_kicker": mediakicker,
                    "media_headline": mediaHeadline,
                    "media_path": linkurl.replace(location.origin, ""), // hier bitte bitte nur der pfad der URL
                    "media_is_autoplay": true, //"true"|"false"
                    "media_is_muted": player ? player.muted() : true, //"true"|"false"
                    "media_is_fullscreen": player ? player.isFullscreen() : false, //"true"|"false"
                    "media_pub_date": e.detail.srcData.pubDate && e.detail.srcData.pubDate !== "unknown" ? new Date(e.detail.srcData.pubDate).toISOString().replace(/T.*/i, "") : "unknown" //"YYYY-MM-DD"
                }
            }
            window.utag.link(trackData);
        });
    }