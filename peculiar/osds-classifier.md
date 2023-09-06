# OSDS Classifier

This is your implementation guide for the OSDS Contextual Classifier.
Please call the API when a new article is (re-) published.

<br>


## Table of Contents





<br>
<br>


## POST Request


Send your `POST` request to `https://oghub-rmscontextual-mi-p.ew.r.appspot.com/iabcategories?url=" + articleUrl`.

<br>
<br>


## Response



```json
{
  "data": {
    {
      "validUntil": 1692265049490,
      "requestId": "b00d7116212ac0514018c8941e8e2b55",
      "requestedAt": 1689673047895,
      "categories": {
          "Medical Health: 286": 0.5452159,
          "Health Insurance: 399": 0.9983974,
          "Personal Finance: 391": 0.93517065,
          "Insurance: 398": 0.99965286,
          "Business and Finance: 52": 0.43605074
      },
      "status": "DONE"
    }

  }
}
```

Please make sure that the categories object exists and is filled in the response.
Write the `res.data.categories` node into our adSSetup like this:

```javascript
adSSetup.iabTax = JSON.stringify(res.data.categories);
```


<br><br>


## Authentification

To send the request successfully, you have to authenticate. You can use the following token for this process:

```javascript
const {GoogleAuth} = require('google-auth-library');

const auth = new GoogleAuth();
const client = await auth.getIdTokenClient("325807998263-meo5591pc8ep2a02vf3fo25uoa152fia.apps.googleusercontent.com");
```

<br>

However, you have to use a `credentials.json` file. Contact the AdTechnology team via `adtechnology@axelspringer.com` to get a credentials.json file.

Also, please have a look [into this demo project](https://github.com/spring-media/adsolutions-osds-demo/blob/main/src/classifier.js), to see a basic working implementation of the API and the authentication.

https://github.com/spring-media/adsolutions-osds-demo/

<br>
<br>




## Important Notes


> :warning: Warning!
> ----------------
> Please do **NOT** call the API in a migration scenario,
> where the content of the articles is not changed.
> Every single classification costs money.



<br>
<br>






