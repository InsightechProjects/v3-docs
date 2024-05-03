---
title: "BigQuery"
linkTitle: "BigQuery"
weight: 10
description: >
  
---
BigQuery is a fully managed, serverless data warehouse from Google Cloud Platform (GCP). It efficiently manages scalable analysis of petabytes of data and integrates with popular Business Intelligence (BI) tools such as Looker Studio, PowerBI, and Tableau for advanced data visualization.

## Setup BigQuery and Service Account in Google Cloud Platform (GCP)

To utilize BigQuery for streaming data, you must set up a GCP service account and configure it properly. Follow these steps to get started:

1. **Create a Google Cloud Project** using the guide provided [here](https://cloud.google.com/resource-manager/docs/creating-managing-projects).
2. **Create a BigQuery dataset** within your project by following the steps [here](https://cloud.google.com/bigquery/docs/datasets).
3. **Create a service account** with detailed steps available [here](https://cloud.google.com/iam/docs/service-accounts-create).
4. **Assign the BigQuery Data Admin role** to your new service account to grant it necessary permissions.
5. **Generate and download a JSON key** for the service account, as instructed [here](https://cloud.google.com/iam/docs/keys-create-delete#creating). This key will be used in subsequent steps.

## Creating a BigQuery Destination

To set up a destination for your data within BigQuery:

- **Destination Name:** Enter a name for your destination.
- **GCP Service Account Key (JSON):** Paste the content of your service account's JSON key file.
- **BigQuery GCP Project ID:** Enter the Project ID where your BigQuery dataset is hosted.
- **BigQuery Dataset:** Specify the name of the dataset.
- **Data Partition Timezone:** Choose a timezone for daily data partitioning. Note: This cannot be changed once the destination is established.

Upon creation, the system will automatically generate `events` and `users` tables within your dataset and maintain a separate view for each type of event.

## Mapping Event Properties

In the BigQuery destination, you have the flexibility to manage various event types. Each event type, such as `pageview`, has its dedicated view that contains all relevant events. These views are named according to their event type and include properties specific to those events — for instance, the `pageview` view will include properties like URL and page title.

The views also feature an `identifier` field, which captures the first-party user identifier that you collect from your data sources. For more in-depth information on how user identities are handled, please refer to our document on Identifying Users.

Within the user interface, you can control the streaming of events to your database. By accessing the event update button, you can easily enable or disable specific event types. If you wish to stream a particular property to BigQuery, simply set its **Status** to “Enabled,” choose an appropriate data type and a data slot for it. Once these settings are saved, the system will automatically update the BigQuery views of the event type by adding the enabled properties or 
removing the disabled ones. This process is fully automated, eliminating the need for manual maintenance or updates of the views.