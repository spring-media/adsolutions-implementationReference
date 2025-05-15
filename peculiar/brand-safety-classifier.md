# AdTech Brand Safety Classifier

This is your implementation guide for our Brand Safety Classifier.
Please call the API when a new article is published.

<br>


## Table of Contents

 - [What is the Brand Safety Classifier?](#what-is-the-brand-safety-classifier)
 - [Sentiment Analysis](#sentiment-analysis)
    - [Sentiment Keyvalues Overview](#sentiment-keyvalues-overview)
    - [Classification Conditions](#classification-conditions)
 - [Request Parameter](#request-parameter)
 - [POST Request](#post-request)
 - [Response Formats](#response-formats)
    - [Resonse with multiple brand-safety matches](#resonse-with-multiple-brand-safety-matches)
    - [Response with no brand-safety match](#response-with-no-brand-safety-match)
    - [Response with an error](#response-with-an-error)
 - [Caching Strategy](#caching-strategy)
 - [Error Handling](#error-handling)
 - [Apply response to adSSetup config](#apply-response-to-adssetup-config)
 - [Request Frequency](#request-frequency)
 - [Xandr Keyword Overview](#xandr-keyword-overview)
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

## Sentiment Analysis

As of May 2025 we also classify sentiments on articles.<br>
As long as you enrich the AdSSetup targets dynamically with the delivered keyvalues, you do not need to make changes on how you handle the classification response.

### Sentiment Keyvalues Overview

| Key Name    | Values                     | Description                    | 
|-------------|----------------------------|--------------------------------|
| mood_amuse  | high, low, medium, veryLow | Sentiment Analysis: Amusement  | 
| mood_anger  | high, low, medium, veryLow | Sentiment Analysis: Anger      | 
| mood_fear   | high, low, medium, veryLow | Sentiment Analysis: Fear       | 
| mood_enjoy  | high, low, medium, veryLow | Sentiment Analysis: Enjoyment  | 
| mood_insp  | high, low, medium, veryLow | Sentiment Analysis: Inspiration | 
| mood_optm  | high, low, medium, veryLow | Sentiment Analysis: Optimism    | 
| mood_sad   | high, low, medium, veryLow | Sentiment Analysis: Sadness     | 


<br>
<br>



### Classification Conditions

#### 1. **Amusement**
- Content is light-hearted, playful, comedic, or designed to entertain. The primary emotional response is smiling, laughter, or a sense of fun.  
- Is applied if the main tone is funny, witty, satirical, or features feel-good entertainment, memes, harmless pranks, light pop culture, etc.  
- **Sample:** _"See how Berlin’s ducks caused the morning commuter chaos — again!"_

---

#### 2. **Anger**
- Content may evoke strong displeasure, frustration, or outrage—usually about injustice, failure, controversy, or scandal. Focus is on conflict, blame, or aggressive criticism.  
- Is applied when the article features scandal, accusations, heated debates, outrage, or exposes wrongdoing. (Not for all negative news, only when anger dominates.)  
- **Sample:** _"Public outcry after politician’s expense fraud uncovered"_

---

#### 3. **Fear**
- Content emphasizes threats, anxieties, dangers, or risks. The primary emotion is concern, worry, or distress about potential harm (physical, economic, societal, etc.).  
- Is applied when the story induces fear or anxiety (e.g., disasters, crime spikes, health scares, war, warnings).  
- **Sample:** _"Rise in new COVID variant cases worries health experts"_

---

#### 4. **Inspiration**
- Content that uplifts, motivates, or encourages the reader. The main response is admiration, a desire to emulate, or feeling hopeful through positive action or resilience.  
- Is applied for stories about overcoming adversity, heroic acts, personal triumphs, major social impact, or profiles meant to motivate the audience.  
- **Sample:** _"Paralympian’s journey from accident to gold medal success"_

---

#### 5. **Optimism**
- Content focused on positive developments, hope for the future, or improvements. The tone is upbeat, reassuring, and forward-looking.  
- Is applied when the article emphasizes solutions, improvements, positive forecasts, or new opportunities — rather than just celebrating individuals ("inspiration"), it’s about society or context.  
- **Sample:** _"German economy expected to rebound strongly next year"_

---

#### 6. **Sadness**
- Content that deals with loss, mourning, tragedy, or negative outcomes. The dominant emotional response is sorrow, sympathy, or regret.  
- Is applied for reporting on deaths, disasters, personal loss stories, major setbacks, or when a sympathetic tone is foregrounded.  
- **Sample:** _"Community mourns loss of beloved local teacher"_

---

#### 7. **Enjoyment**
- Content centered on pleasure, satisfaction, or delight—about experiences, events, or activities that offer joy and fun (distinct from "amusement", which is humor-based).  
- Is applied when the article covers positive lifestyle stories, leisure activities, travel, gastronomy, or cultural events with a tone of enjoyment rather than laughter.  
- **Sample:** _"A guide to enjoying the best summer festivals in Munich"_



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

## Caching Strategy

Currently we implemented a provisional caching system. 
We plan to improve the functionality and its features in the future, but for now we have the following rules in place:

 - The first time a new `article_id` is seen, the article contents will be classified by the AI service (which sometimes can take a few seconds) and is then stored in the cache.
 - every following request with this `article_id` is checked, if the article title and/or contents have changed for more than 20%. If so, the article will be classified again and the cache will be updated.

With this basic caching, we reduce response times as well as costs for the service. Also, since we will be running into the rate limits less frequently, we can ensure a more stable service.
In the future, there will be an option to force a cache update on your own.



<br><br>



## Error Handling

This is an overview of the error codes you might see, along with suggestions on how to handle them.

<br>


| Status | Error               | Explanation                                            | Solution                                               |
|--------|---------------------|--------------------------------------------------------|--------------------------------------------------------|
| 429    | Rate Limit Error    | Too many requests                                      | Wait for some time before making new requests. Rate limits are calculated with token per minute - so it is hard to say a specific number of requests that can produce this error. However, with caching in place, this shouldn't happen very often. |
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





## Xandr Keyword Overview

Here's an overview of the brand safety keywords in Xandr. The possible values for each keyword are [`veryLow`, `low`, `medium`, `high`]:


| Xandr Keyword  | Brand Safety Category                 |
|----------------|---------------------------------------|
| bs_adlt        | Adult & Explicit Sexual Content       |
| bs_arms        | Arms & Ammunition                     |
| bs_crime       | Crime & Harmful Acts to Individuals and Society and Human Right Violations  |
| bs_death       | Death, Injury, or Military Conflict   |
| bs_prcy        | Online Piracy                         |
| bs_htsp        | Hate Speech & Acts of Aggression      |
| bs_prof        | Obscenity and Profanity               |
| bs_drug        | Illegal Drugs/Tobacco/E-Cigarettes/Vaping/Alcohol |
| bs_spam        | Spam or Harmful Content               |
| bs_terr        | Terrorism                             |
| bs_ssis        | Sensitive Social Issues               |
| mood_amuse     | Sentiment Analysis: Amusement         | 
| mood_anger     | Sentiment Analysis: Anger             | 
| mood_fear      | Sentiment Analysis: Fear              | 
| mood_enjoy     | Sentiment Analysis: Enjoyment         | 
| mood_insp      | Sentiment Analysis: Inspiration       | 
| mood_optm      | Sentiment Analysis: Optimism          | 
| mood_sad       | Sentiment Analysis: Sadness           | 

_Experience has shown that articles are mainly flagged with the categories_ `bs_crime` _and_ `bs_death`.


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


