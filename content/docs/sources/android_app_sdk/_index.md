---
title: "Android App SDK"
linkTitle: "Android App SDK"
weight: 30
description: >
  
---
To collect data from your Android native app, you need to implement the Kotlin SDK for Android.

## Create the source

Go to the user interface and create a new source using the **Android App SDK**. The source will be assigned a unique ID that will be used to identify it for data collection.

## Installation

1. Download the SDK from [here].
2. Import the AAR file of the SDK as a module

## Setup the SDK

To use the SDK, you need to import it and call the `setup` function with the server ID and source ID to specify the location of the data collection API endpoint. Here's an example of the code:

```kotlin
package com.example.testapp

import android.app.Application
import com.insightech.dataroo.DatarooSDK

class MyApp : Application() {

    override fun onCreate() {
        super.onCreate()
        DatarooSDK.setup(context = this, server = "server_id", sourceId = "source_id")
    }
}

```

The `setup` function will automatically collect the `app_start` event and set the `device_id` and `session_id`, which will be associated with all subsequent events.

## Collect screen view event data

To track a screen view event when a screen is loaded, use the following code with the screen name:

```kotlin
DatarooSDK.trackView(viewName = "screen_name")
```

The `trackView` function is typically called within the `onRsume` event. For example:

```kotlin
class ExampleActivity : AppCompatActivity() {
	...
	override fun onResume() {
		super.onResume()
		DatarooSDK.trackView(viewName = "screen_name")
	}
}
```

## Collect custom event data

You can collect custom event data using the `track` function. Custom event data can be used to track user interactions. The events will be automatically attached to the latest screen view event and share the same `view_id`. Here's an example of the code:

```kotlin
DatarooSDK.track(event = "event_name", data = mapOf("prop1" to "val1", "prop2" to "val2"))
```

## Identify the user

The `trackView` and `track` functions can take the user ID as an input parameter if the user is identified. For example:

```kotlin
DatarooSDK.trackView(viewName = "screen_name", userId = "user_id_123")

```

```kotlin
DatarooSDK.track(event = "event_name", data = mapOf("prop1" to "val1", "prop2" to "val2"), userId = "user_id_123")
```

Another way to identify the user is by using the specific event `user_identified`. Here's an example of the code:

```kotlin
DatarooSDK.track(event = "user_identified", data = mapOf("user_id" to "user_id_123"))
```

There is no need to send the user ID in every event because once the user is identified, the user ID will be associated with the device ID and all events from the device will be automatically associated with the user.

## Queue the events

By default, events are sent immediately when the functions are called. However, if you don't want to send the events immediately, you can put them into a queue and send them in a batch. To do this, set the `queueData` parameter to `true` when calling the `track` and `trackView` functions. Here's an example of the code:

```kotlin
DatarooSDK.track(event = "event_name", data = mapOf("prop1" to "val1", "prop2" to "val2"), queueData = true)
```

Please note that queuing the events won't affect the timestamps of the events. The events will still have the original timestamps when they were created.