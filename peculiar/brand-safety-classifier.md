# AdTech Brand Safety Classifier

This is your implementation guide for our Brand Safety Classifier.
Please call the API when a new article is published.

<br>


## Table of Contents

 - [What is the Brand Safety Classifier?](#what-is-the-brand-safety-classifier)
 - [Request Parameter](#request-parameter)
 - [POST Request](#post-request)
 - [Response Formats](#response-formats)
    - [Resonse with multiple brand-safety matches](#resonse-with-multiple-brand-safety-matches)
    - [Response with no brand-safety match](#response-with-no-brand-safety-match)
    - [Response with an error](#response-with-an-error)
 - [Error Handling](#error-handling)
 - [Apply response to adSSetup config](#apply-response-to-adssetup-config)
 - [Request Frequency](#request-frequency)
 - [Important Notes](#important-notes)
 - [Help](#help)



<br>
<br>


## What is the Brand Safety Classifier?

Our Brand Safety Classification API is a non critical service, that will enable our marketers to create better brand safe products for advertisers.
Publishers can simply add a request that gets the related keywords for a given article and save these keywords in the CMS, so that these can later be used for targeting in the adSSetup object.

In the ideal case, the service is called only once when a new article is published. Keep in mind, that you should not add this request into the time critical publishing pipeline - but simply let the request run in parallel. It is okay if the article is going live without these keywords. When the response from this API is ready, you can just enrich the article with these keywords.


<br>
<br>



## Request Parameter

Here's the requested information converted into a markdown table:

| Parameter   | Type   | Description                   | Required |
|-------------|--------|-------------------------------|----------|
| title       | string | The title of the article      | true     |
| content     | string | The content of the article    | true     |
| publisher   | string | The publisher of the article  | true     |
| article_id  | string | The ID of the article         | true     |



<br>
<br>

## POST Request

Send your `POST` request to `https://classifier.prd.adtech.as-infra.de/brand-safety`.

We expect a json object in the following format:

```json
{
    "title": "10 reasons why your dog is eating grass",
    "content": "The content shouldn't include widgets or html nodes, but only plain text as string.",
    "publisher": "publisher.de",
    "article_id": "uniqueId123"
}
```



<br><br>



## Response Formats

### Resonse with multiple brand-safety matches

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

<br>

### Response with no brand-safety match

```json
{
    "status": "OK",
    "classification": {
        "matches": [ ]
    }
}
```

<br>

### Response with an error

```json
{
	"status": 400,
	"error": "Invalid Syntax",
	"message": "Please check the syntax and parameters of your request."
}
```




<br><br>


## Error Handling

This is an overview of the error codes you might see, along with suggestions on how to handle them.

<br>


| Status | Error               | Explanation                                            | Solution                                               |
|--------|---------------------|--------------------------------------------------------|--------------------------------------------------------|
| 429    | Rate Limit Error    | Too many requests                                      | Wait for some time before making new requests.         |
| 400    | Invalid Syntax      | Please check the syntax and parameters of your request.| Verify the request syntax and parameters are correct.  |
| 500    | Internal Server Error| An error occurred while processing the request.       | Try to send the request again. If you get this error frequently, please contact us via adtechnology@axelspringer.com |
| 404    | Not Found           | The requested resource was not found.                  | Verify that you are sending your request to the correct endpoint.    |
| 408    | Request Timeout     | The response from Azure was not finished in 30 seconds and timed out.  | As we are making requests to an Azure service, it is possible that these time out. <br>We have a timeout limit of 30 seconds - if you receive this error, just try to send the request again. |
| 500    | Unknown Error       | An unknown error occurred.                             | Please contact us via adtechnology@axelspringer.com and try to send the request again. |





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


