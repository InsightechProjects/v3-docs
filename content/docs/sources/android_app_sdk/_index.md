---
title: "Android App SDK"
linkTitle: "Android App SDK"
weight: 30
description: >
---
The Kotlin SDK for Android enables efficient data collection from native Android applications, streamlining user interaction tracking and event management.

## Create a Source

1. Visit the user interface to create a new source using the **Android App SDK**.
2. Obtain a unique ID for this source to facilitate data collection.

## Installation

1. Download the SDK from here.
2. Import the AAR file of the SDK as a module

## Setup the SDK

To use the SDK, you need to import it and call the `setup` function with the server ID and source ID to specify the location of the data collection API endpoint. Here's an example of the code:

```kotlin
package com.example.testapp

import android.app.Application
import com.insightech.datacord.DatacordSDK

class MyApp : Application() {

    override fun onCreate() {
        super.onCreate()
        DatacordSDK.setup(context = this, server = "server_id", sourceId = "source_id")
    }
}
```

Upon initialization, the `setup` function not only automatically collects the `app_start` event but also assigns a `device_id` and `session_id`. These identifiers are then linked to all subsequent events to ensure consistent tracking throughout the session

## Track Screen Views

Track screen views by invoking `trackView` within the `onResume` method of your activities:

```kotlin
class ExampleActivity : AppCompatActivity() {
	...
	override fun onResume() {
		super.onResume()
		DatacordSDK.trackView(viewName = "screen_name")
	}
}
```

## Track Custom Events

The `track` function allows you to capture custom event data, which is particularly useful for monitoring user interactions. These custom events are automatically linked to the most recent screen view, sharing the same `view_id` for cohesive tracking. Here's how you can implement this in your code:

```kotlin
DatacordSDK.track(event = "event_name", data = mapOf("prop1" to "val1", "prop2" to "val2"))
```

## User Identification

The `trackView` and `track` functions can optionally include a user ID as a parameter when the user has been identified. This allows events to be associated with specific users. Here’s are a couple of examples of how to implement this:

```kotlin
DatacordSDK.trackView(viewName = "screen_name", userId = "user_id_123")

```

```kotlin
DatacordSDK.track(event = "event_name", data = mapOf("prop1" to "val1", "prop2" to "val2"), userId = "user_id_123")
```

You can also identify users by triggering a `user_identified` event. This method directly associates user IDs with subsequent data collection, streamlining user tracking. Here's an example of how to code this:

```kotlin
DatacordSDK.track(event = "user_identified", data = mapOf("user_id" to "user_id_123"))
```

Once a user is identified, there's no need to include the user ID in every event. The user ID will be linked to the device ID, allowing all subsequent events from that device to be automatically associated with the identified user.

## Event Batching

By default, events are immediately transmitted once functions are called. However, if you prefer batching events for later transmission, you can enable queuing by setting the `queueData` parameter to `true` when using the `track` and `trackView` functions. Here's how you can implement this:

```kotlin
DatacordSDK.track(event = "event_name", data = mapOf("prop1" to "val1", "prop2" to "val2"), queueData = true)
```

Please note that queuing events for later transmission does not alter their timestamps. Each event will retain the timestamp from the moment it was originally created.