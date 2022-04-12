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

Service: 
* LoadBalancer - The External IP will always be Pending in local
* NodePort - Use the NodePort service type for local testing - http://localhost:node-port

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

```
kubectl apply -f manifest.yml

kubectl get svc
```


