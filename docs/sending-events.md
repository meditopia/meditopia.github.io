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

**Headers**

The Bearer Token in the request will be shared with you.

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <TOKEN>"
}
```

**Request Body**
```json
{
    "events": [
        {
            "token": "user-token-1",
            "partner_user_id": "user-1",
            "event": "video",
            "event_value": null,
            "received_at": "2024-08-06 15:04:05"
        },
        {
            "token": "user-token-2",
            "partner_user_id": "user-2",
            "event": "audio",
            "event_value": null,
            "received_at": "2024-08-06 15:04:05"
        }
    ]
}
```

* `token`: Unique user token that performed the event.
* `partner_user_id`: Unique ID of the user in your application.
* `event`: The performed event in your application. Could be one of the following:
  * `register`: User registered.
  * `signin`: User signed-in.
  * `audio`: User consumed a audio content.
  * `video`: User consumed a video content.
  * `content`: User consumed a content other than audio or video.
* `event_value`: Additional info about the event. If not exist just send `null`.
* `received_at`: Timestamp of the event.


**Sucessfull response ( Status Code: 204 )**
```json
204 - No Content
```

**Error response ( Status Code: 401, 404, 422 )**

Error codes:
* `A_1000 | A_1001` : Invalid or missing the Bearer Token. Check the `Authorization` header value.
* `A_1002` : Invalid Bearer Token.
* `A_1004` : Invalid IP Address. Check your server's IP and the ones you send us.

```json
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
