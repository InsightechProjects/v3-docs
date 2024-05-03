---
title: "iOS App SDK"
linkTitle: "iOS App SDK"
weight: 20
description: >
  
---
The iOS App SDK is designed for integrating analytics into iOS native applications. It facilitates data collection on user interactions, enabling developers to track events, screen views, and user identities efficiently.

## Create a Source

1. Go to the user interface and create a new source with the **iOS App SDK**.
2. You will receive a unique ID for data collection purposes.

## Installation

1. Download the SDK from here.
2. Drag and drop the SDK into your App using XCode.
3. In your App settings, go to the **General** tab. Under **Frameworks, Libraries, and Embedded Content**, locate the SDK and set it to "Embed & Sign" to complete the installation.

## Setup

To use the SDK, you need to import it and call the `setup` function with the server ID and source ID to specify the location of the data collection API endpoint. Here's an example of the code:

```swift
import DatacordSDK

DatacordSDK.setup(server: "server_id", sourceId: "source_id")
```

Upon initialization, the `setup` function not only automatically collects the `app_start` event but also assigns a `device_id` and `session_id`. These identifiers are then linked to all subsequent events to ensure consistent tracking throughout the session

## Track Screen View

Implement screen view tracking within the `onAppear` lifecycle event:

```swift
.onAppear {
	DatacordSDK.shared?.trackView(viewName: "screen_name")
}
```

## Tracking Custom Events

The `track` function allows you to capture custom event data, which is particularly useful for monitoring user interactions. These custom events are automatically linked to the most recent screen view, sharing the same `view_id` for cohesive tracking. Here's how you can implement this in your code:

```swift
let data: [String: Any] = [
	"prop1": "val1",
	"prop2": "val2"
]
DatacordSDK.shared?.track(event: "event_name", data: data)
```

## User Identification

The `trackView` and `track` functions can optionally include a user ID as a parameter when the user has been identified. This allows events to be associated with specific users. Here’s a couple of examples of how to implement this:

```swift
DatacordSDK.shared?.trackView(viewName: "screen_name", userId: "user_id_123")
```

```swift
let data: [String: Any] = [
	"prop1": "val1",
	"prop2": "val2"
]
DatacordSDK.shared?.track(event: "event_name", data: data, userId: "user_id_123")
```

You can also identify users by triggering a `user_identified` event. This method directly associates user IDs with subsequent data collection, streamlining user tracking. Here's an example of how to code this:

```swift
let data: [String: Any] = [
	"user_id": "user_id_123"
]
DatacordSDK.shared?.track(event: "user_identified", data: data)
```

Once a user is identified, there's no need to include the user ID in every event. The user ID will be linked to the device ID, allowing all subsequent events from that device to be automatically associated with the identified user.

## Event Batching

By default, events are immediately transmitted once functions are called. However, if you prefer batching events for later transmission, you can enable queuing by setting the `queueData` parameter to `true` when using the `track` and `trackView` functions. Here's how you can implement this:

```swift
let data: [String: Any] = [
	"prop1": "val1",
	"prop2": "val2"
]
DatacordSDK.shared?.track(event: "event_name", data: data, userId: "user_id_123", queueData: true)
```

Please note that queuing events for later transmission does not alter their timestamps. Each event will retain the timestamp from the moment it was originally created.