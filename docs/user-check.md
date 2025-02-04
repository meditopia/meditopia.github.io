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
        "user_status": "active",
        "country": "tr",
        "plan_type": "YEARLY01",
        "partner_user_id": "test-3rdparty-user-id",
        "latest_action": "audio",
        "latest_action_date": "2025-01-01T00:00:00Z"
    }
}
```

* `user_status` : Represents the current user state. Can be one of following:
  * `active`
  * `inactive`
* `country` : Country of the user.
* `plan_type` : The subscription plan.
* `partner_user_id` : The unique ID of the user in your application.
* `latest_action` : The latest action of the user.
* `latest_action_date` : The timestamp of the latest action of the user.

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
