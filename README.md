Install argowf in argo ns
```bash
kubectl apply -f Argowf/argo-install.yaml -n argo
```
argo events

Do i need to install argo-event in all ns needs to have argowf in it?
```bash
kubectl apply -f Argowf/argo-event-install.yaml 
kubectl apply -f Argowf/argo-event-rbac.yaml

# NS
kubectl apply -f Argowf/sensor-rbac.yaml -n argo-events # sensor rbac namespaced
kubectl apply -f Argowf/workflow-rbac.yaml -n argo-events # wf rbac namespaced
kubectl apply -f Argowf/eventbus.yaml -n argo-events # Eventbus

kubectl apply -f Argowf/event.yaml -n argo-events # Create webhook sa and argo-event roles for the wf
kubectl apply -f Argowf/event-source.yaml -n argo-events # Eventbus
kubectl apply -f Argowf/sensor.yaml -n argo-events # take from webhook and trigger the wf

```



Webhook teams
test using :
curl -H "Content-Type: application/json" \
     -d '{"text": "Hello from curl! This is a test message to Teams 🚀"}' \
     <WEBHOOK_URL>







## References:
    https://argoproj.github.io/argo-events/quick_start/