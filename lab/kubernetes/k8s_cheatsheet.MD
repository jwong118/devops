Kubernetes Setup
1. Kubernetes is available to setup here:
    - https://kubernetes.io/docs/setup

2. Kubernetes Documentation
    - https://kubernetes.io/docs/home/
    
3. Tutorials
    - https://kubernetest.io/docs/tutorial

k8s Cluster Managemet Commands
1. Display Cluster information
    # kubectl cluster-info

2. Show cluster configurations
    # kubectl config view

3. List all nodes in the cluster    
    # kubectl get nodes

Miscellaneous Commands
1. Create a service
    # kubectl expose deployment <name> --type=NodePort --port=<port>
    
2. Resource schema information
    # kubectl explain <resource>
    
3. List ingress resource
    # kubectl get ingress

4. create config maps
    # kubectl create configmap <name> --from-literal=<key>=<value>

5. Apply changes deficed in a YAML
    # kubectl apply -f <file.yaml>

6. Switch namespace
    # kubectl config set-context --current --namespace=<new-namespace-name>