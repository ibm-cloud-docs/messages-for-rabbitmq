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
{:tip: .tip}


# Getting Connection Strings

In order to connect to {{site.data.keyword.messages-for-rabbitmq_full}}, you need database users and some connection strings. A {{site.data.keyword.messages-for-rabbitmq}} deployment is provisioned with an admin user, and after [setting the admin password](./howto-admin-password), you can use its connection strings to connect to your deployment.

The simplest way to retrieve connection information is from the [cloud databases plug-in](./howto-using-ibmcloud-cli.html). Use the `ibmcloud cdb deployment-connections` command to display a formatted connection URI for any user on your deployment. For example, to retrieve a connection string for the admin user on a deployment named  "example-rabbit", use the following command.

```
ibmcloud cdb deployment-connections example-rabbit -u admin
```
Or
```
ibmcloud cdb cxn example-rabbit -u admin
```

## Generating Connection Strings for additional users

Access to your {{site.data.keyword.messages-for-rabbitmq}} deployment is not just limited to the admin user. You may create additional users and retrieve connection strings specific to them by using the _Service Credentials_ panel, the {site.data.keyword.IBM_notm}} CLI, or through the {{site.data.keyword.IBM_notm}} {{site.data.keyword.databases-for}} API. 

## Generating Connection Strings from _Service Credentials_

1. Navigate to the service dashboard for your service.
2. Click _Service Credentials_ to open the _Service Credentials_ panel.
3. Click **New Credential**.
4. Choose a descriptive name for your new credential. 
5. Click **Add** to provision the new credentials. A username and password, and an associated RabbitMQ user is auto-generated.

The new credentials appear in the table, and the connection strings are available as JSON in a click-to-copy field under _View Credentials_.

### Using Service IDs

Because {{site.data.keyword.messages-for-rabbitmq}} is an IAM service, you can use [Service IDs](https://console.{DomainName}/docs/iam/serviceid.html#serviceids) to manage access to this service. For example, by using an IAM-managed Service ID, that user gets an RabbitMQ user and connection string in _Service Credentials_, and has API key access to the {{site.data.keyword.cloud_notm}} Databases API.  If you have a Service ID, enter its information under _Select Service ID_.

## Generating Connection Strings from the command line

If you manage your service through the {{site.data.keyword.cloud_notm}} CLI and the cloud databases plug-in, you can generate a new user and connection strings with `cdb user-create`. For example, to create a new user for a deployment named "example-deployment", use the following command.

`ibmcloud cdb user-create example-deployment <newusername> <newpassword>`

The response contains the task `ID`, `Deployment ID`, `Description`, `Created At`, `Status`, and `Progress Percentage` fields. The `Status` and `Progress Percentage` fields update when the task is complete.

Once the task has finished, you can retrieve the new user's connection strings with the `ibmcloud cdb deployment-connections` command.

```
ibmcloud cdb deployment-connections example-deployment -u <newusername>
```
Or
```
ibmcloud cdb cxn example-deployment -u <newusername>
```

Full connection information is returned by the `ibmcloud cdb deployment-connections` command with the `--all` flag. To retrieve all the connection information for a deployment named  "example-deployment", use the following command.

```
ibmcloud cdb deployment-connections example-deployment -u <newusername> --all
```

If you don't specify a user, the `deployment-connections` commands return information for the admin user by default.
{: .tip}

### Generating _Service Credentials_ for existing users.

Creating a new user from the CLI doesn't automatically populate that user's connection strings into _Service Credentials_. If you want to add them there, you can create a new credential with the existing user information.

Enter the user name and password in the JSON field _Add Inline Configuration Parameters_, or specify a file where the JSON information is stored. For example, `{"existing_credentials":{"username":"Robert","password":"supersecure"}}`.

Generating credentials from an existing user does not check for or create that user.
{: tip}

## Connection String Breakdown

This is a work in progress.

## Generating Connection Strings via API

The _Foundation Endpoint_ that is shown on the _Overview_ panel of your service provides the base URL to access this deployment through the API. To create and manage users, use the base URL with the `/users` endpoint. Examples and documentation is available in the [API Reference](https://console.{DomainName}/apidocs/cloud-databases-api#creates-a-database-level-user).

To retrieve user's connection strings, use the base URL with the `/users/{userid}/connections` endpoint. Examples and documentation is also available in the [API Reference](https://console.{DomainName}/apidocs/cloud-databases-api#discover-connection-information-for-a-deployment-f-b7f6f4).







