# User Status Webhook

### Introduction

You need to setup a webhook endpoint to receive notifications on user state changes. These notifications notifies endpoint when:
* A new user registers,
* A user renews their subscription,
* A user cancels their subscription,
* A user reactivates their subscription,
* A user changes the subscription plan.

Depending on these events you should grant/revoke/extend user's access to the premium contents of your application.

### Webhook Payload

This is the payload that your webhook endpoint is going to receive. There can be additional fields in the payload, you can ignore those.

```js
{
    "token": "xxx-yyy-zzz",
    "action": "initial",
    "partnerID": "partner-123",
    "country": "tr",
    "planType": "premiumYearly",
    "subStartDate": "2025-02-17 13:22:25",
    "subEndDate": "2026-02-17 13:22:25",
    "subStartDateMs": "1739798545534",
    "subEndDateMs": "1771334545534"
}
```

* `token` : Represents the unique user token that performed the action.
* `action` : The performed action. Can be one of following:
  * `initial` : User started their subscription.
  * `renewed` : User renewed their subscription.
  * `canceled` : User canceled their subscription.
  * `reactivated` : User reactivated their subscription.
  * `planTypeChanged` : User changed the type of subscription plan.
* `partnerID` : The unique ID of your application.
* `country` : Country of the user.
* `planType` : The subscription plan.
* `subStartDate` : UTC start date of the subscription in `YYYY-MM-DD HH:MM:SS` format.
* `subEndDate` : UTC end date of the subscription in `YYYY-MM-DD HH:MM:SS` format.
* `subStartDateMs` : Millisecond Unix timestamp of subscription start date.
* `subEndDateMs` : Millisecond Unix timestamp of subscription end date.

### Implementation Guide
When a user wants to use your application through Meditopia, following will happen in order.

1. Your webhook endpoint will receieve notification with `action: initial`. You should store this payload somewhere for later use.
2. User will be redirected to your partner register page with the user `token` and `language` values present in the url. ( eg. https://auth.mindfulness-app.com/?token=xxx-yyy-zzz&language=tr )
3. After user submits the register form, you should match register information with the payload you received in the step 1 via `token` field.
4. From this point on, this user should be marked as 'Meditopia partner user' on your end to distinguish them from regular users. This step can be implemented based on your choose.
5. After successfull initial registration you should store a `register` event for this user to send to our Event API ( check Sending Events docs ).
