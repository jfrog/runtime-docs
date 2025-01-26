# Installing JFrog Runtime Security

Before you proceed with the installation, review the Runtime [system requirements](system-requirements.md).

**Prerequisites**:&#x20;

Make sure your `kubectl` and `helm` clients can access the Kubernetes cluster where you want to install the Runtime Service.

In addition, you need an ingress controller (preferably configured with TLS).\
JFrog officially supports the Nginx controller. Using other ingress controllers should also work if they support GRPC communication.

### Preparing your JFrog Platform

This guide describes installing JFrog Runtime Security on a pre-existing JFrog platform.

**Before Installing**

Ensure you have the:

* JFrog platform `<join-key>`
* Your organization's domain name
* The Artifactory Kubernetes service name (which you used to [install Xray](https://jfrog.com/help/r/jfrog-installation-setup-documentation/installing-xray))

#### **JFrog Charts**

For the installation of the different JFrog platform components, you will need access to the JFrog Charts Repository.\
Add and update the JFrog Helm chart repository in your local configuration:\
`helm repo add jfrog https://charts.jfrog.io --force-update`

#### **Artifactory Update**

JFrog Platform with JFrog Runtime Security requires setting the JPD with an ingress controller. If your platform is already configured to work with an ingress controller you can skip this part.\
For Artifactory to work with an ingress controller you need to update your Artifactory configuration.\
Set the following chart values along with the Helm install/upgrade command or pass it in a `values.yaml` file. Make sure to replace `<add-your-public-domain-here>` in the `ingress.hosts` and `tls.hosts` sections with your actual domain name.

```
# This related to a standalone nginx server, as opposed to an ingress-controller.
nginx:
  enabled: false
ingress:
  enabled: true
  defaultBackend:
    enabled: true
  hosts:
    # This should be set to a domain which is associated with the 
    # external IPs of your ingress load balancer.
    - <add-your-public-domain-here>
  routerPath: /
  disableRouterBypass: true
  artifactoryPath: /artifactory/
  className: "nginx"
  annotations:
    nginx.ingress.kubernetes.io/proxy-read-timeout: "600"
    nginx.ingress.kubernetes.io/proxy-send-timeout: "600"
    nginx.ingress.kubernetes.io/proxy-body-size: "0"
    nginx.ingress.kubernetes.io/rewrite-target: "/"
  tls:
    - secretName: artifactory-tls-secret
      hosts:
        # This should be set to a domain which is associated with the 
        # external IPs of your ingress load balancer.
        - <add-your-public-domain-here>
```

### Install the Runtime Service

To install the Runtime Service on the JFrog Platform create a new file named `runtime-values.yaml` with the following content:

```
global:
  deployEnv: onprem
  
  # This should be set to a domain which is associated with the 
  # external IPs of your ingress load balancer.

  jfrogUrl: <add-your-public-domain-here>

postgresql:
  enabled: true

# To use external database:
# database:
#   url: postgres://<host>:5432/runtime
#   user: runtime
#   password: <password>

ingress:
  grpc:
    tlsSecretName: runtime-tls-secret
    securedBackendProtocol: false

router:
  jfrogUrl: <artifactory-service-url> # http://artifactory:8082

runtime:
  joinKey: <join-key> # The same one from artifactory
  image:
    registry: releases-docker.jfrog.io


```

Run the following to install the runtime service:

```
helm upgrade --install runtime -f runtime-values.yaml
```

### Install Runtime Sensors

To obtain the installation snippet for runtime sensors, navigate to Sensor Management under Runtime in the Platform Administration tab, and click the `Install Runtime` button to open the sensor installation wizard. For more information, see [Controller/Sensor Installation](../sensor-management/controller-sensor-installation/).&#x20;

#### **Bypassing Certificate Verification**

If you’re using a self-signed certificate, you need to configure the sensors to bypass verification of the server's certificate chain and hostname. To apply this configuration, set the following value in the sensor installation snippet you copied from the sensor installation wizard:\
`--set tlsInsecureSkipVerify=true`

{% hint style="info" %}
Note that this setup should be carefully reconsidered for production environments based on your organization’s security requirements and constraints.
{% endhint %}
