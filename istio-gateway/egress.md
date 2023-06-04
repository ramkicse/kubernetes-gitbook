# Egress

Force to use egress

&#x20;istioctl install --set profile=demo\
\--set meshConfig.outboundTrafficPolicy.mode=REGISTRY\_ONLY



disable egress

istioctl install --set profile=demo\
\--set meshConfig.outboundTrafficPolicy.mode=ALLOW\_ANY



Add Service Entry

````yaml
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: ServiceEntry
metadata:
  name: jsonplaceholder
spec:
  hosts:
  - jsonplaceholder.typicode.com
  ports:
  - number: 80
    name: http
    protocol: HTTP
  resolution: DNS
  location: MESH_EXTERNAL
```
````

