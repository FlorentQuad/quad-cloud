# Setup Guide

## Deploying Applications

Per application there will be resource a group. 

- *!! Only designated users are allowed to create resources in resource group. !!*
- *!! List allowed resources !!*

### Deploy K8s Resources

To deploy K8s resources use the configuration file in the [Bootstrap Repo](https://dev.azure.com/quadsolutions/SupplyLink/_git/pionative-infra?path=/k8s/bootstrap/staging/values-override.yaml) and a Helm chart.

Helm chart location for resources in Bootstrapp Repo:
```
k8s/apps/<app>/*resources*
```

#### Logging
Logging of your resources can be found in Grafana.

#### Pushing Images To Container Registries

Container images are pushed to registries using **federated identies**. A federated identity can be configured through an **Azure App Registration**.

## K8s
To connect to the cluster you need to use the [vpn gateway](https://portal.azure.com/#@quadsolutions.nl/resource/subscriptions/478f3cab-a4eb-41b4-ae96-9f1358e9338e/resourceGroups/shared-k8s-rg/providers/Microsoft.Network/virtualNetworkGateways/shared-hub-vpn-gateway/pointtositeconfiguration)

Cluster access is managed through Azure AD groups:

- `k8s-admin`
- `k8s-developer`

### Grafana

Access is provided via the Azure App Registration `staging-k8s-platform-apps-app`.

### ArgoCD

ArgoCD uses the K8s AD groups mentioned above.

### Accessing Azure Resources from K8s

Access from the K8s cluster to Azure resources is handled via K8s **Service Accounts** integrated with Azure Federated Identity.

This enables workloads to securely access Azure services such as:

- Azure Key Vault (secrets and configuration containers)
- Azure Container Registry (image pulls)

Azure uses the cluster’s **OIDC identity provider endpoint** to validate and authorize requests.

# Links
- [Bootstrap Repo]([https://dev.azure.com:v3/quadsolutions/SupplyLink/pionative-infra](https://dev.azure.com/quadsolutions/SupplyLink/_git/pionative-infra)
- [ArgoCD](https://argocd.internal.staging.pionative.quad.team)
- [Grafana](https://grafana.internal.staging.pionative.quad.team)
