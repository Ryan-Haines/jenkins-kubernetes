# jenkins-kubernetes
jenkinsconfig for kuberenetes deployment

after configuring microk8s for raspberry pi, to start a jenkins container:

kubectl apply -f on each .yaml files in the following order:

```
kubectl apply -f jenkins-volume.yaml &&
kubectl apply -f jenkins-deployment.yaml &&
kubectl apply -f jenkins-service.yaml
```

Get the NodePort assigned to the service:

`$ kubectl get svc jenkins-service`

You'll see an output like:
```

NAME              TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
jenkins-service   NodePort   10.108.144.78   <none>        8080:31813/TCP   1m
```

You can now access Jenkins at http://<Node-IP>:<NodePort>, where <Node-IP> is the IP address of any node in your cluster and <NodePort> is the port number assigned to the service (in this example, 31813).

Get the password by executing against the jenkins process

`kubectl get pods` to get the name of the jenkins-xxxx instance then 

```
kubectl exec -it jenkins-xxxx -- cat /var/jenkins_home/secrets/initialAdminPassword
```

save the password and install suggested plugins

skip user creation

Start!

settings -> configure -> ssh public keys result of `cat ~/.ssh/id_rsa.pub`