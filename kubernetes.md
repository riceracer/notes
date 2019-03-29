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

Use this to get logs of what is going on with the service - errors at the k8s level, whatever

    kubectl describe deployment NAME
    kubectl describe svc NAME
    
# Get info on service resources

Use this to check is service has or is having problems claiming an IP address

    kubectl get svc NAME

# Delete a pod

Delete pod, let k8s redeploy it

    kubectl delete pod PODNAME

# Get kubenetes versions

    kubectl version
    kubectl get nodes
