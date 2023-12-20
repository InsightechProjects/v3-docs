---
title: "BigQuery Destination"
linkTitle: "BigQuery Destination"
weight: 10
description: >
  
---
BigQuery is a fully managed, serverless data warehouse that enables scalable analysis over petabytes of data. As a destination, it can store data and allow you to perform data analytics tasks and create dashboards in popular BI tools such as Looker Studio, PowerBI, Tableau, etc.

## Create Google Cloud Platform (GCP) service account

To stream data into BigQuery, create a GCP service account and its access key. Follow these steps:

1. Create a service account by following the instructions [here](https://cloud.google.com/iam/docs/service-accounts-create).
2. Assign the **BigQuery Data Owner** role to the account.
3. Create a key for the service account and download the JSON key file using the instructions [here](https://cloud.google.com/iam/docs/keys-create-delete#creating).

## Create BigQuery dataset

Create a new BigQuery dataset in the GCP project where you created the service account.

## Create BigQuery destination

Go to the user interface and create a **BigQuery** destination. In the destination settings, copy and paste the content of the service account key JSON file into the **GCP Service Account Key (JSON)** field. Set the GCP project name and dataset name. These settings will allow the system to create tables and views, and stream data into them.

The system will create an `events` table with `local_date` as the day partition field. It is important to set the correct timezone for the destination to ensure events are partitioned correctly.

## Configure the events

The system creates two tables: `events` and `users`. The `events` table contains all the streamed events, while the `users` table contains the relationship between the `identifier` and the first-party `user_id`.

For each event type, the system creates a view once the event is streamed to the destination. For example, the `pageview` view contains all `pageview` events consolidated by `user_id`. If a user has used two devices to browse your website and they are identified on both devices, the `pageview` table will have the same `user_id` attached to the `pageview` events on both devices.

In the system user interface, click on the BigQuery destination to view all the events that are streamed to your BigQuery dataset. The `events` table allows 50 custom variable slots. Click the **Update** button of an event to manage the variables. You can enable and disable variables, change their data types, and the mapping slot. Please note that not all variables sent with the event are enabled by default. You can toggle the setting to **Show All** to see and manage the disabled variables.