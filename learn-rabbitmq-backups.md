---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-18"

keywords: messages, backups, rabbitmq backups, messages for rabbitmq backups

subcollection: messages-for-rabbitmq

---

{{site.data.keyword.attribute-definition-list}}

# Backups with {{site.data.keyword.messages-for-rabbitmq}} 
{: #backups-for-rabbitmq}

The {{site.data.keyword.messages-for-rabbitmq_full}} backups do not contain the actual messages. Your {{site.data.keyword.messages-for-rabbitmq}} deployment backups contain *only* configuration data.  

For more information on backing up your {{site.data.keyword.messages-for-rabbitmq}} service configurations, see the [Managing backups](/docs/databases-for-mongodb?topic=databases-for-mongodb-dashboard-backups&interface=ui) section of the {{site.data.keyword.cloud}} documentation. 

Review the [management responsibilities and terms and conditions](/docs/databases-for-mongodb?topic=databases-for-mongodb-responsibilities-cloud-databases) that you have when you use {{site.data.keyword.messages-for-rabbitmq}} service.


## Concepts and suggestions 
{: #concepts-suggestions}

The expected operation for a {{site.data.keyword.messages-for-rabbitmq}} deployment is to keep queues short: messages are written and read in a short cycle with focus on throughput. {{site.data.keyword.messages-for-rabbitmq}} deployments are not intended as a data store like other {{site.data.keyword.cloud}} offerings. 

For message delivery with durability and consistent quality of service, you must use [quorum queues](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-rabbitmq-ha-dr#ha-features). 

The [Shovel plug-in](https://www.rabbitmq.com/shovel.html) can also help move messages across instances. While not a backup mechanism, this plug-in can aid in message retention. 

Remember, messages are not part of the {{site.data.keyword.messages-for-rabbitmq}} deployment backups regardless of the queue types or plug-ins implemented. 

For more information, see [high availability and disaster recovery](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-rabbitmq-ha-dr). 
