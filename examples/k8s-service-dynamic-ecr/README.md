# Dynamic ECR Repository Example

This example demonstrates how to use the `k8s-service` Helm chart with the dynamic ECR repository construction feature.

## Overview

Instead of hardcoding the full `containerImage.repository` path, you can provide identity parameters (`orgid`, `buid`, `appid`, `applicationName`) to automatically construct the repository URL following the standard convention:

`${orgid}-${buid}-${appid}/${applicationName}`

## Usage

Inspect the [values.yaml](values.yaml) file to see how the parameters are configured:

```yaml
orgid: "myorg"
buid: "finance"
appid: "payment"
applicationName: "processor"
```

Deployment of this example will result in a Pod trying to pull the image from:

`myorg-finance-payment/processor:v1.0.0`

## Deploy

```bash
helm install dynamic-ecr-example ../../charts/k8s-service -f values.yaml
```

## Verify

Check the generated manifest to confirm the image path:

```bash
helm template dynamic-ecr-example ../../charts/k8s-service -f values.yaml | grep "image:"
```
