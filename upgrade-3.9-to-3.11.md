---
copyright:
  years: 2018, 2023
lastupdated: "2023-01-27"

keywords: rabbitmq, upgrade, upgrading

subcollection: messages-for-rabbitmq

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading to RabbitMQ version 3.11
{: #rabbitmq-3.11-upgrade}

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla id ligula dignissim, dapibus erat a, dapibus lorem. Nullam quis ante est. Interdum et malesuada fames ac ante ipsum primis in faucibus. Fusce tristique lorem vitae turpis bibendum venenatis. Pellentesque commodo elementum elit, vel commodo nunc tempus cursus. Proin vel venenatis est. Suspendisse aliquet varius volutpat.

## Required Feature Flags
{: #req-feature-flags}

RabbitMQ 3.11.x makes all feature flags introduced during the life of RabbitMQ 3.8.x required. Ensure all feature flags are enabled before attempting to upgrade to 3.11.x. The affected feature flags are:

- `quorum_queue` (support for quorum queues)
- `implicit_default_bindings` (default bindings now implicit, instead of being stored in the database, to speed up the creation of queues and exchanges)
- `virtual_host_metadata` (ability to add metadata to virtual host metadata; description, tags, etc)
- `maintenance_mode_status` (ability to switch RabbitMQ to a maintenance mode)
- `user_limits` (ability to configure the connection and channel limits for a user)

If you initially created clusters using RabbitMQ 3.8.9 or older, enable all feature flags before upgrading to RabbitMQ 3.11. If the feature flags are not enabled, RabbitMQ 3.11.0+ will refuse to start.{: important}

Nodes now default to 65536 concurrent client connections (This is just for Linux Distributions such as RHEL 9 and CentOS Stream 9) ← This is important is base UBI images is changed.

## Feature Flag Analysis
{: #feature-flag-analysis}

Currently enabled feature flags on 3.9.12

- `implicit_default_bindings`
- `maintenance_mode_status`
- `quorum_queue`
- `virtual_host_metadata`

Required feature flags for 3.11

- `quorum_queue` (support for quorum queues)
- `implicit_default_bindings` (default bindings now implicit, instead of being stored in the database, to speed up creation of queues and exchanges)
- `virtual_host_metadata` (ability to add metadata to virtual host metadata; description, tags, etc)
- `maintenance_mode_status` (ability to switch RabbitMQ to a maintenance mode)
- `user_limits` (ability to configure connection and channel limits for a user)

[Reference](https://blog.rabbitmq.com/posts/2022/07/required-feature-flags-in-rabbitmq-3.11/)

Feature Flags for 3.11

We have an overlap of the feature flags we have already introduced with the required feature flags and we will only have to add one additional feature flag to run on 3.11:

- `quorum_queue` (support for quorum queues)
- `implicit_default_bindings` (default bindings now implicit, instead of being stored in the database, to speed up creation of queues and exchanges)
- `virtual_host_metadata` (ability to add metadata to virtual host metadata; description, tags, etc)
- `maintenance_mode_status` (ability to switch RabbitMQ to a maintenance mode)
- `user_limits` (ability to configure connection and channel limits for a user)
- `classic_mirrored_queue_version` Support setting version for classic mirrored queues
- `classic_queue_type_delivery_support` Bug fix for classic queue deliveries using mixed versions (https://github.com/rabbitmq/rabbitmq-server/issues/5931 - needs to be enabled when
   `classic_queue_type_delivery_support` is enabled, otherwise we see crashing queues)
- `direct_exchange_routing_v2`: direct exchange routing implementation
- `drop_unroutable_metric`: Count unroutable publishes to be dropped in stats
- `empty_basic_get_metric`: Count AMQP basic.get on empty queues in stats
- `feature_flags_v2`: Feature flags subsystem V2
- `listener_records_in_ets`: Store listener records in ETS instead of Mnesia
- `tracking_records_in_ets`: Store tracking records in ETS instead of Mnesia

Feature flags we will not introduce

- `stream queues` (still requires more test to be introduced: #27635): Support queues of type stream
- `stream_single_active_consumer` Single active consumer for streams

## Release Notes
{: #req-feature-flags}

For more information, see [RabbitMQ 3.11.7 Release Notes](https://github.com/rabbitmq/rabbitmq-server/releases?page=1).
