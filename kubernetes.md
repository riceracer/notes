# Port forward

    kubectl port-forward kafka-0 9192:9092 &

# Copy file from remote pod to local context

    kubectl cp <PODNAME>:tmp/output.csv output.csv

# Scale stateful set

    kubectl scale sts SETNAME --replicas=0

# Scale deployment

    kubectl scale deployment/SERVICENAME --replicas=0

# Show logs for pod

    kubectl logs PODNAME

# Describe a service, deployment or whatever

    kubectl describe deployment NAME

# Delete a pod

Delete pod, let k8s redeploy it

    kubectl delete pod PODNAME

# Get kubenetes versions

    kubectl version
    kubectl get nodes
