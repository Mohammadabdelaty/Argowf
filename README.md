# Pod status notification
I've been asked to create Notfication for pod status with specific label in specific ns, so I did this:

## Install argo in argo ns
```bash
kubectl apply -f argo-install.yaml -n argo
```

## argo events

```bash
kubectl apply -f argo-event-install.yaml 
#kubectl apply -f Argowf/argo-event-rbac.yaml

# NS
kubectl apply -f sensor-rbac.yaml -n argo-events # sensor rbac namespaced
kubectl apply -f workflow-rbac.yaml -n argo-events # wf rbac namespaced

kubectl apply -f eventbus.yaml -n argo-events # Eventbus
kubectl apply -f event-source.yaml -n argo-events # Eventbus
kubectl apply -f sensor-teams.yaml -n argo-events # take from webhook and trigger the wf
kubectl apply -f event-job.yaml -n argo-events # Create webhook sa and argo-event roles for the wf
```
In your teams App:

Create channel on teams > Manage > edit connectors > configur webhook > copy the link > Done
Test your webhook link: webhook teams

```bash
curl -H "Content-Type: application/json" \
     -d '{"text": "Hello from curl! This is a test message to Teams 🚀"}' \
     <WEBHOOK_URL>
```

Then after deploying the job you should see the messages.

## References:
    https://argoproj.github.io/argo-events/quick_start/
    https://github.com/argoproj
