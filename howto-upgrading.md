---
copyright:
  years: 2020, 2025
lastupdated: "2025-06-05"

keyowrds: rabbitmq, upgrading, major versions, changing versions, rabbitmq upgrading, new deployment, major version

subcollection: messages-for-rabbitmq

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading to a new Major Version
{: #upgrading}

When a major version of a database is at its end of life (EOL), it is a good idea to upgrade to a current major version.

Find the available versions of RabbitMQ on the [{{site.data.keyword.messages-for-rabbitmq_full}} catalog](https://cloud.ibm.com/databases/messages-for-rabbitmq/create?catalog_query){: external} page, from the {{site.data.keyword.databases-for}} CLI plug-in command [`ibmcloud cdb deployables-show`](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#deployables-show), or through the {{site.data.keyword.databases-for}} API [`/deployables` endpoint](https://cloud.ibm.com/apidocs/cloud-databases-api#get-all-deployable-databases).

Upgrade your new deployment by [restoring a backup](/docs/cloud-databases?topic=cloud-databases-dashboard-backups) of your data into the new version. Restoring from a backup has a number of advantages:

- The original deployment continues running and production work can be uninterrupted.
- You can test the new database out of production and act on any application incompatibilities.
- The entire process can be rerun at any point.
- A fresh restoration reduces the likelihood that unneeded artifacts of the older version are carried over to the new deployment.

Alternatively, you can also use RabbitMQ Shovel to migrate to another version.

If you get warning messages, such as 'Deprecated features are being used' or 'All stable feature flags must be enabled after completing an upgrade' in the RabbitMQ Management UI, no action is needed during a version upgrade, and you can continue with backup and restore to the next supported version. Do not enable experimental or unstable features introduced in the versions, as those are not supported. Open a support ticket before enabling any feature flag.
{: .important}

If you get the warning message "Deprecated features are being used" in the RabbitMQ Management UI, adopt newly introduced [stable features](https://www.rabbitmq.com/docs/feature-flags#list-of-feature-flags).
{: .tip}

## Upgrading in the UI
{: #upgrading-ui}
{: ui}

Upgrade to a new version when [restoring a backup](/docs/cloud-databases?topic=cloud-databases-dashboard-backups) from the _Backups_ tab of your _Deployment Overview_. Click **Restore** on a backup to bring up a dialog box where you can choose options for the new deployment. One of the configurable options is the database version, which is auto-populated with the versions available for you to upgrade to. Select a version and click **Restore** to start the provision and restore process.


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
    "parameters": {
      "backup_id": "crn:v1:bluemix:public:messages-for-rabbitmq:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:backup:06392e97-df90-46d8-98e8-cb67e9e0a8e6",
    "version":3.9
    }
  }'
```
{: pre}

## Upgrade using RabbitMQ Shovel
{: #upgrading-shovel}

You can use a shovel to move messages from a current cluster to a new cluster during a RabbitMQ version upgrade. For more information, see [RabbitMQ Shovel](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-rabbitmq-shovel){: external}.


## Upgrading from v3.13 to v4
{: #upgrading-ui-v313-to-v4}

There are [major changes](https://cloud.ibm.com/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-rabbitmq-relnotes&interface=ui#messages-for-rabbitmq-18mar2025) between v3.x and v4.x. To upgrade your {{site.data.keyword.messages-for-rabbitmq}} instance from v3.13 to v4, perform the following extra step of deleting the high availability related policies before performing Backup-Restore.

Starting from v4, {{site.data.keyword.messages-for-rabbitmq}} does not support high availability of Classic Queues, hence, when you try to import definitions from v3.13 to v4, the restore fails because the definitions contain Classic Queue high availability related policies that are not recognized by the policy setting.

To avoid this error and to have a successful upgrade, perform the following steps.

1. Log in to the UI of the v3.13 instance.
2. Navigate to the **Policies** side panel in the *Admin* tab.
3. Delete the **ha-all** policy in *Policies* tab.
4. After deletion of the policy, [take an on-demand backup](/docs/cloud-databases?topic=cloud-databases-dashboard-backups&interface=cli#ondemand-backup) of this instance from the IBM Cloud UI.
5. Upon successful backup creation, restore this particular backup to the v4 instance by following [these steps](/docs/cloud-databases?topic=cloud-databases-dashboard-backups&interface=ui#restore-backup).

## Troubleshooting
{: #upgrading-ts}

If you encounter errors while importing definitions during an upgrade {{site.data.keyword.messages-for-rabbitmq}} , see [Why can't I import definitions from Messages for RabbitMQ version 3.9 to version 3.11?](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-troubleshoot-defs){: external}.
