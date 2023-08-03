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
