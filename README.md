# angular-nginx
Example Project on how to run Angular Project on NGINX

### angular app
```
cd my-app
npm install
npm start
```

### docker
```
// build the image
docker build -t ang-nginx-ui .

// run the image
docker run -d --name ang-nginx-webapp -p 80:80 ang-nginx-ui
```
### kubernetes

To access image from local Docker for Desktop set 
* image: *local-image-tag:version*
* imagePullPolicy: *Never* or *IfNotPresent*

```
    spec:
      containers:
      - image: ang-nginx-ui:latest
        name: webapp
        # imagePullPolicy: Always
        imagePullPolicy: Never
        resources: {}
        ports:
          - containerPort: 80 
```

Service Types: 
* LoadBalancer - The External IP will always be Pending in local
* NodePort - Use the NodePort service type for local testing - http://localhost:node-port

```
NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes                ClusterIP      10.96.0.1        <none>        443/TCP        119d
nginx-webapp              LoadBalancer   10.102.112.175   <pending>     80:31419/TCP   14s
nginx-webapp-cluster-ip   ClusterIP      10.106.65.77     <none>        80/TCP         13s
nginx-webapp-node-port    NodePort       10.103.53.52     <none>        80:30340/TCP   10s
```

```
kubectl apply -f manifest.yml

kubectl get svc
```


