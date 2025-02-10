# User Check

### Introduction

You can use this endpoint, when you need to check current state of the user on Meditopia's side.
It can be useful when you are not sure whether current state of the given user is not sync with yours.

### Request

**URL**
> GET https://partners.meditopia.com/default/v1/user-check?token=xxx-yyy

---

**Headers**

?> The Bearer Token in the request will be shared with you.

```js
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <TOKEN>"
}
```

---

**Sucessfull response ( Status Code: 200 )**

```js
{
    "success": true,
    "data": {
        "userStatus": "inactive",
        "latestAction": "canceled",
        "latestActionDate": "2025-02-07T22:16:40.144Z",
        "country": "tr",
        "planType": "YEARLYTEST008",
        "partnerUserID": "damdam"
    }
}
```

* `userStatus` : Represents the current user state. Can be one of following:
  * `active`
  * `inactive`
* `country` : Country of the user.
* `planType` : The subscription plan.
* `partnerUserID` : The unique ID of the user in your application.
* `latestAction` : The latest action of the user.
* `latestActionDate` : The timestamp of the latest action of the user.

---

**Error response ( Status Code: 401, 404, 422 )**

```js
{
    "success": false,
    "errors": [
        {
            "code": "G_1005",
            "message": "Error while decrypting token."
        }
    ]
}
```
