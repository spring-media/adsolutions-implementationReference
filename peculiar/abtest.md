# Propagate ab test data to the adserver reports

For a publisher it is possible to flag the data the adserver aggregates to a specific abtest. This way changes on the publisher side can be analysed using the advertising data they generated for different testgroups.
To make use of this feature a publisher needs to pass the data to the adlib and therefore has two options:

# Option 1 - directly add to adSSetup.target

The structure for abtest data for the target string may be of key value pairs or just values, e.g.:

```
<script type="text/javascript">
  // adding key value pairs
  const adSSetup = {
    ...
    target: "abtest=testname:bild-login-test,testgroup:loggedIn;"
  };
</script>

<script type="text/javascript">
  // adding values only
  const adSSetup = {
    ...
    target: "abtest=blackpagebackground,true;"
  };
</script>
```

# Option 2 - send by custom event (should be done as soon as possible)

The structure for abtest data for the target string may be of key value pairs or just values, e.g.:

```
<script type="text/javascript">
  // passing an object
  const adTechEvent = new CustomEvent("abdata", {
      "detail": {
          "testname": "bild-login-test",
          "testgroup": "loggedIn"
      }
  });
  document.dispatchEvent(adTechEvent);
</script>

<script type="text/javascript">
  // passing a string
  const adTechEvent = new CustomEvent("abdata", "blackpagebackground,true");
  document.dispatchEvent(adTechEvent);
</script>
```

The data can be analysed by taking a key value report by the key "abtest" from the adserver.

## Contact

__Team AdTechnology__<br/>
[adtechnology@axelspringer.com](mailto:adtechnology@axelspringer.com)

