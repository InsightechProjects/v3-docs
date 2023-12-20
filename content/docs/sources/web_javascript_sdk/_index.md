---
title: "Web JavasScript SDK"
linkTitle: "Web JavasScript SDK"
weight: 10
description: >
  To collect data from websites, implement Web JavaScript SDK on your website pages.
---
To collect data from websites, implement Web JavaScript SDK on your website pages. You can configure the source in the web interface to control the events you want to collect.

## Create the source

Go to the user interface and create a new source using the **Web JavaScript SDK**. The source will be assigned a unique ID that will be used to identify it for data collection and provide you with a snippet of JavaScript code that you can install to your website via tag management systems (TMS) or embed in your web pages directly.

### Domains

### Data Layer Name

## Event types

The SDK automatically tracks the automatic events based on the configurations set in the web interface. It also tracks custom events in data layer objects, including eCommerce events.

### Automatic events:

- `pageview`
This event is triggered automatically when a page is loaded or the URL is changed in single-page applications (SPA).
- `session_start`
This event is triggered automatically when the first `pageview` event is triggered on a new session. A session is defined as a new page view more than 30 minutes after the previous page view or the user comes to the website from an external source.
- `web_click`
This event is triggered automatically when users click on any elements.

## The data layer and custom events

You can define a data layer name such as “dataLayer” in the configurations to collect events in the data layer object. The data layer is a JSON array that you can `push` events into and each pushed event will trigger data collection in the SDK.

For example, the code below collects the user identity with the data layer named `dataLayer`.

```jsx
dataLayer.push({
  'event': 'user_identified',
	'user_id': 'cNBMvhGM3AV7TA4nIbe1eUiLVVT2'
});
```

## eCommerce events

The SDK will automatically collect eCommerce events that follow the [Google Analytics 4](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtag) schema in the data layer. These include the following events:

- view_item_list
This event will generate a `view_product_list` event and one `view_product_list_item` event for each item.
- view_item
This event will generate a `view_product_details` event and one `view_product_details_item` event for each item.
- add_to_cart
This event will generate an `add_to_cart` event and one `add_to_car_item` event for each item.
- begin_checkout
This event will generate a `begin_checkout` event and one `begin_checkout_item` event for each item.
- purchase
This event will generate a `purchase` event and one `purchase_item` event for each item.