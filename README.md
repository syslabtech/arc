
# ARC Helm REPO

## Adding the Helm Repository

To add the Actions Runner Controller Helm repository, run the following command:

```bash
helm repo add actions-runner-controller https://actions-runner-controller.github.io/actions-runner-controller
```

## Installing the Actions Runner Controller

To install the Actions Runner Controller in the `ns-build` namespace, execute the command below. This will create the namespace if it does not exist and set the necessary configurations:

```bash
helm install --namespace ns-build --create-namespace \
  --set=authSecret.create=true \
  --set=authSecret.github_token="YOUR_ORGANIZATION_TOKEN" \
  --set=certManagerEnabled=false \
  --set=replicaCount=2 \
  --wait actions-runner-controller actions-runner-controller/actions-runner-controller
```

## Upgrading or Installing the Actions Runner Controller

To upgrade or install the Actions Runner Controller in the `filebeat` namespace, use the following command:

```bash
helm upgrade --install --namespace filebeat \
  --set=authSecret.create=true \
  --set=authSecret.github_token="YOUR_ORGANIZATION_TOKEN" \
  --wait actions-runner-controller actions-runner-controller/actions-runner-controller
```

file provides clear instructions on how to add the Helm repository, install, and upgrade the Actions Runner Controller. Make sure to replace the GitHub tokens with your own for security purposes.

Citations:
[1] https://actions-runner-controller.github.io/actions-runner-controller
