---
copyright:
  years: 2017,2018
lastupdated: "2018-10-26"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting an external application
{: #connecting-external-app}

Your applications and drivers use connection strings to make a connection to {{site.data.keyword.messages-for-rabbitmq_full}}. Each deployment has connection strings specifically for drivers and applications. 

## Getting Connection Strings

The easiest way to get connection strings for an application is to create a set of _Service Credentials_ specifically for your application to connect with. Doing so also returns all the connection information as JSON in a click-to-copy field.

Alternatively, the {{site.data.keyword.cloud_notm}} CLI [cloud databases plug-in](./howto-getting-connection-strings.html#generating-connection-strings-from-the-command-line) supports generating users and connection strings, as does the [{{site.data.keyword.IBM_notm}} {{site.data.keyword.databases-for}} API](https://console.{DomainName}/apidocs/cloud-databases-api#creates-a-database-level-user).

Full documentation on generating and retrieving connection strings is on the [Getting Connection Strings](./howto-getting-connection-strings.html) page.

## Connecting with a language's driver

All the information a driver needs to make a connection to your deployment is in the "rabbitmq" section of your connection strings. The table contains a breakdown for reference.

Table is a work in progress

Many RabbitMQ drivers will be able to make a connection to your deployment when given the URI-formatted connection string found in the "composed" field of the connection information. For example, `sample connection string goes here`

The table covers a few of the common RabbitMQ drivers.

Language|Driver|Documentation
----------|-----------
Node|`ampqlib`|[Link](https://www.npmjs.com/package/amqplib)
Java|RabbitMQ Java Client Library|[Link](http://www.rabbitmq.com/java-client.html)
Ruby|`Bunny`|[Link](http://rubybunny.info/)
Python|`pika`|[Link](https://pika.readthedocs.io/en/0.10.0/index.html)
{: caption="Table 2. Common Elasticsearch drivers" caption-side="top"}

## Driver TLS and self-signed certificate support

All connections to {{site.data.keyword.messages-for-rabbitmq}} are TLS 1.2 enabled, so the driver you use to connect needs to be able to support encryption. Your deployment also comes with a self-signed certificate so the driver can verify the server upon connection. 

### Using the self-signed certificate

1. Copy the certificate information from the Base64 field of the connection information. 
2. Decode the Base64 string into text and save it to a file. (You can use the Name that is provided or your own file name).
3. Provide the path to the driver.

### CLI plug-in support for the self-signed certificate

You can display the decoded certificate for your deployment with the CLI plug-in with the command `ibmcloud cdb deployment-cacert "your-service-name"`. It decodes the base64 into text. Copy and save the command's output to a file and provide the file's path to the driver.






 
