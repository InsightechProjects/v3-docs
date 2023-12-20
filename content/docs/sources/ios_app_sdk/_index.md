---
title: "iOS App SDK"
linkTitle: "iOS App SDK"
weight: 20
description: >
  
---
To collect data from your iOS native app, you need to implement the Swift SDK for iOS.

## Create the source

Go to the user interface and create a new source using the **iOS App SDK**. The source will be assigned a unique ID that will be used to identify it for data collection.

## Installation

1. Download the SDK from [here].
2. Drag and drop the SDK into your App using XCode.
3. In your App settings, go to the **General** tab. Under **Frameworks, Libraries, and Embedded Content**, locate the SDK and set it to "Embed & Sign" to complete the installation.

## Setup the SDK

To use the SDK, you need to import it and call the `setup` function with the server ID and source ID to specify the location of the data collection API endpoint. Here's an example of the code:

```swift
import DatarooSDK

DatarooSDK.setup(server: "server_id", sourceId: "source_id")

```

The `setup` function will automatically collect the `app_start` event and set the `device_id` and `session_id`, which will be associated with all subsequent events.

## Collect screen view event data

To track a screen view event when a screen is loaded, use the following code with the screen name:

```swift
DatarooSDK.shared?.trackView(viewName: "screen_name")

```

The `trackView` function is typically called within the `onAppear` event. For example:

```swift
.onAppear {
	DatarooSDK.shared?.trackView(viewName: "dashboard_view")
}

```

## Collect custom event data

You can collect custom event data using the `track` function. Custom event data can be used to track user interactions. The events will be automatically attached to the latest screen view event and share the same `view_id`. Here's an example of the code:

```swift
let data: [String: Any] = [
	"prop1": "val1",
	"prop2": "val2"
]
DatarooSDK.shared?.track(event: "event_name", data: data)

```

## Identify the user

The `trackView` and `track` functions can take the user ID as an input parameter if the user is identified. For example:

```swift
DatarooSDK.shared?.trackView(viewName: "screen_name", userId: "user_id_123")

```

```swift
let data: [String: Any] = [
	"prop1": "val1",
	"prop2": "val2"
]
DatarooSDK.shared?.track(event: "event_name", data: data, userId: "user_id_123")

```

Another way to identify the user is by using the specific event `user_identified`. Here's an example of the code:

```swift
let data: [String: Any] = [
	"user_id": "user_id_123"
]
DatarooSDK.shared?.track(event: "user_identified", data: data)

```

There is no need to send the user ID in every event because once the user is identified, the user ID will be associated with the device ID and all events from the device will be automatically associated with the user.

## Queue the events

By default, events are sent immediately when the functions are called. However, if you don't want to send the events immediately, you can put them into a queue and send them in a batch. To do this, set the `queueData` parameter to `true` when calling the `track` and `trackView` functions. Here's an example of the code:

```swift
let data: [String: Any] = [
	"prop1": "val1",
	"prop2": "val2"
]
DatarooSDK.shared?.track(event: "event_name", data: data, userId: "user_id_123", queueData: true)

```

Please note that queuing the events won't affect the timestamps of the events. The events will still have the original timestamps when they were created.