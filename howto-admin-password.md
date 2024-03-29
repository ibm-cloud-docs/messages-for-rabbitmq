---
copyright:
  years: 2017, 2023
lastupdated: "2023-04-27"

keywords: rabbitmq, rabbitmq admin password

subcollection: messages-for-rabbitmq

---

{{site.data.keyword.attribute-definition-list}}

# Setting the Admin Password
{: #admin-password}

The {{site.data.keyword.messages-for-rabbitmq_full}} service is provisioned with an admin user.

You must set the admin password before you can use it to connect. To set the password through the {{site.data.keyword.cloud_notm}} dashboard, select _Manage_ from the service dashboard to open the management panel for your service. Open the _Settings_ tab, and use the _Change Database Admin Password_ panel to set a new admin password.

![The Change Database Admin Password Panel in Settings](images/settings-admin-password.png){: caption="Figure 1. The Change Database Admin Password Panel in _Settings_" caption-side="bottom"}

## Setting the admin password through the CLI
{: #setting-password-cli}
{: cli}

Use the `cdb user-password` command from the [{{site.data.keyword.databases-for}} CLI plug-in](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference) to set the admin password with the command line.

For example, to set the admin password for a deployment named "example-deployment", use the following command.
```sh
ibmcloud cdb user-password example-deployment admin <newpassword>
```

## Setting the admin password via the API
{: #setting-password-api}
{: api}

The _Foundation Endpoint_ that is shown on the _Overview_ panel of your service provides the base URL to access this deployment through the API. Use it with the `/deployments/{id}/users/{username}` endpoint to set the admin password.

```sh
curl -X PATCH `https://api.{region}.databases.cloud.ibm.com/v4/ibm/deployments/{id}/users/admin' \
-H "Authorization: Bearer $APIKEY" \
-H "Content-Type: application/json" \
-d '{"password":"newrootpasswordsupersecure21"}'
```

For more information, see the [API Reference](https://{DomainName}/apidocs/cloud-databases-api#set-database-level-user-s-password).
