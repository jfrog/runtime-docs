# Enable/Disable Runtime Sensors.

Sensors are deployed as a DaemonSet and are installed by default on each of the cluster’s nodes. However, after the sensor's installation using Helm, runtime sensors can be disabled and enabled on demand.

To disable runtime sensors:

`kubectl label nodes <nodes> disable_jfrog_runtime=true`

To enable runtime sensors:

`kubectl label nodes <nodes> disable_jfrog_runtime`-

\<nodes> should be replaced with:

* A single node, e.g. kubectl label nodes my\_node disable\_jfrog\_runtime=true
* A list of nodes, e.g. kubectl label nodes node1 node2 node3 disable\_jfrog\_runtime=true
* All nodes, kubectl label nodes --all disable\_jfrog\_runtime=true
