# Create a replicaset
kubectl create -f replicaset-demo.yaml

# Get list of ReplicaSets
kubectl get replicaset
kubectl get rs

# Describe the newly created ReplicaSet
kubectl describe rs/<replicaset-name>


# Expose ReplicaSet as a Service
Expose ReplicaSet with a service (NodePort Service) to access the application externally (from internet)
# Expose ReplicaSet as a Service
kubectl expose rs <ReplicaSet-Name>  --type=NodePort --port=80 --target-port=8080 --name=<Service-Name-To-Be-Created>
kubectl expose rs my-helloworld-rs  --type=NodePort --port=80 --target-port=8080 --name=my-helloworld-rs-service

# Get Service Info
kubectl get service
kubectl get svc

# Get Public IP of Worker Nodes
kubectl get nodes -o wide

# Access the Application using Public IP
http://<node1-public-ip>:<Node-Port>/hello

# Test Replicaset Reliability or High Availability
Test how the high availability or reliability concept is achieved automatically in Kubernetes
Whenever a POD is accidentally terminated due to some application issue, ReplicaSet should auto-create that Pod to maintain desired number of Replicas configured to achive High Availability.
# To get Pod Name
kubectl get pods

# Delete the Pod
kubectl delete pod <Pod-Name>

# Verify the new pod got created automatically
kubectl get pods   (Verify Age and name of new pod)

# Test ReplicaSet Scalability feature
Test how scalability is going to seamless & quick
Update the replicas field in replicaset-demo.yml from 3 to 6.
# Before change
spec:
  replicas: 3

# After change
spec:
  replicas: 6
Update the ReplicaSet
# Apply latest changes to ReplicaSet
kubectl replace -f replicaset-demo.yml

# Verify if new pods got created
kubectl get pods -o wide