{{{
  "title": "Set Group Horizontal Autoscale Policy",
  "date": "10-20-2015",
  "author": "Johann Tang",
  "attachments": []
}}}

Applies a horizontal autoscale policy to a group. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to apply a horizontal autoscale policy to a group.

## URL

### Structure

    PUT https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/horizontalAutoscalePolicy/

### Example

    PUT https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0/horizontalAutoscalePolicy

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| GroupID | string | ID of the group being queried. Retrieved from query to parent group, or by looking at the URL of the Group in the Control Portal UI. | Yes |

### Content Properties
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| policyId | string | The unique identifier of the autoscale policy | Yes |
| loadBalancerPool | complex | Information about the load balancer | Yes |

### Load Balancer Pool
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| id | string | ID of the load balancer | Yes|
| publicPort | int | Port configured on the public-facing side of the load balancer pool. | Yes |
| privatePort| int | The internal (private) port of the node server | Yes |

### Example
```
{
  "policyId" : "6cf7f7d139ee4d4f98a09bd0400b1a56",
  "loadBalancerPool" :  
  {
    "id" : "bf82320cc96d42048fc7d5e41b0cdada",
    "privatePort" : 80,
    "publicPort" : 80
  }
}
```

## Response
| Name | Type | Description |
| --- | --- | --- |
| groupId | string | ID of the group |
| policyId | string | The unique identifier of the autoscale policy |
| locationId | string | Data center location identifier |
| availableServers | int | The number of servers available for scaling |
| targetSize | int | Number of servers to scale to |
| scaleDirection | string | Direction to Scale (In or Out ) |
| scaleResourceReason | string | Reason for scaling, either: CPU, Memory, MinimumResourceCount, or None |
| loadBalancer | complex | |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this data center |

### Load Balancer Definition
| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the load balancer |
| name | string | Friendly name of the load balancer |
| publicPort | int | Port configured on the public-facing side of the load balancer pool. |
| privatePort| int | The internal (private) port of the node server |
| publicIP | string | The external (public) IP address of the load balancer |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this data center |

### Example
```
{
  "groupId": "fc06fd421e2ee41190460050568600e8",
  "policyId": "6cf7f7d139ee4d4f98a09bd0400b1a56",
  "locationId": "WA1",
  "availableServers": 2,
  "targetSize": 1,
  "scaleDirection": "None",
  "scaleResourceReason": "Cpu",
  "loadBalancer": {
    "id": "bf82320cc96d42048fc7d5e41b0cdada",
    "name": "hotfix111314",
    "publicPort": 80,
    "privatePort": 80,
    "publicIP": "63.251.170.219",
    "links": [
      {
        "rel": "self",
        "href": "/v2/sharedLoadBalancers/ALIAS/WA1/bf82320cc96d42048fc7d5e41b0cdada"
      }
    ]
  },
  "links": [
    {
      "rel": "self",
      "href": "/v2/groups/ALIAS/fc06fd421e2ee41190460050568600e8/horizontalAutoscalePolicy"
    },
    {
      "rel": "group",
      "href": "/v2/groups/ALIAS/fc06fd421e2ee41190460050568600e8"
    },
    {
      "rel": "horizontalAutoscalePolicy",
      "href": "/v2/horizontalAutoscalePolicies/ALIAS/6cf7f7d139ee4d4f98a09bd0400b1a56"
    }
  ]
}
```
