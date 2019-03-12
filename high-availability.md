---

Copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# High-Availability
{: #high-availability}

{{site.data.keyword.messages-for-rabbitmq_full}} is a managed cloud database service that is fully integrated into the {{site.data.keyword.cloud_notm}} ecosystem. The database, storage, and supporting infrastructure all run in {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.messages-for-rabbitmq}} provides replication, fail-over, and high-availability features to protect your databases and data from infrastructure maintenance, upgrades, and failures. Deployments contain a cluster with three nodes where all three nodes are equal peers. If one data member becomes unreachable, your cluster continues to operate normally.

By contrast, application resilience and connection error handling are the responsibility of the application developer.

## Application-level High-Availability

Applications that communicate over networks and cloud services are subject to transient connection failures. You want to design your applications to retry connections when errors are caused by a temporary loss in connectivity to your deployment or to {{site.data.keyword.cloud_notm}}.

Because {{site.data.keyword.messages-for-rabbitmq}} is a managed service, regular updates and database maintenance occurs as part of normal operations. This can occasionally cause short intervals where your database is unavailable. 

Your applications have to be designed to handle temporary interruptions to the database, implement error handling for failed database commands, and implement retry logic to recover from a temporary interruption.

Several minutes of database unavailability or connection interruption is not expected. Open a [support ticket](https://cloud.ibm.com/unifiedsupport/cases/add) with details if you have time periods longer than a minute with no connectivity so we can investigate.

## Resource Scaling

{{site.data.keyword.messages-for-rabbitmq}} deployments do not auto-scale. Deployment owners can [monitor](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-monitoring) the state of the deployment, estimate typical resource usage, and scale the deployment accordingly.

If you are planning on running operations that might put a spike in the usual RAM usage, or any data operations that could overflow your allotted storage, you can manually scale your service's resources up first to avoid hitting any limits that can affect deployment operations.

## SLA

{{site.data.keyword.messages-for-rabbitmq}} deployments conform to the {{site.data.keyword.cloud_notm}} [SLA terms](/docs/overview?topic=overview-SLAs#SLAs).
