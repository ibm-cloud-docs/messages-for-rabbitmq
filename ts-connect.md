---

copyright:
  years: 2020, 2024
lastupdated: "2024-12-18"

keywords: troubleshooting Messages for RabbitMQ, failure to connect, intermittent connection timeout, unable to connect

subcollection: messages-for-rabbitmq

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can’t I connect to my {{site.data.keyword.messages-for-rabbitmq_full}} deployment?
{: #troubleshoot-connect}
{: troubleshoot}
{: support}

If you encounter errors when connecting to your {{site.data.keyword.messages-for-rabbitmq_full}} deployment, review these common causes and solutions.
{: shortdesc}

You receive an error message or fail to connect to a {{site.data.keyword.messages-for-rabbitmq}} deployment. When reviewing application logs, you might see errors that mention intermittent connection timeouts or unable to connect.
{: tsSymptoms}

Review the following information to troubleshoot and resolve common connectivity problems:
{: tsResolve}

* An unsecured connection is a common cause of connectivity errors.  All {{site.data.keyword.messages-for-rabbitmq}} connections use TLS/SSL encryption. {{site.data.keyword.messages-for-rabbitmq}} rejects unsecured connections. To avoid errors, make sure you configured a secure connection. For more information, see [Getting Started](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-getting-started).
* If you are using a private endpoint, make sure that you specify connection strings that contain the [Private Endpoint](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-service-endpoints&interface=ui#private-endpoints-credentials) and that you followed the steps in [Connecting through Private Endpoints](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-service-endpoints&interface=ui#private-endpoint-connections).
* If your application log captures a short connection interruption, that behavior is expected as a normal part of operations for this managed service. Design your applications to retry connections when errors are caused by a temporary loss in connectivity to your deployment or to {{site.data.keyword.cloud_notm}}. 
* If retrying your connection hasn't worked, reestablish your connection. If a connection has closed, retrying will have no effect. 
* If you experience several minutes of connection interruption, check the Cloud Status for the service. For more information, see [Application-level High-Availability](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-high-availability#high-availability-for-your-application).
