---
title: "Overview of Event Data"
linkTitle: "Overview of Event Data"
weight: 10
description: >
---
## Event Schema

Data sent to the system is processed in the form of events, where each event is encapsulated in a structured format as shown below.

```json
{
	"event_id": "event_unique_id",
	"event": "event_name",
	"user_id": "user_123",
	"device_id": "device_unique_id",
	"session_id": "session_123",
	"view_id": "pageview_xyz",
	"timestamp": 1683363983423,
	"data": {
		"prop1": "ABC",
		"prop2": "test"
	}
}
```

Here's a detailed breakdown of each field in the event schema:

- **event_id (required):** A unique identifier for the event. Note that the system does not de-duplicate events based on this ID, and reusing an ID may impact analytical outcomes.
- **event (required):** A string that specifies the type of event, such as `pageview` for viewing web pages or `web_click` for mouse clicks. Certain types of events may activate specific processing logic.
- **user_id (optional):** Identifies the user; associating this field ties the event to a specific user, linking subsequent events from the same device to that user.
- **device_id (required):** A unique identifier for the device generating the event. Linking this with a user ID connects all events from this device to the identified user.
- **session_id (optional):** A unique identifier for the session, maintained by the client-side SDK. If not provided, the system uses a 30-minute window to determine session starts.
- **view_id (optional):** Identifies the specific view, like a webpage or app screen.
- **timestamp (required):** Records the time of the event in milliseconds.
- **data (optional):** A JSON object holding custom data variables, where property names should not begin with an underscore.
