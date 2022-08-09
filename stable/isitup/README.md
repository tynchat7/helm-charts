# IsItUp Helm Chart

## Chart Details
This chart will Deploy the IsItUp application onto Kubernetes cluster which will allow us to check our internal apps if they are up and running or down.

## Prerequisites Details
* Helm >=2.8.0 
* Kubernetes >=1.9
  

## Chart Installation

If you would like customizing the chart, please see below for further information . <br>

* To get started add our repository 
  ```
  $  helm repo add fuchicorp https://fuchicorp.github.io/helm_charts
  ```

* To install the chart with the release name `isitup`:

  ```
  $ helm install isitup fuchicorp/isitup
  ```
* To install into a Namespace 
  ```
  cd /helm_charts/stable/
  $ helm install isitup ./isitup --namespace tools
  ```


## After Install Instructions
Once you have installed your chart you will see that we have populated the `values.yaml` file. You can either use the chart like that or customize it as needed. <br> <br>


## Configurations of the IsItUp helm chart
| Parameter                                   | Description                           | Default                                                          |
| ------------------------------------------- | ------------------------------------- | ---------------------------------------------------------------- |
| `Name`                                      | isitup statefulset name               | `isitup`                                                         |
| `Image.repository`                          | Container image name                  | `fsadykov/isitup`                                                |
| `Image.pullPolicy`                          | Container pull policy                 | `IfNotPresent`                                                   |
| `Image.tag`                                 | Container image tag                   | `latest`                                                         |
| `imagePullSecrets`                          | Container pull policy                 | `[]`                                                             |
| `nameOverride`                              | Override the resource name prefix     | `isitup`                                                         |
| `fullnameOverride`                          | Override the full resource names      | `isitup-{release-name}` (or `isitup` if release-name)            |
| `serviceAccount.create`                     | create service account                | `true`                                                           |
| `serviceAccount.annotation`                 | annotations for the service account   | `{}`                                                             |
| `serviceAccount.name`                       | service account name                  | `""`                                                             |
| `podAnnotations`                            | associate annotations to the pod      | `{}`                                                             |
| `podSecurityContext`                        | associate security group to the pod   | `{}`                                                             |
| `securityContext`                           | associate security access to users    | `{}`                                                             |
| `globalEnvironments.enabled`                | enable environment variable           | `true`                                                           |
| `globalEnvironments.environments.name`      | add environment variable              | `DEBUG`                                                          |
| `globalEnvironments.environments.value`     | enable environment variable           | `"true"`                                                         |
| `globalEnvironments.environments.name`      | add environment variable              | `GIT_TOKEN`                                                      |
| `globalEnvironments.environments.value`     | configure environment variable        | your gitHub token `${git_toket}`                                 |
| `imageSecret.enabled`                       | enable image secret                   | `true`                                                           |
| `imageSecret.allSecrets.name`               | configure image secret                | `nexus-creds`                                                    |
| `service.type`                              | Configures the service type           | `LoadBalancer`, `ClusterIP` or `NodePort`                        |
| `service.port`                              | Configures the service port           | `80`                                                             |
| `Ingress.enabled`                           | Create Ingress for isitup UI (https)  | `true`                                                           |
| `Ingress.annotations`                       | Associate annotations to the Ingress  | `{}`                                                             |
| `Ingress.hosts.host`                        | Associate hosts with the Ingress      | your deployment endpoint `${endpoint}` ex: `isitup.fuchicorp.com`|
| `Ingress.hosts.path`                        | Associate path with the Ingress       | `/`                                                              |
| `Ingress.tls.hosts`                         | Associate TLS with the Ingress        | your deployment endpoint `${endpoint}` ex: `isitup.fuchicorp.com`|
| `githubProxy.enabled`                       | create proxy                          | `true`                                                           |
| `githubProxy.githubOrganization`            | Associate githubOrganization to proxy | `fuchicorp.com`                                                  |
| `githubProxy.endpoint`                      | Associate the endpoint                | your deployment endpoint `${endpoint}` ex: `isitup.fuchicorp.com`|
| `Resources`                                 | Container resource requests and limits| `{}`                                                             |
| `autoscaling.enabled`                       | Enable autoscaling                    | `false`                                                          |
| `autoscaling.minReplicas`                   | set min replicas for autoscaling      | `1`                                                              |
| `autoscaling.maxReplicas`                   | set max replicas for autoscaling      | `100`                                                            |
| `autoscaling.targetCPUUtilizationPercentage`| set CPU target                        | `80`                                                             |
| `nodeSelector`                              | Node labels for pod assignment        | `{}`                                                             |
| `tolerations`                               | Tolerations for pod assignment        | `[]`                                                             |
| `affinity`                                  | Affinity settings                     | `{}`                                                             |

## Configuring Service 

### **Examples below are of the service type and ports associated:**
  
  - **ClusterIP** 
```
service:
  type: ClusterIP
  port: 80
```
  - **LoadBalancer** 
```
service:
  type: LoadBalancer
  port: 80
  ```
  - **NodePort** 
```
service:
  type: NodePort
  port: 80
```
Please note, you will need to allow access for these ports via your firewall or security group. <br><br>

## Upgrade chart
* To upgrade helm chart after changing anything in values.yaml
  ```
  $ helm upgrade isitup ./isitup
  ```
## Fetch chart
* To fetch the isitup chart and customize it
  ```
  $ helm fetch fuchicorp/isitup --untar
  ```
## Testing if deployed Chart is working as intended
Copy your deployed chart endpoint to the web browser `$endpoint`, ex: `isitup.fuchicorp.com`<br> <br>

## Delete Chart
* to delete the chart do the following 
  ```
  $ helm uninstall isitup --namespace tools
  ```
