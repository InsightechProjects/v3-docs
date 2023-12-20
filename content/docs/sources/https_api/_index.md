---
title: "HTTPS API"
linkTitle: "HTTPS API"
weight: 100
description: >
  
---
If you are unable to find an SDK for the channel from which you want to collect data, using the HTTPS API source type is always a flexible option. The SDKs also collect data via the HTTPS API, but they provide an interface to interact with the API endpoint and automate specific data collection tasks.

Once you have created an HTTPS API endpoint, you can send the data to the endpoint in the following JSON format. Each request can collect multiple events as an array, reducing the number of network requests.

```json
[{
	event_id: "event_unique_id",
	event: "event_type",
  user_id: "user_123",
	device_id: "device_unique_id",
	session_id: "session_123",
	view_id: "pageview_xyz",
	timestamp: 1683363983423,
	data: {
		prop1: "ABC",
		prop2: "test"
	}
},
...
]
```

## Event fields

- **id** - required: This is the unique identifier of the event. Reusing the same ID may not result in de-duplication of the event, but it could impact the analytics results.
- **type** - required: This is a string value that indicates the type of event, such as "pageview" for website page views or "click" for clicks. Certain event types may trigger special logic in the data processing.
- **user_id** - optional: When set, the `user_id` associates the device with a specific user.
- **device_id** - required: This is the unique identifier of the device that generates the event. If a user is identified, the `user_id` will be linked to the `device_id` when the data is processed, and all events associated with the device will also be associated with the user.
- **session_id** - optional: This is the unique identifier of the session. The client-side SDK can maintain the session and include the `session_id` in the requests. If the `session_id` is empty, the data processor will use a 30-minute window to determine if the event marks the start of a new session.
- **view_id** - optional: This is the unique identifier of the view, such as a page view or mobile app screen.
- **timestamp** - required: This is the millisecond timestamp of the event.
- **data** - optional: This is a one-level nested JSON object that can contain custom data. The property names in the JSON must not start with an underscore. Each event can have a maximum of 50 properties in the `data` field.