# Sending Events

### Introduction

Use this endpoint to send the actions users performed in your application to the Mediopia Partners API. 

We recommend sending these events on scheduled intervals.

### Limitations & Notes
* Only the IP's you share can send data to this API.
* You can send maximum of 100 events on each request.
* If one of the events has a error ( eg. user not found, invalid event type etc. ) none of the events in the payload are processed. You have to send them again.

### Request

**URL**
> POST https://partners.meditopia.com/default/v1/events

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

**Request Body**
```js
{
    "events": [
        {
            "token": "Ul862KQgtqyWMekaDDfziZWUG70UkSdyO1SUKUVAlvcH4RMWZlriOS6re1AgTkTgo13_J4IJtmMBUNp7z10TSo4sjJOW1AJfwIZ3XcMZYoT05dZiChtJ-A3-6P3ZcX8nrz-2LMDBMNkALnWrlxAhaiNPEZM",
            "partnerUserID": "partner-test-id-1",
            "event": "register",
            "eventValue": "test_val",
            "receivedAt": "2024-01-02 15:04:05"
        },
        {
            "token": "Ul862KQgtqyWMekaDDfziZWUG70UkSdyO1SUKUVAlvcH4RMWZlriOS6re1AgTkTgo13_J4IJtmMBUNp7z10TSo4sjJOW1AJfwIZ3XcMZYoT05dZiChtJ-A3-6P3ZcX8nrz-2LMDBMNkALnWrlxAhaiNPEZM",
            "partnerUserID": "partner-test-id-1",
            "event": "audio",
            "eventValue": null,
            "receivedAt": "2024-01-03 10:10:10"
        },
        {
            "token": "PeGxEkupo5cEZ3AJahPmmufqONGrlGyWd9_Us7ODyHLFI5hs-2NtM7dOAHskJQe2Bmw9IFqXnwy33G9zUMsCUOxFdmo8TAwV2iPdscYxiMCV8g59UOXAyRnKUECGxp2xgj1EPxVV35h5WmLkTj5-FnRsqqDm54c",
            "partnerUserID": "partner-test-id-2",
            "event": "register",
            "eventValue": "test_val4",
            "receivedAt": "2024-02-03 10:10:10"
        }
    ]
}
```

* `token`: Unique user token that performed the event.
* `partnerUserID`: Unique ID of the user in your application.
* `event`: The performed event in your application. Could be one of the following:
  * `register`: User registered.
  * `signin`: User signed-in.
  * `audio`: User consumed a audio content.
  * `video`: User consumed a video content.
  * `content`: User consumed a content other than audio or video.
* `eventValue`: Additional info about the event. If not exist just send `null`.
* `receivedAt`: Timestamp of the event.

---

**Sucessfull response ( Status Code: 204 )**

```json
204 - No Content
```

---

**Error response ( Status Code: 401, 404, 422 )**

Error codes:
* `A_1000 | A_1001` : Invalid or missing the Bearer Token. Check the `Authorization` header value.
* `A_1002` : Invalid Bearer Token.
* `A_1004` : Invalid IP Address. Check your server's IP and the ones you send us.

```js
{
    "success": false,
    "errors": [
        {
            "code": "A_1004",
            "message": "Bad request."
        }
    ]
}
```
