---

copyright:
  years: 2018, 2024
lastupdated: "2024-11-15"

keywords: messages-for-rabbitmq release notes

subcollection: messages-for-rabbitmq

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes
{: #rabbitmq-relnotes}

Use these release notes to learn about the latest updates to {{site.data.keyword.messages-for-rabbitmq_full}} that are grouped by _date_ or _build number_.
{: shortdesc}

## 15 November 2024
{: #messages-for-rabbitmq-15nov2024}
{: release-note}

{{site.data.keyword.databases-for}} logs and events are now available on {{site.data.keyword.logs_full}}
: {{site.data.keyword.databases-for}} has onboarded {{site.data.keyword.logs_full_notm}}, a scalable logging service that persists logs and provides users with capabilities for querying, tailing, and visualizing logs. Customers are expected to use {{site.data.keyword.logs_full_notm}} to review their database logs and events starting **November 15, 2024** as {{site.data.keyword.databases-for}} will not send information to legacy logging systems of _{{site.data.keyword.la_full}}_ and _{{site.data.keyword.at_full}}_ starting **November 15, 2024**. For more information, see [Set up logging and monitoring](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-getting-started-cdb-logging-monitoring) and [About IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-about-cl).

## 29 September 2024
{: #messages-for-rabbitmq-29sept2024}
{: release-note}

{{site.data.keyword.messages-for-rabbitmq}} version 3.12 End of Life on April 30, 2025
:  Action is required before April 30, 2025, for your RabbitMQ 3.12 deployments. After April 30, 2025, {{site.data.keyword.messages-for-rabbitmq}} instances on version 3.12 that are still active will have their access removed, in line with our database versioning policy. You are expected to be on version 3.13, the latest version of {{site.data.keyword.messages-for-rabbitmq}}. For more information, see [Upgrading to a new major version](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-upgrading).

## 16 September 2024
{: #databases-for-rabbitmq-16sept2024}
{: release-note}

Private endpoints as new default
:  To ensure best possible security for your databases, private endpoints are now the default in the {{site.data.keyword.cloud}} console. CLI and Terraform now require the endpoint type to be provided as part of creating an instance.

## 12 August 2024
{: #databases-for-rabbitmq-12aug2024}
{: release-note}

RabbitMQ v3.13 is live
: RabbitMQ v3.13 is available on {{site.data.keyword.messages-for-rabbitmq}}. It includes several new features, bug fixes, and optimizations, such as the following:
  - [MQTT QoS 0 queue type](https://www.rabbitmq.com/docs/mqtt#qos0-queue-type){: external} is available to be used if specific criteria is met.
  - [Overload protect](https://www.rabbitmq.com/docs/mqtt#overload-protection){: external} against high [memory usage](https://www.rabbitmq.com/docs/memory-use){: external} due to MQTT QoS 0 messages.
  - Deprecated features are now listed via https API on RabbitMQ Management UI and a warning is logged upon their usage.
  - Visibility of enabled feature flags via https API and RabbitMQ management UI for administrator users.

## 1 May 2024
{: #databases-for-rabbitmq-01may2024}
{: release-note}

New hosting models
:  You can choose between two hosting models: Isolated Compute and Shared Compute. Isolated Compute is a secure single-tenant offering for complex, highly performant enterprise workloads. Shared Compute is a flexible multi-tenant offering for dynamic, fine-tuned, and decoupled capacity selections. For more information, see [Hosting models](/docs/cloud-databases?topic=cloud-databases-hosting-types){: external}.

## 12 February 2024
{: #messages-for-rabbitmq-12feb2024}
{: release-note}

{{site.data.keyword.messages-for-rabbitmq}} Streams Available
:  RabbitMQ Streams is a persistent replicated data structure that functions similarly to queues, buffering messages from producers for consumption by consumers.
For more information, see [RabbitMQ Streams](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-rabbitmq-streams){: external}.

## 19 January 2024
{: #messages-for-rabbitmq-19jan2024}
{: release-note}

{{site.data.keyword.messages-for-rabbitmq}} version 3.11 End of Life on July 24, 2024
:  Action is required before July 24, 2024, for your RabbitMQ 3.11 deployments. After July 24, 2024, {{site.data.keyword.messages-for-rabbitmq}} instances on version 3.11 that are still active will have their access removed, in line with our Database Versioning Policy. You are expected to be on version 3.12, the latest preferred version of {{site.data.keyword.messages-for-rabbitmq}}.
For more information, see [Upgrading to a new Major Version](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-upgrading){: external}.

## 20 December 2023
{: #messages-for-rabbitmq-20dec2023}
{: release-note}

{{site.data.keyword.messages-for-rabbitmq}} Version 3.12 [Preferred](/docs/cloud-databases?topic=cloud-databases-versioning-policy#version-tags){: external} Release
:  For more information about provisioning a {{site.data.keyword.messages-for-rabbitmq}} instance, see [Provisioning](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-provisioning){: external}.

## 27 November 2023
{: #messages-for-rabbitmq-27nov2023}
{: release-note}

Monitoring Integration documentation updated
:  Monitoring Integration documentation now lists metrics for all {{site.data.keyword.databases-for}} services. For more information, see [Monitoring Integration](/docs/cloud-databases?topic=cloud-databases-monitoring){: external}.

## 08 November 2023
{: #messages-for-rabbitmq-08nov2023}
{: release-note}

{{site.data.keyword.messages-for-rabbitmq}} Version 3.12 [Preview](/docs/cloud-databases?topic=cloud-databases-versioning-policy#version-tags){: external} Release
:  Version 3.12 is released as a Preview. Features in this release:
   - [Optimizations](https://blog.rabbitmq.com/posts/2023/05/rabbitmq-3.12-performance-improvements/){: external} for both quorum and classic queues: improved throughput, lower throughput variability, lower latency, lower memory footprint.
   -  More mature and efficient implementation of (nonmirrored) classic queues v2 (CQv2).
   - Classic queue lazy and non-lazy modes no longer apply: classic queues v2 always behave similarly to the lazy mode in earlier release series: moving data to disk aggressively and only keeping a subset of data in memory.
   - Significantly [reduced MQTT and Web MQTT memory footprint per connection](https://blog.rabbitmq.com/posts/2023/03/native-mqtt/){: external}.
   - [RabbitMQ Shovel](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-rabbitmq-shovel){: external} plug-in now requires to have `verify_none` configured.

For more information, see [RabbitMQ 3.12 Release Notes](https://github.com/rabbitmq/rabbitmq-server/releases/tag/v3.12.0){: external}.

For more information about provisioning a {{site.data.keyword.messages-for-rabbitmq}} instance, see [Provisioning](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-provisioning){: external}.

## 06 November 2023
{: #messages-for-rabbitmq-06nov2023}
{: release-note}

RabbitMQ Shovel Documentation Added
:  Shovel is a plug-in for RabbitMQ that enables you to define replication relationships between brokers. For more information, see [RabbitMQ Shovel](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-rabbitmq-shovel){: external}.

RabbitMQ Streams is now available for {{site.data.keyword.messages-for-rabbitmq}}. RabbitMQ Streams is similar to queues, but differs in how messages are stored and consumed. Streams are effective for large fan-outs, high throughput scenarios, and large logs. For more information, see [RabbitMQ's Streams]{https://www.rabbitmq.com/streams.html}{: external}.

## 01 September 2023
{: #messages-for-rabbitmq-01sept2023}
{: release-note}

RabbitMQ Streams now available

:  RabbitMQ Streams is now available for {{site.data.keyword.messages-for-rabbitmq}}. RabbitMQ Streams is similar to queues, but differs in how messages are stored and consumed. Streams are effective for large fan-outs, high throughput scenarios, and large logs. For more information, see [RabbitMQ's Streams](https://www.rabbitmq.com/streams.html){: external}.

## 29 August 2023
{: #messages-for-rabbitmq-29aug2023}
{: release-note}

Definition Troubleshooting Documentation Added
:  [RabbitMQ definitions](https://www.rabbitmq.com/definitions.html){: external} are metadata that RabbitMQ stores about its cluster. This metadata includes information about users, vhosts, queues, exchanges, bindings, and runtime parameters. Definitions can be used to restore a cluster or migrate to a new cluster. An error while importing definitions can be due to invalid imported arguments being imported from {{site.data.keyword.messages-for-rabbitmq}} 3.9 to version 3.11. For more information, see [Why can't I import definitions from {{site.data.keyword.messages-for-rabbitmq}} version 3.9 to version 3.11?](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-troubleshoot-defs).

## 20 July 2023
{: #messages-for-rabbitmq-20jul2023}
{: release-note}

{{site.data.keyword.messages-for-rabbitmq}} version 3.9 End of Life on September 21, 2023
:  On September 21, 2023 {{site.data.keyword.messages-for-rabbitmq}} version 3.9 reaches its end of life. On that date, all {{site.data.keyword.messages-for-rabbitmq}} instances on version 3.9 that are still active will have their access removed, in line with our [Database Versioning Policy](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-versioning-policy){: external}. You are expected to be on version 3.11, the latest preferred version of {{site.data.keyword.messages-for-rabbitmq}}. If needed, [upgrade](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-upgrading) your database instances.

## 23 May 2023
{: #messages-for-rabbitmq-23may2023}
{: release-note}

Setting up disk alerts for disk utilization tutorial
:  In this tutorial, you use the {{site.data.keyword.cloud_notm}} API and the [{{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started){: external} to set up an alert that emails you whenever the disk utilization of your database exceeds 90%. This specific example creates an alert on a {{site.data.keyword.databases-for-elasticsearch}} deployment, but it is applicable to all the databases in the IBM {{site.data.keyword.databases-for}} catalog. For more information, see [Setting up disk alerts for disk utilization](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-disk-util-alert-tutorial).

## 09 March 2023
{: #messages-for-rabbitmq-09mar2023}
{: release-note}

RabbitMQ Version 3.11 Release
:  {{site.data.keyword.messages-for-rabbitmq_full}} version 3.11 is now available. With this release, messages that are delivered by a quorum queue and negatively acknowledged with a requeue are added to the back of the queue until the queue has redelivery limit set. With a redelivery limit, requeueing uses the original position of the message, if possible. With this update, if you get stuck or requeue deliveries at a high rate, you do not indefinitely grow the quorum queue Raft log, potentially driving the node out of disk space. If the original behavior is important to keep, ensure your applications' quorum queues have a redelivery limit set. This is a **potentially breaking change**. For more information, see [Upgrading to a new Major Version](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-upgrading).

Unmirrored Classic Queues Handling Change
:  With the release of version 3.11, unmirrored classic queue handling is changed. If a node was to be shut down during maintenance, an unmirrored classic queue was automatically moved to another node. With version 3.11, this behavior is changed to match the documented RabbitMQ behavior. An unmirrored classic transient queue is deleted and an unmirrored classic durable queue is unavailable during that time. For more information, see RabbitMQ's [Classic Queue Mirroring](https://www.rabbitmq.com/ha.html#non-mirrored-queue-behavior-on-node-failure).{: external}

`idle_since` field now uses RFC 3339 format
:  The `idle_since` field now uses RFC 3339 format. Here is a sample value with the previous format: `2022-03-22 11:39:37`. Here is a sample value with the new format: `2022-03-22T11:39:37.908+01:00`.

## 19 October 2022
{: #messages-for-rabbitmq-19oct2022}
{: release-note}

Deploying and Connecting a Cloud Databases Instance Tutorial
:  This tutorial guides you through the process of deploying a {{site.data.keyword.databases-for}} instance and connecting it to a web front end by creating a webpage that allows visitors to input a word and its definition. These values are then stored in a database running on {{site.data.keyword.databases-for}}. You install the database infrastructure by using Terraform and your web application uses the popular Express framework. The application can then be run locally, or by using Docker. For more information, see [Deploying and Connecting a {{site.data.keyword.databases-for}} Instance](/docs/messages-for-rabbitmq?topic=cloud-databases-create-instance-tutorial).

## 11 October 2022
{: #messages-for-rabbitmq-11oct2022}
{: release-note}

Protecting {{site.data.keyword.messages-for-rabbitmq_full}} resources with context-based restrictions
:  Context-based restrictions (CBR) give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to {{site.data.keyword.databases-for}} resources can be controlled with CBR and identity and access management (IAM) policies. For more information, see [Protecting Cloud Databases resources with context-based restrictions](/docs/messages-for-rabbitmq?topic=cloud-databases-cbr&interface=ui).

## 25 January 2022
{: #messages-for-rabbitmq-25jan2022}
{: release-note}

{{site.data.keyword.messages-for-rabbitmq_full}} 3.8 End of Life in July 2022
:  On July 12, 2022, Messages for RabbitMQ version 3.8 reaches its end of life. See blog post announcement [here](https://www.ibm.com/cloud/blog/announcements/messages-for-rabbitmq-38-end-of-life-in-july-2022).

## 30 June 2021
{: #messages-for-rabbitmq-30jun2021}
{: release-note}

General Availability of {{site.data.keyword.messages-for-rabbitmq_full}} support for IBM Cloud Databases enabled by IBM Cloud Satellite.
:  A distributed cloud provides consistent security and services across environments, centralized workload visibility, reduced latency, easier compliance and higher application development velocity. See blog post announcement [here](https://www.ibm.com/cloud/blog/announcements/deploy-managed-cloud-native-databases-anywhere-with-ibm-cloud-satellite).

## 21 July 2020
{: #messages-for-rabbitmq-21jul2020}
{: release-note}

IBM Cloud Messages for RabbitMQ 3.8 is Now Preferred
:  RabbitMQ 3.8 Preferred status. See blog post announcement [here](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-messages-for-rabbitmq-38-is-now-preferred).

## 13 April 2020
{: #messages-for-rabbitmq-13apr2020}
{: release-note}

{{site.data.keyword.messages-for-rabbitmq_full}} autoscaling
:  We are excited to announce that autoscaling of your deployments based on disk capacity and disk I/O utilization is now available for {{site.data.keyword.messages-for-rabbitmq_full}} via the UI, API, and CLI. See blog post announcement [here](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-databases-portfolio-introduces-autoscaling).

## 6 August 2019
{: #messages-for-rabbitmq-06aug2019}
{: release-note}

New Regions Available for IBM Cloud Database Services
:  {{site.data.keyword.messages-for-rabbitmq_full}} is now available to be deployed in Seoul; South Korea; and Chennai, India. See blog post announcement [here](https://www.ibm.com/cloud/blog/announcements/new-regions-available-for-ibm-cloud-database-services).

## 19 December 2018
{: #messages-for-rabbitmq-19dec2018}
{: release-note}

General Availability of {{site.data.keyword.messages-for-rabbitmq_full}}
:  {{site.data.keyword.messages-for-rabbitmq_full}} added to the [IBM Cloud Databases](https://www.ibm.com/cloud/databases) family. See blog post announcement [here](https://www.ibm.com/cloud/blog/ibm-cloud-databases-for-etcd-elasticsearch-and-messages-for-rabbitmq-are-now-generally-available).
