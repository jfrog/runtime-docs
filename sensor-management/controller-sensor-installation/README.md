# Controller/Sensor Installation

The JFrog Runtime has two installation options depending on what you have purchases.&#x20;

* Runtime Integrity: Default option with [Runtime Controller ](../../jfrog-runtime-security/solution-architecture.md#controller)only.&#x20;
* Runtime Impact: An additional option that includes Runtime Controller and [Runtime Sensors](../../jfrog-runtime-security/solution-architecture.md#runtime-sensor).&#x20;

The Sensor Management capability includes a convenient feature that allows users to install sensors on their clusters easily.

To install a runtime sensor on a cluster, simply click on the **Install Runtime** button in **Sensor Management**. This will prompt you with the installation wizard that contains the necessary commands to install the sensor.

The wizard aims to deploy all runtime sensor components on a single cluster regardless of the number of servers contained.

Simply name your cluster, which will be used under the cluster management as the name of the cluster you are about to deploy.&#x20;

The wizard allows you to specify the namespace where the JFrog Runtime component will run.&#x20;

For consistency, please make sure to use the same name on all of the clusters. &#x20;

To complete the installation, copy and execute the snippet from a jump server where the kubectl context is set to the required cluster.&#x20;

Once the sensor is deployed successfully, a new line indicating the sensor deployment will be added under sensor management.&#x20;

To uninstall the sensors on a cluster, see [Uninstall](uninstall-sensors.md).&#x20;

If you wish to disable the sensor, see [here](enable-disable-runtime-sensors..md).&#x20;

### Installing Runtime

1. Navigate to **Administration** > **Runtime** > **Sensor Management** page and click **Install Runtime**. \
   A wizard appears. \
   ![](<../../.gitbook/assets/Screenshot 2024-09-03 at 15.59.41.png>)
2. Provide the environment details:\
   a. **Cluster name**: Name of the cluster which will be used under the cluster management as the name of the cluster you are about to deploy. \
   b. **Name space**: Specify the namespace where the JFrog Runtime component will run
3. Select the installation type; **Controller** only or **Controller and Sensors**. &#x20;
4.  Copy and run the command that is shown in your terminal. \
    You can view the status of your controllers and sensors in [Sensor Management.](broken-reference) \


    ![](<../../.gitbook/assets/Screenshot 2024-09-03 at 16.01.03.png>) ![](<../../.gitbook/assets/Screenshot 2024-09-03 at 16.05.28.png>)







