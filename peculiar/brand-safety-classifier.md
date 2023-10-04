# AdTech Brand Safety Classifier

This is your implementation guide for our Brand Safety Classifier.
Please call the API when a new article is (re-) published.

<br>


## Table of Contents

 - [POST Request](#post-request)
 - [Response](#response)
 - [Apply response to adSSetup config](#apply-response-to-adssetup-config)
 - [Request Frequency](#request-frequency)
 - [Important Notes](#important-notes)
 - [Help](#help)



<br>
<br>


## POST Request

Send your `POST` request to `https://verify.asadcdn.com/brand-safety-classifier`.

We expect a json object in the following format:

```json
{
    "title": "10 reasons why your dog is eating grass",
    "content": "The content shouldn't include widgets or html nodes, but only plain text as string.",
    "publisher": "publisher.de"
}
```



<br><br>



## Response

```json
{
    "status": "OK",
    "classification": {
        "matches": [
            {
                "category": "Crime & Harmful Acts to Individuals and Society and Human Right Violations",
                "keyValueTarget": {
                    "key": "bs_crime",
                    "value": "high"
                }
            },
            {
                "category": "Death, Injury, or Military Conflict",
                "keyValueTarget": {
                    "key": "bs_death",
                    "value": "medium"
                }
            }
        ]
    }
}
```




<br><br>



## Apply response to adSSetup config

Now that we have received our classification response, we can simple take the keyValueTargets from the matched categories (_if there are any_) and write them into the adSSetup.target.
You can use something like the following code snippet:

```javascript
for (var match of classification.matches) {
  adSSetup.target += `${match.key}=${match.value};`;
}
```

<br>

When included, the adSSetup should look something like this:

```javascript
  adSSetup.target = "bs_crime=high;bs_death=medium;";
```


Please make sure, that you do not overwrite the adSSetup.target object, but add the values (since the target object can be quite full with a lot of relevant targeting information).
If there are multiple matching categories, you can separate them by a semicolon.



<br><br>

## Request Frequency

A short note about the frequency of requests related to a single article.
Please do not send requests on little editorial changes on the articles as this process is connected to costs. 
It should be enough to only send the initial published article content for the classification, since the general context or brand safety is unlikely to be affected by minor updates to the article's wording.



<br><br>



## Important Notes


> :warning: Warning!
> ----------------
> Please do **NOT** call the API in a migration scenario,
> where the content of the articles is not changed.
> Every classification costs us money and we can not guarantee,
> that the API will work stable in case of thousands of requests at the same time.



<br><br>





## Help

If something is unclear or you have any questions, you can contact us via email:


__Ad Technology Team__
adtechnology@axelspringer.de




<br>


