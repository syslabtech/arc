Here's a well-structured `README.md` file that includes the provided `RunnerDeployment` YAML configuration. This document will help users understand how to deploy a RunnerDeployment in a Kubernetes environment using the Actions Runner Controller.


# RunnerDeployment Configuration for GitHub Actions

This document provides the configuration for deploying a GitHub Actions RunnerDeployment using the Actions Runner Controller in a Kubernetes cluster.

## RunnerDeployment YAML Configuration

The following YAML configuration defines a `RunnerDeployment` named `buildenv-4c5r` in the `ns-build` namespace. It specifies the desired state for the runners, including resource requests and limits.

```yaml
apiVersion: actions.summerwind.dev/v1alpha1
kind: RunnerDeployment
metadata:
  name: buildenv-4c5r
  namespace: ns-build
spec:
  replicas: 5
  template:
    spec:
      organization: Dynamic-1001-GmbH
      githubAPICredentialsFrom:
        secretRef:
          name: controller-manager
      group: Default
      labels:
        - buildenv-4c5r
      resources:
        requests:
          memory: "256Mi"
          cpu: "100m"
        limits:
          memory: "5Gi"
          cpu: "4000m"
```

### Configuration Breakdown

- **apiVersion**: Specifies the API version for the RunnerDeployment.
- **kind**: Indicates that this configuration is for a RunnerDeployment.
- **metadata**: Contains metadata about the RunnerDeployment, including its name and namespace.
- **spec**: Defines the desired state of the RunnerDeployment.
  - **replicas**: The number of runner instances to deploy (5 in this case).
  - **template**: Contains the template for the runner pods.
    - **organization**: The GitHub organization associated with the runners.
    - **githubAPICredentialsFrom**: References a Kubernetes secret that contains the GitHub API credentials.
    - **group**: The group to which the runners belong.
    - **labels**: Labels to categorize the runners.
    - **resources**: Specifies resource requests and limits for the runner pods.
      - **requests**: Minimum resources required for the pods.
      - **limits**: Maximum resources allowed for the pods.

## Applying the Configuration

To create the `RunnerDeployment`, save the above YAML configuration to a file named `runnerdeployment.yaml`, and apply it to your Kubernetes cluster using the following command:

```bash
kubectl apply -f runnerdeployment.yaml
```

## Conclusion

This configuration sets up a RunnerDeployment for GitHub Actions using the Actions Runner Controller. Adjust the parameters as necessary to fit your specific requirements. Make sure to have the `controller-manager` secret properly configured with your GitHub API credentials for successful authentication.


This `README.md` file provides a clear explanation of the `RunnerDeployment` configuration, making it easy for users to understand and apply it in their Kubernetes environments.
