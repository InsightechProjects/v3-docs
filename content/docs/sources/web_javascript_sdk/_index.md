---
title: "Web JavasScript SDK"
linkTitle: "Web JavasScript SDK"
weight: 10
description: >
---
The Web JavaScript SDK is designed to capture user data from web pages. It automatically records interactions such as page views, clicks, and various events from the data layer. You can tailor data collection settings through the source settings interface.

## Create a Source

To create a new source:

1. Access the user interface.
2. Select the **Web JavaScript SDK** option.
3. Upon creation, you'll receive a unique source ID. This ID is crucial for identifying your source during data collection. You will also be provided with a JavaScript code snippet. You can integrate this snippet into your website either through a Tag Management System (TMS) or by embedding it directly into your web pages.

## Event Types

The SDK captures both automatic and custom events based on your configuration settings:

### Automatic events:

- `pageview`
Triggered automatically when a page loads or the URL changes, as seen in single-page applications (SPA).
- `session_start`
Triggered when the first `pageview` event occurs in a new session. A session is defined as either a new page view occurring more than 30 minutes after the last page view or when a user visits from an external source.
- `web_click`
Triggered when users click on any page elements.

## Install the Web JavaScript SDK

To install the SDK, insert the following script into every webpage. Ensure to replace `source_id` and `server_id` with the appropriate values provided for your source.

```jsx
<script>
!function(){ var async = function(c){ var d = document, s = d.createElement('script'), h = d.getElementsByTagName('head')[0]; s.src = 'https://cdn.datacord.io/datacord.js'; if(c){s.addEventListener('load', function(e){c(null,e);}, false);} h.appendChild(s); }; async(function(){ inst = new _Analytics("source_id","server_id"); }); }();
</script>
```

## Data Layer and Custom Events

Define a data layer name (e.g., `dataLayer`) in your configurations to manage events within this layer. Events pushed to this layer trigger data collection via the SDK.

For instance, to collect user identity information, use the following code:

```jsx
dataLayer.push({
  'event': 'user_identified',
	'user_id': 'cNBMvhGM3AV7TA4nIbe1eUiLVVT2'
});
```

## eCommerce Events

The SDK is configured to automatically handle eCommerce events based on the [Google Analytics](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm) 4 schema. Events include:

- `view_item_list`: Generates a `view_product_list` event and a `view_product_list_item` event for each item.
- `view_item`: Triggers a `view_product_details` event and a `view_product_details_item` event for each listed item.
- `add_to_cart`: Triggers an `add_to_cart` event and an `add_to_cart_item` event for each item added.
- `begin_checkout`: Triggers a `begin_checkout` event and a `begin_checkout_item` event for each item.
- `purchase`: Triggers a `purchase` event and a `purchase_item` event for each item purchased.

This setup allows for detailed tracking of user interactions and behaviors in eCommerce environments.