# Lab09A
# Step 
Using a StatefulSet

```sh
kubectl get pv,pvc
kubectl get sc 

kubectl get pod 
kubectl get statefulsets

kubectl apply -f kubia-sc-class.yaml
kubectl apply -f kubia-service-headless.yaml

kubectl apply -f kubia-statefulset.yaml

kubectl get pv,pvc
kubectl get sc 

kubectl get pod 
kubectl get statefulsets
kubectl get pods --watch

k apply -f kubia-service-public.yaml

**Playing with your Pods 
k get svc 

**Hit the pods 
curl (kubia-public IP address)

**post some data
curl -X POST -d "DataCON pan pan pan" (kubia-public IP address)
curl (kubia-public IP address)

**Directly post data to pods ( to simulate failure )
k get pod -o wide

curl (kubia-0 IP):8080
curl -X POST -d "DATA: Jedi" (kubia-0 IP):8080
curl (kubia-0 IP):8080

curl (kubia-1 IP):8080
curl -X POST -d "DATA: Sith" (kubia-1 IP):8080
curl (kubia-1 IP):8080

** Simulate POD failure
k get pods 
kubectl delete pods (the_SITH) --grace-period=0 --force
k get pods 
curl (kubia-public IP address)

** Simulate NODE failure ( DO NOT DO THIS ON PRODUCTION )
kubectl drain <node-name> --force --delete-local-data --ignore-daemonsets

k get pods -o wide

**bring back the node
kubectl uncordon (node-name)
```

# Please clean up before moving to LAB09B
```sh
kubectl get statefulsets
k delete statefulsets.apps kubia
k get pods

k delete pvc --all
k delete pv --all

ls /nfsdata/dat3 
delete all the sub folder under dat3 
```


# Lab09B
# If time permits , do this: Running MySQL Replication with Stateful Sets
# refer: https://kubernetes.io/docs/tasks/run-application/run-replicated-stateful-application/

# Steps





```sh

```

# Step 


```sh

```

# Step 

```sh

```

# Step

```sh


```

# Step


```sh

```

# Step

```sh

```

# Step


```sh

```



# Step

```sh

```

# Step



```sh

```

END