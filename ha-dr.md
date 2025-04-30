---

copyright:
  years: 2025
lastupdated: "2025-04-30"

keywords: HA for rabbitmq, DR for rabbitmq, rabbitmq recovery time objective, rabbitmq recovery point objective

subcollection: messages-for-rabbitmq

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability and disaster recovery for {{site.data.keyword.messages-for-rabbitmq}}
{: #rabbitmq-ha-dr}

[High availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible in the presence of unexpected failures. [Disaster recovery](#x2113280){: term} is the process of recovering the service instance to a working state.
{: shortdesc}

{{site.data.keyword.messages-for-rabbitmq}} is a highly available regional service designed for availability during a regional outage. {{site.data.keyword.messages-for-rabbitmq}} is designed to meet the [Service Level Objectives (SLO)](/docs/resiliency?topic=resiliency-slo) with the Standard plan.

For more information about the available region and data center locations, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

## High availability architecture
{: #ha-architecture}

![Architecture](images/RabbitMQ_HA1.drawio.svg){: caption="RabbitMQ architecture" caption-side="bottom"}

### High availability features
{: #ha-features}

{{site.data.keyword.messages-for-rabbitmq}} supports the following high availability features:



| Feature | Description | Consideration |
| -------------- | -------------- | -------------- |
| Automatic failover | Standard on all clusters and resilient against a zone or single member failure. |  |
| Member count | 3 member deployment. It is resilient to the failure of one member during the same failure period. | |
| Queue selection | Mirror Classic Queue and Quorum Queue ensure messages durability and fast fail-over.  | Select the correct queue type. |
{: caption="HA features for {{site.data.keyword.messages-for-rabbitmq}}" caption-side="bottom"}

## Disaster recovery architecture
{: #disaster-recovery-intro}

The general strategy for disaster recovery is to create a new {{site.data.keyword.messages-for-rabbitmq}} instance using the backup, and restore it to same or another region.

![Disaster recovery architecture](images/RabbitMQ_DR1.drawio.svg){: caption="RabbitMQ disaster recovery architecture" caption-side="bottom"}

### Disaster recovery features
{: #dr-features}

{{site.data.keyword.messages-for-rabbitmq}} supports the following disaster recovery features:

| Feature | Description | Consideration |
| -------------- | -------------- | -------------- |
| Backup restore | Create a new instance from previously created backup; see [Managing Cloud Databases backups](https://cloud.ibm.com/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-dashboard-backups&interface=ui#restore-backup). | New connection strings for the restored instance must be referenced throughout the workload. Only definitions are backup <--- clarify!!!> |
| Shovel | Asynchronous message routing that enables you to define replication between brokers across clusters. | Configure it within the same region or cross-region. |
{: caption="DR features for {{site.data.keyword.messages-for-rabbitmq}}" caption-side="bottom"}

### Planning for DR
{: #features-for-disaster-recovery}

The DR steps must be practiced regularly. As you build your plan, consider the following failure scenarios and resolutions.



| Failure | Resolution |
| -------------- | -------------- |
| Hardware failure (single point) | (Example) {{site.data.keyword.IBM_notm}} provides a database that is resilient from single point of hardware failure within a zone. No customer configuration is required. |
| Zone failure | The {{site.data.keyword.messages-for-rabbitmq}} members are distributed between zones. Three members provide additional resiliency to multiple zone failures. |
| Data corruption | Selection of durable queue type ensures that messages are intact. |
| Regional failure | Backup restore. Use the restored instance in production. `/n  /n` Shovel. Replicate messages cross region. |
{: caption="DR scenarios for {{site.data.keyword.messages-for-rabbitmq}}" caption-side="bottom"}

### Connection limits
{: #connection-limits}

Is it important to prevent overwhelming your deployment with connections. If the number of connections to the database exceeds the connection limit, new connections fail and return an error. {{site.data.keyword.messages-for-rabbitmq}} connections limits are listed [here](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-high-availability&interface=ui#rabbitmq-connection-limits).

## Your responsibilities for HA and DR
{: #feature-responsibilities}



It is your responsibility to continuously test your plan for HA and DR.

Interruptions in network connectivity and short periods of unavailability of a service might occur. It is your responsibility to make sure that application source code includes [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha) to maintain high availability of the application.
{: note}

The following information can help you create and continuously practice your plan for HA and DR.

When restoring from backups, a new instance is created with new connection strings. Existing workloads and processes must be adjusted to consume the new connection strings.

A recovered database may also need the same customer-created dependencies of the disaster database - make sure these and other services exist in the recovered region:

   - IBM® Key Protect for IBM Cloud®
   - Hyper Protect Crypto Services

Remember that deleting an instance also deletes its associated backups. However, deleted instance may be recoverable within a limited timeframe. For more information, see the [Backups FAQ](/docs/cloud-databases?topic=cloud-databases-faq-backups).

It is not possible to copy backups off the IBM Cloud, so consider using the service-specific tools for additional backups. It may be required to recover from malicious database deletion followed by a reclamation-delete of a database. Careful management of IAM access to databases can help reduce exposure to this problem.

The following checklist associated with each feature can help you create and practice your plan.

- Backup restore
   - Verify that backups are available at the desired frequency to meet RPO requirements. Manage Cloud Databases backups documents backup frequency. Consider a script using IBM Cloud® Code Engine - Working with the Periodic timer (cron) event producer to create additional on-demand backups to improve RPO if the criticality and size of the database allow. However, given RabbitMQ's PITR capabilities, carefully evaluate the need for additional backups.
   - There are some restrictions on database restore regions - verify your restore goals can be achieved by reading managing Cloud Databases backups.
   - Verify the retention period of the backups meet your requirements.
   - Schedule test restores regularly to verify that the actual restored times meet the defined RTO. Remember that database size significantly impacts restore time. Please consider strategies to minimize restore times, such as breaking down large databases into smaller, more manageable units and purging unused data.
   - Verify the Key Protect service.

To find out more about responsibility ownership between the customer and IBM Cloud for using {{site.data.keyword.messages-for-rabbitmq}}, see [Shared responsibilities for Cloud Databases](/docs/cloud-databases?topic=cloud-databases-responsibilities-cloud-databases).
