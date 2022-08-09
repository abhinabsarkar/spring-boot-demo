# Running stateful Spring Boot App on AKS

![alt txt](/images/aks-stateless-springboot-app.jpg)

Declaring a service of type LoadBalancer exposes it externally using a cloud provider’s load balancer. The cloud provider will provision a load balancer for the Service, and map it to its automatically assigned NodePort. How the traffic from that external load balancer is routed to the Service pods depends on the cluster provider.

![alt txt](/images/aks-kubenet-traffic.jpg)

> Nodeport shown in the diagram is for reference. It can be different.

This is the default method for many Kubernetes installations in the cloud, but it uses an IP for every service, and that IP is configured to have its own load balancer configured in the cloud. These add costs and overhead that is overkill for essentially every cluster with multiple services.

> Because of the above mentioned drawbacks, it is best to use `Ingress Controller` in production.

## Run this application on AKS cluster

Set up the AKS cluster
```bash
# Create an AKS cluster
az aks create --resource-group rg-aks-demo --name aks-abs-demo --node-count 1 --generate-ssh-keys --verbose
# Get the AKS credentials - download credentials and configure the Kubernetes CLI
az aks get-credentials --resource-group rg-aks-demo1 --name aks-demo1 --verbose
```
Inside the `k8s-resources` folder, open the file config-map.yaml. Update the data section with the values. This will override the `application.properties` file.

Deploy the application to AKS cluster.
```bash
# Run the below command from the code folder
kubectl apply -f k8s-resources/

# Verify the pods are running
kubectl get pods
# Verify the service of type LoadBalancer is running
kubectl get svc
NAME                                  TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
spring-boot-session-azure-redis-app   LoadBalancer   10.0.148.152   20.200.88.9   80:30627/TCP   3h20m
```

Browse by visiting `http://<EXTERNAL-IP>/`