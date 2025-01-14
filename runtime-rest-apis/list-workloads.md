# List Workloads

### Get Workload <a href="#hca43983mpiv" id="hca43983mpiv"></a>

**Description:** List of Workloads

**Security:** Requires a valid user with a "Read" permission

**Usage:** `POST /runtime/api/v1/workloads`

**Consumes:** `application/json`

**Produces:** `application/json`

#### Request body <a href="#d928slqmiyka" id="d928slqmiyka"></a>

| Name       | Type      | Required/Optional | Description                                                                                        |
| ---------- | --------- | ----------------- | -------------------------------------------------------------------------------------------------- |
| `limit`    | int       | required          | Key-based pagination - number of rows per request                                                  |
| `next_key` | string    | optional          | Id from the previous request, empty on the first request                                           |
| `order_by` | string    | optional          | Available options: `name`, `cluster`,`runtime_status` ,`vulnerabilties_count`, `registry`, `risks` |
| `filters`  | filterObj | optional          | Filter the results by the available filters listed in filter\_object                               |

**filterObj:**

| Name            | Type                       | Required/Optional | Description                                                                                                                                                                                                                                                     |
| --------------- | -------------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_period`   | string                     | optional          | <p>Default - now<br>Options: now, 1 hour, 24 hourse, 3 days, 7 days, 10 days</p>                                                                                                                                                                                |
| `cve_id`        | array\[string]             | optional          | CVE identifier                                                                                                                                                                                                                                                  |
| `risk`          | array                      | optional          | Malicious, untrusted\_registry, integrity\_violation, critical\_applicable                                                                                                                                                                                      |
| `component`     | Array\[filterComponentObj] |                   | - all components                                                                                                                                                                                                                                                |
| `applicability` | Array of app\_enum         | optional          | <p>Contextual Analysis result.</p><p>Possible values: <code>not_scanned</code>, <code>applicable</code>,</p><p><code>not_applicable</code>, <code>undetermined</code>, <code>rescan_required</code>,<code>upgrade_required</code>, <code>not_covered</code></p> |
| `severity`      | array\[string]             | optional          | <p>Contextual Analysis result.</p><p>Possible values: <code>not_scanned</code>, <code>applicable</code>,</p><p><code>not_applicable</code>, <code>undetermined</code>, <code>rescan_required</code>,<code>upgrade_required</code>, <code>not_covered</code></p> |
| `workloads`     | Array\[filterWorkloadObj]  | optional          | If added return data only on workloads that are in the list                                                                                                                                                                                                     |

**filterComponentObj:**

| Name      | Type   | Required/Optional | Description                                                   |
| --------- | ------ | ----------------- | ------------------------------------------------------------- |
| `name`    | string | required          | Component name                                                |
| `version` | string | optional          | Component version; if not provided, all versions are returned |

**filterWorkloadObj:**

| Name        | Tyoe   | Required/Optional | Description                                                                       |
| ----------- | ------ | ----------------- | --------------------------------------------------------------------------------- |
| `name`      | string | required          |                                                                                   |
| `namespace` | string | optional          | Name of name space; if not provided all matches the other params (name & cluster) |
| `cluster`   | string | optional          | Name of cluster; if not provided all matches the other params (name & namespace)  |

#### Response body <a href="#z3w3i3z4ksgi" id="z3w3i3z4ksgi"></a>

| Name          | Type                 | Description                                                  |
| ------------- | -------------------- | ------------------------------------------------------------ |
| `total_count` | int                  | The total number of images tags that match the filter quarry |
| `pagination`  | paginationObj        | Pagination info for the request                              |
| `workloads`   | Array \[workloadObj] |                                                              |

paginationObj:

| Name       | Type   | Description                                              |
| ---------- | ------ | -------------------------------------------------------- |
| `limit`    | int    | Key-based pagination - number of rows per request        |
| `next_key` | string | Id from the previous request, empty on the first request |

**workloadObj:**

| Name                    | Type                 | Description                                                                                                                                                                                                                                                                              |
| ----------------------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`                  | string               | Workload name                                                                                                                                                                                                                                                                            |
| `namespace`             | string               | Workload namespace                                                                                                                                                                                                                                                                       |
| `cluster`               | string               | Cluster name                                                                                                                                                                                                                                                                             |
| `runtime_status`        | string               | Possible values: `running`, `stopped`, `unknown`                                                                                                                                                                                                                                         |
| `nodes`                 | Array of string      | Nodes of the workload                                                                                                                                                                                                                                                                    |
| `architectures`         | string               | Image architecture                                                                                                                                                                                                                                                                       |
| `risks`                 | Array\[ risk\_enum]  | <p>Possible values: <code>malicious</code>, <code>untrusted_registry</code>, <code>integrity_violation</code>, <code>critical_applicable_cves</code>,</p><p><code>untrusted_registry</code>, <code>integrity_violation</code> inherent from images and rest aggregation from process</p> |
| `vulnerabilities_count` | int                  | The sum of all vulnerabilities of the process                                                                                                                                                                                                                                            |
| `Processes`             | Array\[processesObj] | Object of Processes related to this workload                                                                                                                                                                                                                                             |

**processesObj:**

| Name                 | Type                 | Description                                                                     |
| -------------------- | -------------------- | ------------------------------------------------------------------------------- |
| `name`               | string               | Process name                                                                    |
| `runtime_status`     | enum                 | `running` / `stopped` / `unknown`                                               |
| `risks`              | Array of risk\_enum  | `Malicious`/ `untrusted_registry`/ `integrity_violation`/ `critical_applicable` |
| `vulnerabilities`    | Array\[vulnObj]      | An array of the vulnerabilities detected on the process                         |
| `malicious_packages` | Array\[maliciousObj] | An array of malicious packages detected on the image tag                        |
| `arguments`          | string               | Arguments of the running processes                                              |
| `path`               | string               | File system path                                                                |
| `working_directory`  | string               |                                                                                 |
| `image_digest`       | string               |                                                                                 |
| `process_hash`       | string               |                                                                                 |

**vulnObj:**

| Name            | Type                 | Description                                                                                                                                                                                                                                                      |
| --------------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cve_id`        | string               | CVE identifier                                                                                                                                                                                                                                                   |
| `xray_id`       | string               | Xray identifier                                                                                                                                                                                                                                                  |
| `severity`      | string               | Severity level of the issue (e.g., "High")                                                                                                                                                                                                                       |
| `cvss_v2`       | string               | CVSS version 2 score                                                                                                                                                                                                                                             |
| `cvss_v3`       | string               | CVSS version 3 score                                                                                                                                                                                                                                             |
| `applicability` | string               | <p>Contextual Analysis result.</p><p>Possible values: <code>not_scanned</code>, <code>applicable</code>,</p><p><code>not_applicable</code>, <code>undetermined</code>, <code>rescan_required</code>, <code>upgrade_required</code>, <code>not_covered</code></p> |
| `components`    | array\[componentObj] | The components information                                                                                                                                                                                                                                       |

**maliciousObj:**

| Name         | Type                 | Description               |
| ------------ | -------------------- | ------------------------- |
| `xray_id`    | string               | Xray identifier           |
| `components` | array\[componentObj] | The component information |

**componentObj:**

| Name           | Type   | Description                                                                                        |
| -------------- | ------ | -------------------------------------------------------------------------------------------------- |
| `component_id` | string | The component identifier in the Xray format (e.g., "gav://com.thoughtworks.xstream:xstream:1.4.5") |
| `name`         | string | Component name                                                                                     |
| `version`      | string | Component version                                                                                  |

**Response codes:**

| Status code | Description                               |
| ----------- | ----------------------------------------- |
| 200         | OK                                        |
| 400         | Bad request - Required fields are missing |
| 403         | Permission denied                         |
| 404         | Not found                                 |
| 500         | Internal server error                     |

#### Examples <a href="#a9zq3fyw3mh7" id="a9zq3fyw3mh7"></a>

**Example request**

<pre><code>{
"limit": "50",
"last_key": "id123",
    	
	"filters": {
		"severities": ["Critical", "High"],
                "registry" : untrusted_registry,
<strong>                "workloads": [{
</strong>	              "name": "corends",
                      "namespace":"jfs-production", 
                      "cluster":"jfs-production"
                      }]

 	}
 }
</code></pre>

**Example successful response**

```
200 OK
{
    "pagination": {
        "limit": 1,
        "next_key": "1"
    },
    "total_count": 14,
    "workloads": [
        {
            "architecture": "amd64",
            "cluster": "z0dimagtestenv2812",
            "name": "ozone",
            "namespace": "production",
            "nodes": [
                "ip-10-90-101-188",
                "ip-10-90-108-15"
            ],
            "processes": [
                {
                    "arguments": "/usr/local/bin/dumb-init -- entrypoint.sh /usr/local/bin/start-ozone-all.sh",
                    "malicious_packages": [],
                    "name": "dumb-init",
                    "path": "/usr/local/bin/dumb-init",
                    "risks": [],
                    "runtime_status": "running",
                    "vulnerabilities": []
                }],

"risks": [
                "critical_applicable_cves"
            ],
            "runtime_status": "running",
            "vulnerabilities_count": 0
        }


```

**Example error response:**

```
404 Not Found
{
    "error": "error message"
}
```
