#Step by step documentation of adlib processing (regard last updated date)

1. set global fif var to false
2. init ASCDP main object
3. init ASCDP.pageSet while importing adSSetup if defined
    3.2 for AMP define ASCDP.pageSet.availableSlots by adSSetup
4. set reference to actual window as ASCDP.window
5. detect iFrame integration
6. process autoreloader for home switch
7. set rlSlot CSS
8. create ASCDP_CSS style tag
9. append OBA style tag
10. define ASCDP.getUrlParameter
11. define module and script loader
12. predefine collector objects ASCDP.adtemplates and ASCDP.partners
13. define ASCDP.hashMap
14. define ASCDP.adS:
    * properties:
    * direct defined methods:
    * preload modules:
15. try to get consent cookie and save it as ASCDP.pageSet.tcString
16. process tcf.js:
    * define tcData analyser
    * define tcData addTCListener - for OT intercept their listener method
    * define tcData hideForPreview
    * check for cmp, if no cmp found process
      * read cookies and set ASCDP.pageSet.cookies + define if not accessible ASCDP.pageSet.cookies.springUG
      * getHeidi and setUserGroup
    * if found register listener
17. send adlibLoaded event
18. load ast and ast relevant modules
19. if exists process adlibLoaded measurement
20. check if 
    * adSSetup is defined
    * ads may be loaded
    * adlib hasn't already been loaded and processed
    * isn't framed beside dooh or amp
20.1 if true
    * check for target "badcontent" to disable DFP
    * register listener for
      * message
      * slotAvailable
      * renderAd
      * reloadAds
    * load requiredJS
    * do speedCheck
    * process tcf relevant things when no cmp has been detected
    * filter placement doubles and 
    
    