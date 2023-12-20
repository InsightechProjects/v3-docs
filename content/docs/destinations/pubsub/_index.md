---
title: "PubSub Destination"
linkTitle: "PubSub Destination"
weight: 20
description: >
  
---
Google PubSub is a messaging service provided by Google Cloud. It enables asynchronous communication between applications using topics and subscriptions. Subscribers who have subscribed to a topic can receive messages published to that topic.

PubSub offers reliable and scalable messaging, making it suitable for various use cases such as real-time analytics, event-driven architectures, and decoupled microservices.

## Create a Google Cloud Platform (GCP) service account

To stream data into BigQuery, create a GCP service account and its access key. Follow these steps:

1. Create a service account by following the instructions [here](https://cloud.google.com/iam/docs/service-accounts-create).
2. Assign the **Pub/Sub Publisher** role to the account.
3. Create a key for the service account and download the JSON key file using the instructions [here](https://cloud.google.com/iam/docs/keys-create-delete#creating).

## Create PubSub topic(s)

The PubSub destination supports two modes:

1. Streaming all events to a single PubSub topic.
2. Streaming events to a topic named after the event type. For example, all `pageview` events will be streamed to the `events` topic, while all `web_click` events will be streamed to the `web_click` topic.

Depending on the mode you choose, create the necessary topic name(s). For the second mode, which is specific to each event type, you can set up the schema to map the variables of the event's data.

## Create PubSub destination

Go to the user interface and create a *Pub/Sub* destination. In the destination settings, copy and paste the content of the service account key JSON file into the **GCP Service Account Key (JSON)** field. Set the GCP project name. These settings allow the system to send the events to your Pub/Sub topics.