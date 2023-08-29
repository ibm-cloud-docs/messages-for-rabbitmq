---
copyright:
  years: 2020, 2023
lastupdated: "2023-08-29"

keyowrds: rabbitmq, upgrading, major versions, changing versions, rabbitmq upgrading

subcollection: messages-for-rabbitmq

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading to a new Major Version
{: #upgrading}

When a major version of a database is at its end of life (EOL), it is a good idea to upgrade to a current major version. 

Find the available versions of RabbitMQ on the [{{site.data.keyword.messages-for-rabbitmq_full}} the catalog](https://cloud.ibm.com/catalog/messages-for-rabbitmq){: external} page, from the {{site.data.keyword.databases-for}} CLI plug-in command [`ibmcloud cdb deployables-show`](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#deployables-show), or through the {{site.data.keyword.databases-for}} API [`/deployables` endpoint](https://cloud.ibm.com/apidocs/cloud-databases-api#get-all-deployable-databases).

Upgrade your new deployment by [restoring a backup](/docs/messages-for-rabbitmq?topic=cloud-databases-dashboard-backups#restoring-a-backup) of your data into the new version. Restoring from a backup has a number of advantages:

- The original deployment continues running and production work can be uninterrupted.
- You can test the new database out of production and act on any application incompatibilities.
- The entire process can be rerun at any point.
- A fresh restoration reduces the likelihood that unneeded artifacts of the older version are carried over to the new deployment.

## Upgrading in the UI
{: #upgrading-ui}
{: ui}

Upgrade to a new version when [restoring a backup](/docs/messages-for-rabbitmq?topic=cloud-databases-dashboard-backups#restoring-a-backup) from the _Backups_ tab of your _Deployment Overview_. Click **Restore** on a backup to bring up a dialog box where you can choose options for the new deployment. One of the configurable options is the database version, which is auto-populated with the versions available for you to upgrade to. Select a version and click **Restore** to start the provision and restore process.

## Upgrading through the CLI
{: #upgrading-cli}
{: cli}

To upgrade and restore from backup through the CLI, use the [ibmcloud resource service-instance-create](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command:

```sh
ibmcloud resource service-instance-create <service-name> <service-id> <service-plan-id> <region>
```
{: pre}

The parameters `service-name`, `service-id`, `service-plan-id`, and `region` are all required. You also supply the `-p` with the version and backup ID parameters in a JSON object. If you need to use a key protect key, resize the deployment, or allocate dedicated cores, you can do so with the optional parameters `key_protect_key`, `members_disk_allocation_mb`, `members_memory_allocation_mb`, or `members_cpu_allocation_count`, along with their respective values to the body of the request:

```sh
ibmcloud resource service-instance-create example-upgrade messages-for-rabbitmq standard us-south \
-p '{"backup_id": "crn:v1:bluemix:public:messages-for-rabbitmq:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:backup:06392e97-df90-46d8-98e8-cb67e9e0a8e6", "version":3.8}'
```
{: pre}

## Upgrading through the API
{: #upgrading-api}
{: api}

Complete [the necessary steps to use the resource controller API](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-provisioning&interface=api#provision-controller-api) before you use it to upgrade from a backup. 

Next, send the API a `POST` request. The parameters `name`, `target`, `resource_group`, and `resource_plan_id` are all required. You also supply the `version` and `backup_id`. To use a key protect key, resize the deployment, or allocate dedicated cores, configure the following optional parameters and their values: `key_protect_key`, `members_disk_allocation_mb`, `members_memory_allocation_mb`, or `members_cpu_allocation_count`.

```sh
curl -X POST \
  https://resource-controller.bluemix.net/v2/resource_instances \
  -H 'Authorization: Bearer <>' \
  -H 'Content-Type: application/json' \
    -d '{
    "name": "my-instance",
    "target": "bluemix-us-south",
    "resource_group": "5g9f447903254bb58972a2f3f5a4c711",
    "resource_plan_id": "messages-for-rabbitmq-standard",
    "backup_id": "crn:v1:bluemix:public:messages-for-rabbitmq:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:backup:06392e97-df90-46d8-98e8-cb67e9e0a8e6",
    "version":3.9
  }'
```
{: pre}

## Troubleshooting
{: #upgrading-ts}

If you encounter errors while importing definitions during an upgrade {{site.data.keyword.messages-for-rabbitmq}}, see [Why can't I import definitions from Messages for RabbitMQ version 3.9 to version 3.11?](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-troubleshoot-defs){: external}.
