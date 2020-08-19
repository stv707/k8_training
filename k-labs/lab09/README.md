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

**Simulate POD failure
k get pods 
kubectl delete pods (the_SITH) --grace-period=0 --force
k get pods 
curl (kubia-public IP address)

**Simulate NODE failure ( DO NOT DO THIS ON PRODUCTION )
kubectl drain (node-name) --force --delete-local-data --ignore-daemonsets

k get pods -o wide

**Bring back the node
kubectl uncordon (node-name)
```

# Please clean up before moving to LAB09B
```sh
kubectl get statefulsets
k delete statefulsets.apps kubia
k get pods

k delete pvc --all
k delete pv --all
k delete svc --all 

ls /nfsdata/dat3 
delete all the sub folder under dat3 
```


# Lab09B
- Running MySQL Replication with Stateful Sets
- refer: https://kubernetes.io/docs/tasks/run-application/run-replicated-stateful-application/
- refer: https://medium.com/@Alibaba_Cloud/kubernetes-application-management-stateful-services-7825e076bcb3
# Steps
```sh
kubectl apply -f mysql-configmap.yaml
k get cm

kubectl apply -f mysql-services.yaml
k get svc

kubectl apply mysql-statefulset.yaml 

kubectl get pods -l app=mysql --watch

kubectl run mysql-client --image=mysql:5.7 -i --rm --restart=Never --\
  mysql -h mysql-0.mysql <<EOF
CREATE DATABASE test;
CREATE TABLE test.messages (message VARCHAR(250));
INSERT INTO test.messages VALUES ('hello');
EOF

kubectl run mysql-client --image=mysql:5.7 -i --rm --restart=Never --\
  mysql -h mysql-read <<EOF
CREATE DATABASE test;
CREATE TABLE test.messages (message VARCHAR(250));
INSERT INTO test.messages VALUES ('hello WORLD 2');
EOF


kubectl run mysql-client --image=mysql:5.7 -i -t --rm --restart=Never --\
  mysql -h mysql-read -e "SELECT * FROM test.messages"
  
kubectl run mysql-client --image=mysql:5.7 -i -t --rm --restart=Never --\
  mysql -h mysql-read -e "SELECT @@server_id,NOW()"


**Run this on new terminal 
kubectl run mysql-client-loop --image=mysql:5.7 -i -t --rm --restart=Never --\
  bash -ic "while sleep 3; do mysql -h mysql-read -e 'SELECT @@server_id,NOW()'; done"

**Simulate POD failure
kubectl delete pod mysql-2

kubectl run mysql-client --image=mysql:5.7 -i -t --rm --restart=Never --\
  mysql -h mysql-read -e "SELECT * FROM test.messages"

**Scale the statefulsets 


```
# Please clean up 
```sh
kubectl get statefulsets
k delete statefulsets.apps mysql
k get pods

k delete pvc --all
k delete pv --all
k delete svc --all 
k delete cm --all 

ls /nfsdata/dat3
delete all the sub folder under dat3 
```
END