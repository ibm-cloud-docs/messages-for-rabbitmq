---
copyright:
  years: 2023, 2026
lastupdated: "2026-10-20"

keyowrds: rabbitmq, shovel

subcollection: messages-for-rabbitmq

---

{{site.data.keyword.attribute-definition-list}}

# RabbitMQ Shovel
{: #rabbitmq-shovel}

Shovel is a plug-in for RabbitMQ that enables you to define replication relationships between brokers.

## Prerequisite
{: #rabbitmq-shovel-prereqs}

Before you configure Shovel, make sure that you create a user with `admin` permission on both formations. For more information, see [Managing Users and Permissions](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-user-management){: external}.

## Configuring RabbitMQ Shovel in the console
{: #rabbitmq-shovel-config}
{: ui}

Create your Shovel on the destination formation. In RabbitMQ versions 3.12 and newer, it is mandatory to add `verify_none` in the source and destination URI, as detailed in the configuration procedure.

Follow these steps to configure RabbitMQ Shovel:

1. Log in to the [RabbitMQ Management UI](https://www.rabbitmq.com/management.html){: external} and select the **Admin** tab.
1. Select *Shovel Management* from the list.
1. Add a new shovel with the following information, then click *Add shovel*:
   - **Name**: test-shovel
   - **Source**: AMQP 0.9.1
     - *URI*: `amqps://username:password@<source_hostname>:<source_port>?verify=verify_none`
     - *Queue_name*: `source_queue`
   - **Destination**: AMQP 0.9.1
     - *URI*: `amqps://username:password@<target_hostname>:<target_port>?verify=verify_none`
     - *Queue_name*: `target_queue`
1. Review the details to verify that the shovel is created correctly.
1. To verify Shovel status, select *Shovel status*.
1. Now you can add a message to your source queue and it will redirect to the destination queue.

Replication relationships between brokers can be created within same region or cross-region.
{: .tip}

## Configuring RabbitMQ Shovel by using the API
{: #rabbitmq-shovel-config-api}
{: api}

Create your Shovel on the destination formation. In RabbitMQ versions 3.12 and newer, it is mandatory to add `verify=verify_none` in the source and destination URI, as detailed in the configuration procedure.

Follow these steps to configure RabbitMQ Shovel by using the API:

1. Obtain the source and destination RabbitMQ connection details, including the host name, port, administrator username and password, source queue name, and destination queue name.
2. Run the following API request to create a shovel:

    ```sh
    curl -v \
      --cacert <ca_cert_path> \
      -u <admin_username>:<admin_password> \
      -X PUT "https://<http_host>:<http_port>/api/parameters/shovel/%2F/<shovel_name>" \
      -H "content-type: application/json" \
      -d @- << EOF
    {
      "component": "shovel",
      "name": "shovel_name",
      "value": {
        "src-protocol": "amqp091",
        "src-uri": "amqps://<username>:<password>@<amqps_host>:<amqps_port>?verify=verify_none",
        "src-queue": "src_queue",
        "dest-protocol": "amqp091",
        "dest-uri": "amqps://<username>:<password>@<amqps_host>:<amqps_port>?verify=verify_none",
        "dest-queue": "dest_queue",
        "add-forward-headers": false,
        "ack-mode": "on-publish",
        "delete-after": "never"
      }
    }
    ```
    {: pre}

1. Review the API response to verify that the shovel was created successfully.
1. Verify the shovel configuration from the RabbitMQ Management UI under **Admin** > **Shovel Management**.
1. To verify shovel operation, publish a message to the source queue and confirm that it is forwarded to the destination queue.

The parameters `add-forward-headers`, `ack-mode`, and `delete-after´ are optional. If they are not specified, RabbitMQ uses the default values. For more information about available configuration options, see the [RabbitMQ Shovel documentation](https://www.rabbitmq.com/docs/shovel-dynamic#amqp091-reference).
{: note}

## Configuring RabbitMQ Shovel by using the CLI
{: #rabbitmq-shovel-config-cli}
{: cli}

Create your Shovel on the destination formation. In RabbitMQ versions 3.12 and newer, it is mandatory to add -´verify=verify_none` in the source and destination URI, as detailed in the configuration procedure.

Follow these steps to configure RabbitMQ Shovel by using the CLI:

1. Obtain the source and destination RabbitMQ connection details, including the host name, port, administrator username and password, source queue name, and destination queue name.

Run the following command to create a shovel:

    ```sh
    rabbitmqadmin shovels declare_amqp091 --name my-shovel \
        --source-uri "amqps://<username>:<password>@<amqps_host>:<amqps_host>?verify=verify_none" \
        --destination-uri "amqps://<username>:<password>@<amqps_host>:<amqps_host>?verify=verify_none" \
        --source-queue "source-queue" \
        --destination-queue "dest-queue"
    ```
    {: pre}

1. Verify that the command completes successfully.
1. Verify the shovel configuration from the RabbitMQ Management UI under **Admin** > **Shovel Management**.
1. To verify shovel operation, publish a message to the source queue and confirm that it is forwarded to the destination queue.

The CLI example shows only the required parameters. For more information about available configuration options, see the [RabbitMQ Shovel documentation](https://www.rabbitmq.com/docs/shovel-dynamic#amqp091-reference).
{: note}
