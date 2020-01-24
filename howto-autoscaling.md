---

Copyright:
  years: 2020
lastupdated: "2020-01-13"

keywords: rabbitmq, databases, autoscaling, disk I/O, memory

subcollection: messages-for-rabbitmq

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Autoscaling
{: #autoscaling}

Autoscaling is designed to respond to the short-to-medium term trends in resource usage on your {{site.data.keyword.messages-for-rabbitmq_full}} deployment. When enabled, your deployment is checked at the interval you specify. If it is running short on resources, more resources are added to the deployment. To keep an eye on your resources, use the [Monitoring integration](/docs/services/messages-for-rabbitmq?topic=cloud-databases-monitoring), which provides metrics for memory, disk space, and disk I/O utilization.

You can set your deployment to autoscale disk, RAM, or both. 

General Autoscaling parameters
- When to scale, based on usage over a period of time
- by how much to scale, as a percentage of the resources per member
- how often to scale, measured either in seconds, minutes, or hours
- hard limit on scaling

![Example Autoscaling panel](images/autoscaling-panel.png)

Memory - Memory autoscaling is based on Disk I/O utilization in order to provide more memory for disk caching as your read/write load increases. The benefit is that additional memory might alleviate pressure on disk I/O by supporting more caching. Autoscaling configurations based on memory usage are currently not available. 

Disk - Disk autoscaling can scale when either disk usage reaches a certain threshold, Disk I/O utilization reach a certain threshold, or both. (If looking at the "or" in the UI, it operates as an `inclusive or`, `|`, `v`.) The amount of IOPS available to your deployment increases with disk size at a ratio of 10 IOPS for each GB.

The resource numbers refer to each database node in a deployment. For example, there are three members in a RabbitMQ cluster and if the deployment is scaled with 10GB of disk and 1GB of RAM, that means each member gets 10GB of disk and 1GB of RAM. The total resources added to your deployment is 30GB of disk and 3GB of RAM.

Limits 
- can't set anything to scale in an interval less than 60 seconds.
- Maximum Disk = 4 TB per member
- Maximum RAM = 112 GB per member

Autoscaling does not scale down deployments where disk or memory usage has shrunk. The RAM provisioned to your deployment remains for your future needs, or until you scale down your deployment manually. The disk provisioned to your deployment remains because disk can not be scaled down. 
{: .tip}

## Configuring Autoscaling in the UI

The Autoscaling panel is on the _Resources_ tab of your deployment's _Manage_ page. To enable scaling, fill in your desired parameters. Then, check the boxes to enable the parameters you are using. Be sure to click **Save Changes** for your configuration to be saved and your changes to take affect.

To disable autoscaling, uncheck the boxes for the parameters that you no longer want to use. If you uncheck all the boxes, autoscaling is disabled. Click **Save Changes** to save the configuration.

## Configuring Autoscaling in the API

You can get the autoscaling parameters for your deployment through the API by sending a `GET` request to the [`/deployments/{id}/groups/{group_id}/autoscaling`]() endpoint. 
```
curl -X GET -H "Authorization: Bearer $APIKEY" 'https://api.{region}.databases.cloud.ibm.com/v4/ibm/deployments/{id}/groups/member/autoscaling'
```

To enable and set the autoscaling parameters for your deployment through the API, send a `POST` request to the endpoint.
```
curl -X PATCH https://api.{region}.databases.cloud.ibm.com/v4/ibm/deployments/{id}/groups/member/autoscaling -H 'Authorization: Bearer <>' 
-H 'Content-Type: application/json' 
-d '{"autoscaling": {
      "memory": {
        "scalers": {
          "io_utilization": {
            "enabled": true, 
            "over_period": "5m",
            "above_percent": 90}
          },
          "limits": {
            "scale_increase_percent": 10.0,
            "scale_period_seconds": 30,
            "scale_maximum_mb": 125952,
            "units": "mb"
          }
      }
    }'
```
To disable autoscaling, send the PATCH request with the currently enabled scalers set to `false`. If all of them are set to `false`, then autoscaling is disabled on your deployment.