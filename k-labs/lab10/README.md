# Lab10A
# Step 
Limiting resources available to a pods/containers
```sh





```



# Lab10B
# Step 
ResourceQuota
```sh

* create NameSpace 
kubectl create namespace jedi
kubectl create namespace sith 


* run create_user_namespace.sh to generate kubeconfig 
chmod +x create_user_namespace.sh
./create_user_namespace.sh jedi
./create_user_namespace.sh sith


* create hard pod limit 
kubectl apply -f quota-pod_jedi.yaml --namespace=jedi 

kubectl apply -f quota-pod_sith.yaml --namespace=sith


* create linux user 
useradd jedi1 
useradd sith1

* copy the config file to home dir of each 
cp jedi_kubeconfig   ~jedi1 

cp sith_kubeconfig   ~sith1 


* copy quota_test_jedi.yaml to jedi1 user $HOME
cp quota_test_jedi.yaml  ~jedi1

* copy quota_test_sith.yaml to sith1 user $HOME
cp quota_test_sith.yaml  ~sith1


* set .bashrc to call the kubeconfig file on each home dir 
echo "export KUBECONFIG=/home/jedi1/jedi_kubeconfig"  >> ~jedi1/.bashrc 
echo "export KUBECONFIG=/home/sith1/sith_kubeconfig"  >> ~sith1/.bashrc 

* update Access

chown -R jedi1:jedi1  ~jedi1/* 

chown -R sith1:sith1  ~sith1/*

su - jedi1 
kubectl apply -f quota_test_jedi.yaml
*check the pods / deployments 

*on another Terminal 
su - sith1 
kubectl apply -f quota_test_sith.yaml
*check the pods / deployments 




```

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