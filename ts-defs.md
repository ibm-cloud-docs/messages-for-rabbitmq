---

copyright:
  years: 2023, 2026
lastupdated: "2026-03-30"

keywords: troubleshooting Messages for RabbitMQ, connectivity, definitions, error importing definitions

subcollection: messages-for-rabbitmq

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I import definitions between {{site.data.keyword.messages-for-rabbitmq}} versions?
{: #troubleshoot-defs}
{: troubleshoot}
{: support}

If you encounter errors while importing definitions between {{site.data.keyword.messages-for-rabbitmq}} versions, review these common causes and solutions.
{: shortdesc}

You encounter errors while importing definitions between {{site.data.keyword.messages-for-rabbitmq}} versions.
{: tsSymptoms}

[RabbitMQ definitions](https://www.rabbitmq.com/definitions.html){: external} are metadata that RabbitMQ stores about its cluster. This metadata includes information about users, vhosts, queues, exchanges, bindings, and runtime parameters. Definitions can be used to restore a cluster or migrate to a new cluster. An error while importing definitions can be due to invalid imported arguments being imported from {{site.data.keyword.messages-for-rabbitmq}} versions. Review the following information to troubleshoot and resolve common definition problems:
{: tsResolve}

Look into your [logs](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-logging) and search for this line:
 
```sh
Encountered an error when importing definitions
```
{: pre} 

If this error is found, check which argument is causing the issue. Once you have identified the argument causing the issue, correct it and try to import the definition again.

How can I restore the backup if my instances has temporary or server named queues?
{: tsSymptoms}

Users will encounter an errors while restoring with temporary queues. RabbitMQ can creates temporary queues if those are not declared. These queues start with prefix "amq.gen-". These temporary queues are exported in the definition of the backup, and are tried to be restored. However, RabbitMQ does not allow temporary queue definitions to be imported, which will fail the restore when exchange binding is created.
For a successful restore(import) of the backup, users **must** remove the temporary queues from their instances before they create a backup(export).

Note: RabbitMQ allows you to export and import definitions, which are configurations for exchanges, users, permissions, and non-transient queues.

Read more about temporary of server named queues [here](https://www.rabbitmq.com/docs/queues#server-named-queues){: external}.
{: tsResolve}
