---
description: Create New Gateway
---

# Stubbed-out gateway

{% code lineNumbers="true" fullWidth="true" %}
````yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-user-gateway-injected
  namespace: istioinaction
spec:
  selector:
    matchLabels:
      ingress: my-user-gateway-injected
  template:
    metadata:
      annotations:
        sidecar.istio.io/inject: "true"
        inject.istio.io/templates: gateway        
      labels:
        ingress: my-user-gateway-injected
    spec:
      containers:
      - name: istio-proxy
        image: auto 
---
apiVersion: v1
kind: Service
metadata:
  name: my-user-gateway-injected
  namespace: istioinaction
spec:
  type: LoadBalancer
  selector:
    ingress: my-user-gateway-injected
  ports:
  - port: 80
    name: http
  - port: 443
    name: https      
---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: my-user-gateway-injected-sds
  namespace: istioinaction
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "watch", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: my-user-gateway-injected-sds
  namespace: istioinaction
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: my-user-gateway-injected-sds
subjects:
- kind: ServiceAccount
  name: default

```

````
{% endcode %}

The Kubernetes deployment specified is stubbed out and annotated with instructions for how Istio should do the injection. Specifically, we configure the template used for injection to be the gateway template. You can see which templates are available in the istio-sidecar-injector configmap in the istio-system namespace.
