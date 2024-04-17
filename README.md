# Gloo-9317 Reproducer

## Installation

Add Gloo EE Helm repo:
```
helm repo add glooe https://storage.googleapis.com/gloo-ee-helm
```

Export your Gloo Edge License Key to an environment variable:
```
export GLOO_EDGE_LICENSE_KEY={your license key}
```

Install Gloo Edge:
```
cd install
./install-gloo-edge-enterprise-with-helm.sh
```

> NOTE
> The Gloo Edge version that will be installed is set in a variable at the top of the `install/install-gloo-edge-enterprise-with-helm.sh` installation script.

## Setup the environment

Run the `install/setup.sh` script to setup the environment:

- Deploy the HTTPBin service
- Deploy the VirtualServices

```
./setup.sh
```

## Call HTTPBin and check Access-Log

You can call the HTTPBin service via cURL. The response will have a 2 second delay as configured in the `VirtualService`:

```
curl -v http://api.example.com/get
```

When youn now chech the gateway-proxy's access-log, you will see that the `proxy_latency_response_out` is equal to the `DURATION`.

```
kubectl -n gloo-system logs -f gateway-proxy-{id}
```