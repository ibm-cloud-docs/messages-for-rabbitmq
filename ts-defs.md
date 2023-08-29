---

copyright:
  years: 2023
lastupdated: "2023-08-29"

keywords: troubleshooting Messages for RabbitMQ, connectivity, definitions, error importing definitions

subcollection: messages-for-rabbitmq

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I import definitions from {{site.data.keyword.messages-for-rabbitmq}} version 3.9 to version 3.11?
{: #troubleshoot-defs}
{: troubleshoot}
{: support}

If you encounter errors while importing definitions from {{site.data.keyword.messages-for-rabbitmq}} 3.9 to version 3.11, review these common causes and solutions.
{: shortdesc}

You encounter errors while importing definitions from {{site.data.keyword.messages-for-rabbitmq}} 3.9 to version 3.11.
{: tsSymptoms}

[RabbitMQ definitions](https://www.rabbitmq.com/definitions.html){: external} are metadata that RabbitMQ stores about its cluster. This metadata includes information about users, vhosts, queues, exchanges, bindings, and runtime parameters. Definitions can be used to restore a cluster or migrate to a new cluster. An error while importing definitions can be due to invalid imported arguments being imported from {{site.data.keyword.messages-for-rabbitmq}} 3.9 to version 3.11. Review the following information to troubleshoot and resolve common definition problems:
{: tsResolve}

Look into your [logs](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-logging) and search for this line:
 
```sh
Encountered an error when importing definitions
```
{: pre} 

If this error is found, check which argument is causing the issue. Once you have identified the argument causing the issue, correct it and try to import the definition again.

