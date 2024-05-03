---
title: Datacord Documentation
aliases:
  # Fixes a broken Home Page link from Gallery pages.
  - /_pages/
type: docs
---
Welcome to the Datacord SDK documentation! This resource is your ultimate guide to integrating and leveraging the Datacord SDK across multiple platforms, including iOS, Android, and web applications via JavaScript. Whether you're a developer looking to enhance app functionality with real-time data analytics or a product manager interested in understanding user interactions, our documentation provides all the necessary tools and information to get you started and efficiently use our system.

---

## Get Started with Datacord SDK

### Step 1: Create a Source

A "source" in Datacord acts as the entry point for your data. It defines where and how data is collected within your application. Here's how you can set up a source:

1. **Create a New Source**: Click on ‘Create Source’ and select the platform for which you are integrating, such as iOS, Android, or Web.
2. **Configure Your Source**: Name your source and set up any specific parameters that relate to your data collection needs.
3. **Implement SDK**: Use the provided SDK snippet to implement the source in your application.

See more details about the sources [here](https://docs.datacord.io/docs/sources/).

### Step 2: Send Data to the Source

Once your source is set up, you can start sending data to it. Here’s what you need to do:

1. **Collect Data**: In your application, collect the data you want to send (e.g., user events, interactions).
2. **Format Data**: Ensure your data is in the correct JSON format as specified in the SDK guidelines.
3. **Send Data**: Use the SDK's function to send the formatted data to your designated source.

### Step 3: Create a Destination to Receive the Data

A "destination" is where your data is sent for analysis or further use. Setting up a destination is crucial for making the most of the data collected. Here’s how to create a destination:

1. **Add a New Destination**: Click on ‘Add Destination’. Choose the service you want to use, like BigQuery for data analysis or Pub/Sub for data streaming.
2. **Configure Destination Settings**: Provide necessary configuration details such as credentials and data handling rules.
3. **Link Destination with Source**: Establish a connection between your source and the new destination to start data flow.

See more details about the destinations [here](https://docs.datacord.io/docs/destinations/).

---

By following these steps, you can quickly set up the Datacord SDK and start utilizing powerful data-driven insights to improve your application. For detailed instructions, code snippets, and best practices, explore the specific sections of our documentation tailored to each task. Happy coding!