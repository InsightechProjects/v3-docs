---
title: "Pub/Sub"
linkTitle: "Pub/Sub"
weight: 20
description: >
---
Google Pub/Sub is a messaging service provided by Google Cloud that supports asynchronous communication between applications. It operates using topics and subscriptions, where messages published to a topic are received by all subscribers of that topic.

Pub/Sub is designed for reliability and scalability, making it ideal for applications involving real-time analytics, event-driven architectures, and decoupled microservices.

## Create a Google Cloud Platform (GCP) service account

To stream data into BigQuery, create a GCP service account and its access key. Follow these steps:

1. **Create a Google Cloud Project** using the guide provided [here](https://cloud.google.com/resource-manager/docs/creating-managing-projects).
2. **Create a Service Account:** Start by creating a service account following the detailed instructions [here](https://cloud.google.com/iam/docs/service-accounts-create).
3. **Assign Roles:** Assign the **Pub/Sub Publisher** role to the newly created service account to grant it the necessary permissions.
4. **Generate and Download Key:** Create a key for the service account and download the JSON key file as instructed [here](https://cloud.google.com/iam/docs/keys-create-delete#creating).

## Create Pub/Sub topic(s)

You can configure PubSub to handle events in two distinct ways:

1. **Single Topic Mode:** Stream all events to a single Pub/Sub topic. 
2. **Event-Specific Topic Mode:** Stream events to different topics based on the event type. For instance, `pageview` events might be streamed to a “pageview” topic, while `web_click` events go to a “web_click” topic.

Choose the mode that best fits your needs and create the necessary topics accordingly. For the event-specific mode, you can configure the schema to map variables from the event data.

## Create a Pub/Sub Destination

To configure a Pub/Sub destination within your project, proceed to the user interface and enter the necessary information in the destination settings:

- **Destination Name:** Provide a name for your destination to identify it within your system.
- **GCP Service Account Key (JSON):** Insert the contents of your service account's JSON key file. This key enables the destination to authenticate and interact with your GCP services.
- **Pub/Sub GCP Project ID:** Type in the Project ID of the GCP project that hosts your Pub/Sub topics.
- **Pub/Sub Topic Mode:** Select whether to use a single Pub/Sub topic for all event types or a separate topic for each event type.
- **Pub/Sub Topic:** If you opt for a single topic, specify the name of this Pub/Sub topic.

## Managing Event Type Streaming

Within the destination user interface, you will find a list of all event types that are set up to stream to Pub/Sub. Each event type has an “Update” button that allows you to enable or disable streaming for that specific event. This feature provides control over which event types are actively streamed to your Pub/Sub topics, enabling you to manage data flow efficiently.