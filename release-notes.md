---

copyright:
  years: 2018, 2023
lastupdated: "2023-05-23"

keywords: messages-for-rabbitmq release notes

subcollection: messages-for-rabbitmq

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.messages-for-rabbitmq_full}}
{: #rabbitmq-relnotes}

Use these release notes to learn about the latest updates to {{site.data.keyword.messages-for-rabbitmq_full}} that are grouped by _date_ or _build number_.
{: shortdesc}

## 23 May 2023
{: #messages-for-rabbitmq-23may2023}
{: release-note}

Setting up disk alerts for disk utilization tutorial
:  In this tutorial, you use the {{site.data.keyword.cloud_notm}} API and the [{{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started){: external} to set up an alert that emails you whenever the disk utilization of your database exceeds 90%. This specific example creates an alert on a {{site.data.keyword.databases-for-elasticsearch}} deployment, but it is applicable to all the databases in the IBM {{site.data.keyword.databases-for}} catalog. For more information, see [Setting up disk alerts for disk utilization](/docs/databases-for-mysql?topic=messages-for-rabbitmq-disk-util-alert-tutorial).

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

{{site.data.keyword.messages-for-rabbitmq_full}} 3.8 End of Life in July  2022
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
