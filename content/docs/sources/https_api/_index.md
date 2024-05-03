---
title: "HTTPS API"
linkTitle: "HTTPS API"
weight: 100
description: >
---
If you can't find an SDK suitable for your data collection needs, consider using the HTTPS API source type, which offers flexibility. While SDKs also utilize the HTTPS API, they simplify interaction and automate data handling tasks. You can send data in JSON format to your HTTPS API endpoint. Multiple events can be batched in a single request to minimize network calls. The JSON data should include fields such as event ID, event type, user ID, and timestamps, along with any additional event-specific data. Here’s an example structure for sending data:

```json
[{
	"event_id": "event_unique_id_1",
	"event": "event_type_1",
	"user_id": "user_123",
	"device_id": "device_unique_id",
	"session_id": "session_123",
	"view_id": "pageview_xyz",
	"timestamp": 1683363983423,
	"data": {
		"prop1": "value1",
		"prop2": "value2"
	}
},
{
	"event_id": "event_unique_id_2",
	"event": "event_type_2",
	"user_id": "user_123",
	"device_id": "device_unique_id",
	"session_id": "session_123",
	"view_id": "pageview_xyz",
	"timestamp": 1683363983423,
	"data": {
		"prop1": "value1",
		"prop2": "value2"
	}
}]
```

## Event fields

- **event_id** (required): Unique identifier for each event.
- **event** (required): Describes the type of event, like "pageview" or "click".
- **user_id** (optional): Links events to a specific user.
- **device_id** (required): Identifies the device generating the event.
- **session_id** (optional): Identifies the session; absence of this may trigger new session identification based on activity timing.
- **view_id** (optional): Identifies the view or screen.
- **timestamp** (required): Records the exact time of the event in milliseconds.
- **data** (optional): Allows inclusion of custom data with constraints on property names and quantity.