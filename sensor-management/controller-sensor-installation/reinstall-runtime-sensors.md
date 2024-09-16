# Reinstall Runtime Sensors

Sensors can be reinstalled by reapplying the installation snippet. If a newer version of the sensors is available, they will be updated to the new version.

However, if the sensors were uninstalled, simply reinstalling them will generate a new Cluster ID, which will be presented as a separate cluster in the UI.

To avoid this, run the following command before uninstalling the cluster to retrieve the Cluster ID:

`kubectl -n <NAMESPACE> get configmaps runtime-config-configmap -o custom-columns='clusterId:data.clusterId'`

`# Output:`

`# clusterId`

`# 225c8bec-1a85-4099-ac8e-144b81ac99e8`

This will allow you to reinstall the sensors with the same Cluster ID, preserving the continuity of the monitoring data. To reinstall the sensors with the same Cluster ID, simply set the Cluster ID in the helm upgrade command of the installation snippet:

`--set clusterID`

With the Cluster ID provided during installation, the cluster historical data will be merged with the new installation data.

\


\
