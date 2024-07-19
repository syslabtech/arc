# Horizontal Runner Autoscaler Configuration

This document outlines the configuration for a `HorizontalRunnerAutoscaler` that automatically adjusts the number of GitHub Actions runners based on workload in a Kubernetes cluster.

## HorizontalRunnerAutoscaler YAML Configuration

The following YAML configuration defines a `HorizontalRunnerAutoscaler` named `organization-runner-autoscaler` in the `ns-build` namespace. This configuration allows for dynamic scaling of runner instances based on the percentage of busy runners.

```yaml
apiVersion: actions.summerwind.dev/v1alpha1
kind: HorizontalRunnerAutoscaler
metadata:
  name: organization-runner-autoscaler
  namespace: ns-build
spec:
  scaleDownDelaySecondsAfterScaleOut: 120
  scaleTargetRef:
    kind: RunnerDeployment
    name: pod-action-runner
  minReplicas: 1
  maxReplicas: 5
  metrics:
  - type: PercentageRunnersBusy
    scaleUpThreshold: '0.75'
    scaleDownThreshold: '0.25'
    scaleUpFactor: '1'
    scaleDownFactor: '1'
```

### Configuration Breakdown

- **apiVersion**: Specifies the API version for the Horizontal Runner Autoscaler.
- **kind**: Indicates that this configuration is for a HorizontalRunnerAutoscaler.
- **metadata**: Contains metadata about the autoscaler, including its name and namespace.
- **spec**: Defines the desired scaling behavior.
  - **scaleDownDelaySecondsAfterScaleOut**: The delay (in seconds) before scaling down after a scale-out event (120 seconds in this case).
  - **scaleTargetRef**: References the `RunnerDeployment` that this autoscaler will manage.
    - **kind**: The kind of resource being targeted (RunnerDeployment).
    - **name**: The name of the `RunnerDeployment` to scale (pod-action-runner).
  - **minReplicas**: The minimum number of replicas to maintain (1).
  - **maxReplicas**: The maximum number of replicas to scale up to (5).
  - **metrics**: Specifies the metrics used for scaling decisions.
    - **type**: The type of metric to monitor (PercentageRunnersBusy).
    - **scaleUpThreshold**: The threshold for scaling up (75% busy runners).
    - **scaleDownThreshold**: The threshold for scaling down (25% busy runners).
    - **scaleUpFactor**: The factor by which to increase replicas when scaling up (1).
    - **scaleDownFactor**: The factor by which to decrease replicas when scaling down (1).

## Applying the Configuration

To create the `HorizontalRunnerAutoscaler`, save the above YAML configuration to a file named `horizontalrunnerautoscaler.yaml`, and apply it to your Kubernetes cluster using the following command:

```bash
kubectl apply -f horizontalrunnerautoscaler.yaml
```

## Conclusion

This configuration sets up a Horizontal Runner Autoscaler for GitHub Actions runners, allowing for automatic scaling based on the workload. Adjust the parameters as necessary to fit your specific requirements and ensure optimal performance of your CI/CD processes.
