---
copyright:
  years: 2019, 2022
lastupdated: "2022-04-12"

keywords: rabbitmq, databases, jms, shovel, delayed, stomp, mqtt

subcollection: messages-for-rabbitmq

---

{:external: .external target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Using RabbitMQ plugins
{: #plugins}

RabbitMQ supports various plugins to extend its core functions. {{site.data.keyword.messages-for-rabbitmq_full}} comes with a selection of plugins that are already enabled on your deployment. plugin management is handled by the {{site.data.keyword.messages-for-rabbitmq}} service. Users cannot enable or disable plugins.

## Available {{site.data.keyword.messages-for-rabbitmq}} plugins
{: #plugins-available}

plugin | Name 
-------|-------
[Shovel plugin](#shovel-plugin) | `rabbitmq_shovel` 
[Shovel Management plugin](#delayed-message-plugin)| `rabbitmq_shovel_management`
[Delayed Message plugin](#delayed-message-plugin) | `rabbitmq_delayed_message_exchange`
[STOMP plugin](#stomp-plugin) | `rabbitmq_stomp`
[RabbitMQ Management plugin](#rabbitmq-management-plugin) | `rabbitmq_management`
[JMS plugin](#jms-plugin) | `rabbitmq_jms_topic_exchange`
[MQTT plugin](#mqtt-plugin) | `rabbitmq_mqtt`
{: caption="Table 1. Available RabbitMQ plugins" caption-side="top"}


## Shovel plugin
{: #shovel-plugin}

{{site.data.keyword.messages-for-rabbitmq}} comes with the [Shovel plugin](https://www.rabbitmq.com/shovel.html), `rabbitmq_shovel`, and the [Shovel Management plugin](https://github.com/rabbitmq/rabbitmq-shovel-management), `rabbitmq_shovel_management`, enabled. You can configure the plugin through both the [RabbitMQ Management plugin UI](#rabbitmq-management-plugin) and its accompanying API.

The _Shovel Status_ and _Shovel Management_ links appear under the _Admin_ tab.

![Admin tab with the Shovel plugin](images/plugins-shovel-ui.png){: caption="Figure 1. Admin tab with the Shovel plugin" caption-side="bottom"}

If you do not see the _Admin_ tab, you might need to log in to the management UI with the [admin user](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-admin-password). 
{: .tip}

In the RabbitMQ Management API, the Shovel Management plugin adds endpoints for listing, creating, and deleting shovels. Usage and examples are in the [GitHub repository's documentation](https://github.com/rabbitmq/rabbitmq-shovel-management#usage).

## Delayed Message plugin
{: #delayed-message-plugin}

The [delayed message plugin](https://github.com/rabbitmq/rabbitmq-delayed-message-exchange), `rabbitmq_delayed_message_exchange` is a third-party plugin that adds delayed messaging and scheduled messaging to RabbitMQ. 

To use the plugin, declare an exchange with the type `x-delayed-type`. To delay a message, publish it with the `x-delay` header with the number of milliseconds to delay the message. More detailed usage information is in the [plugin's documentation](https://github.com/rabbitmq/rabbitmq-delayed-message-exchange#usage).

## STOMP plugin
{: #stomp-plugin}

The [RabbitMQ STOMP plugin](https://www.rabbitmq.com/stomp.html), `rabbitmq_stomp`, supports sending [STOMP-formatted](http://stomp.github.io/) messages through RabbitMQ. The plugin enables a port to handle STOMP traffic on your deployment, and it is TLS/SSL secured. The connection information for STOMP clients is in the `stomp_ssl` section of your deployment's [connection strings](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-connection-strings#the-stomp_ssl-section).

## RabbitMQ Management plugin
{: #rabbitmq-management-plugin-info}

The RabbitMQ Management plugin, `rabbitmq_management`, provides access to your deployment through a web browser, `rabbitmqadmin`, and through the RabbitMQ API. For more information on using this information, see the [Connecting with the RabbitMQ Management Plugin](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-rabbitmq-management-plugin) page. 

## JMS plugin
{: #jms-plugin}

The RabbitMQ JMS Topic Exchange plugin, `rabbitmq_jms_topic_exchange`, is enabled by default for {{site.data.keyword.messages-for-rabbitmq}} deployments. This plugin adds server-side support for the [RabbitMQ JMS client](https://github.com/rabbitmq/rabbitmq-jms-client) and supports JMS topic routing plus selection based on JMS SQL selection rules.

The RabbitMQ JMS Client is required to communicate with the plugin. Review the [JMS Client documentation page](https://www.rabbitmq.com/jms-client.html) that is provided by RabbitMQ for more detailed information on installation and configuration, along with examples.

More detailed information about the JMS plugin can also be found in the RabbitMQ JMS Topic Exchange plugin [GitHub repo](https://github.com/rabbitmq/rabbitmq-jms-topic-exchange). 

## MQTT plugin
{: #mqtt-plugin}

The MQTT plugin, `rabbitmq_mqtt`, is enabled by default for {{site.data.keyword.messages-for-rabbitmq}} deployments. Information on using the MQTT plugin is available on the [MQTT Plugin](https://www.rabbitmq.com/mqtt.html) page. 