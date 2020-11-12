## Mock implementation of externa REST API that returns customer info

written in Python with asyncio library.

## To test this service with Kong Ingress with mTLS enabled

```
# spin up minikube latest kuberentes version, v1.18.3 as of now
minikube start --driver=kvm2 --disk-size='20000mb' --cpus='4' --memory='16384mb'

# download istio 1.6.8 and install
bin/istioctl manifest apply --set profile=demo --set values.global.mtls.auto=true --set values.global.mtls.enabled=true
 kubectl label ns default istio-injection=enabled

# create kong namespace with istio injection
kubectl create ns kong
kubectl label ns kong istio-injection=enabled

# run this service with skaffold
skaffold dev

# test the service

curl http://<kong-service-ip:port>/ext-cust-svc/customers/1111

```
