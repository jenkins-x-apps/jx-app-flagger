# jx-app-flagger

The chart for the [Flagger](https://flagger.app/) for Jenkins X.

## Install

This chart can be installed using the `jx` CLI.

```shell
jx add app jx-app-flagger
```

Enable Istio in production namespace:

```shell
$ kubectl label namespace jx-production istio-injection=enabled
```

Create the Istio gateway:

```shell
$ kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: jx-gateway
  namespace: istio-system
spec:
  selector:
    istio: ingressgateway # use Istio default gateway implementation
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - "*"
EOF
```
