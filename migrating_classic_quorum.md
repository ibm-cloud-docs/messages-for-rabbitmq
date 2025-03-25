---
copyright:
  years: 2025
lastupdated: "2025-03-25"

keyowrds: migrate, classic, quorum

subcollection: messages-for-rabbitmq

---

{{site.data.keyword.attribute-definition-list}}

# Migrating from Classic Queues to Quorum Queues
{: #migrating_classic_quorum}

Starting {{site.data.keyword.messages-for-rabbitmq_full}} version 4, Mirrored(HA) Classic Queues is [deprecated](https://www.rabbitmq.com/docs/3.13/ha). Customer are requested to use 
Quorum Queues, which was [introduced in RabbitMQ v3.8](https://www.ibm.com/blog/announcement/ibm-cloud-messages-for-rabbitmq-38-is-now-preferred/). You can choose 
one of the following methods during the major version upgrade from v3.13 to v4 of {{site.data.keyword.messages-for-rabbitmq}}.

## Method 1: Moving from Classic to Quorum Queues in the same instance
{: #method1-same-instance}

1. Stop the publishers and subscribers that are connected to the Classic Queue.
2. Create a new temporary quorum queue in the vhost, same as the Classic Queue.
3. Configure a temporary Shovel to move any messages from the old Classic Queue to the new temporary Quorum Queue.
4. After all the messages are moved to the temporary quorum queue, delete the Shovel.
5. Delete the source Classic Queue. Then, recreate a Quorum Queue with the same name and bindings as the source Classic mirrored queue in the same vhost.
6. Create a new Shovel to move the messages from the temporary Quorum Queue to the new Quorum Queue.
7. After all the messages are moved to the new Quorum Queue, delete the Shovel.
8. Restart the publishers and subscribers.

## Method 2: Moving from Classic to Quorum Queues in separate instances
{: #method2-separate-instances}

To perform method 2 using the Shovel plug-in, follow the steps in the [Shovel Plugin documentation](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-rabbitmq-shovel).
