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
        "latestActionDate": "2025-02-07 22:16:40",
        "country": "tr",
        "planType": "YEARLYTEST008",
        "partnerUserID": "xx-yy-zz",
        "subStartDate": "2025-02-17 13:22:25",
        "subEndDate": "2026-02-17 13:22:25",
        "subStartDateMs": "1739798545534",
        "subEndDateMs": "1771334545534"
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
* `subStartDate` : UTC start date of the subscription in `YYYY-MM-DD HH:MM:SS` format.
* `subEndDate` : UTC end date of the subscription in `YYYY-MM-DD HH:MM:SS` format.
* `subStartDateMs` : Millisecond Unix timestamp of subscription start date.
* `subEndDateMs` : Millisecond Unix timestamp of subscription end date.

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
