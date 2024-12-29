# List Clusters

### Get Cluster <a href="#hca43983mpiv" id="hca43983mpiv"></a>

**Description:** Retrieve a list of clusters configured by the user, optionally returning the associated nodes for each cluster based on user input.

**Security:** Admin

**Usage:** `GET /runtime/api/v1/clusters/{id}`

**Consumes:** `application/json`

**Produces:** `application/json`

#### Request body <a href="#d928slqmiyka" id="d928slqmiyka"></a>

| Name       | Type   | Required/Optional | Description                                                                          |
| ---------- | ------ | ----------------- | ------------------------------------------------------------------------------------ |
| `limit`    | int    | Required          | Maximum number of clusters to return per request. Default is \`100\`. (Range: 1-100) |
| `next_key` | string | Optional          | ID from the previous request, empty on the first request                             |
| i`d`       | int    | Optional          | If ID passed, limit is 1, and returns info about clusters                            |

#### Response body <a href="#id-52825iys1ugq" id="id-52825iys1ugq"></a>

| Name          | Type               | Description                                                   |
| ------------- | ------------------ | ------------------------------------------------------------- |
| `total_count` | int                | The total number of clusters that match the filter query.     |
| `pagination`  | paginationObj      | Pagination info for the request                               |
| `clusters`    | Array\[clusterObj] | A list of cluster objects containing details of each cluster. |
|               |                    |                                                               |

**paginationObj:**

| Name       | Type   | Description                                              |
| ---------- | ------ | -------------------------------------------------------- |
| `limit`    | int    | Key-based pagination - number of rows per request        |
| `next_key` | string | Id from the previous request, empty on the first request |

**clusterObj:**

| Name                            | Type              | Description                                                                        |
| ------------------------------- | ----------------- | ---------------------------------------------------------------------------------- |
| `monitored_at`                  | string (ISO 8601) | Timestamp when the monitoring of cluster started                                   |
| `id`                            | string            | Unique identifier for the cluster in the system. (this is the cluster\_identifier) |
| `name`                          | string            | The name of the cluster.                                                           |
| `controller_version`            | string            | Version of the cluster controller.                                                 |
| `controller_status`             | string            | Possible options: running, stopped                                                 |
| `controller_last_updated`       | string            |                                                                                    |
| `provider`                      | string            | The cloud provider where the cluster is hosted (e.g., aws).                        |
| `regions`                       | Array\[string]    | List of regions in which the cluster is deployed.                                  |
| `nodes_count`                   | int               | The total number of nodes in the cluster.                                          |
| `running_nodes_count`           | int               | The number of nodes currently running.                                             |
| `failed_nodes_count`            | int               | The number of nodes that have failed.                                              |
| `failed_to_install_nodes_count` | int               | The number of nodes that failed to install.                                        |
| `disabled_nodes_count`          | int               | The number of nodes that are currently disabled.                                   |

**Response codes:**

| Status code | Status code                               |
| ----------- | ----------------------------------------- |
| 200         | OK                                        |
| 400         | Bad request - Required fields are missing |
| 403         | Permission denied                         |
| 404         | Not found                                 |
| 500         | Internal server error                     |

#### Request URL : <a href="#id-2a69rfaw96qy" id="id-2a69rfaw96qy"></a>

```json
GET /runtime/api/v1/clusters?limit=10&offset=0&return_nodes=true
```

#### Examples <a href="#a9zq3fyw3mh7" id="a9zq3fyw3mh7"></a>

**Example request**

```json
{
  "limit": "50",
  "last_key": "id123",
}
```

**Example successful response**

```json
200 OK

"pagination": {
"total_count": 105
	"next_key": "87319827319827",
"limit": 10
},
"total_count": 2,
"clusters": [
        {
            
            "monitored_at": "2024-10-14T15:26:37.202185Z",
            "id": "7254a153-2d14-4906-9231-f76ef89cdb61",
            "name": "yalinruntimeback",
            "controller_last_updated": "2024-10-31T07:22:42.844701Z",
            "controller_version": "1.0.0",
            "controller_status": "running",
            "provider": "aws",
            "regions": [
                "eu-north-1"
            ],
            "nodes_count": 2,
            "running_nodes_count": 2,
            "failed_nodes_count": 0,
            "failed_to_install_nodes_count": 0,
            "disabled_nodes_count": 0
        }
    ]
}
```

**Example error response:**

```json
404 Not Found
{
    "error": "error message"
}
```
