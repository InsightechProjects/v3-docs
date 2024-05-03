---
title: "Identifying Users and Omni-Channel Journeys"
linkTitle: "Identifying Users and Omni-Channel Journeys"
weight: 10
description: >
---
Associating user identifiers with devices enables linking of both subsequent and, in certain cases, previous anonymous events to individual users. Once a user identifier is linked to a device, all further actions from that device are attributed to the user until the identifier is removed or the device identifier changes.

In BigQuery destinations, events that occur before a user is identified are also retrospectively attributed to that user. This allows for comprehensive insights into the user's interactions, including which marketing channels they engaged with before being identified.

## Identifying Users

You can send a user identifier to the system using two methods:

- Include the user identifier in the `user_id` field of any event. For example:

```json
{
	"event_id": "a6dc1d73b531c706d125688dc437c23f",
	"event": "banner_view",
	"user_id": "user_123",
	"device_id": "device_abc",
	"timestamp": 1683363983423,
	"data": {
		"banner_name": "winter_promotion",
		"banner_type": "promotion"
	}
}
```

- Use the `user_identified` event to send the identifier:

```json
{
	"event_id": "a6dc1d73b531c706d125688dc437c23f",
	"event": "user_identified",
	"device_id": "device_abc",
	"timestamp": 1683363983423,
	"data": {
		"user_id": "user_123"
	}
}
```

After processing these events, all subsequent interactions from the device will be linked to the user until either a `user_revoked` event is sent or the `device_id` is changed.

## Retroactive User Identifying

For BigQuery destinations, the system not only links all subsequent events to the identified user, but also retroactively associates all previous anonymous events with them. This retroactive linking updates the `identifier` field in event views after the user is identified.

## Omni-Channel Journeys

Identifying users across multiple sources or devices enables the integration of data via the `identifier` field in BigQuery views, forming comprehensive omni-channel journeys. For instance, in a SaaS business, by correlating marketing channels with user registrations and subsequent subscription payments, it is possible to analyze the revenue generated from each marketing channel.