# Commands to build and run docker image locally
docker build -t kube-service .
docker run -p 8080:8080 kube-service

### To list all images
docker images

### To find current running docker process
docker ps -a

### To stop a container
docker stop

### To remove an image
docker rmi 

### To go inside the container
docker exec -it /bin/sh

### To push docker image to docker hub after building the image
docker login -u=azaveri7
docker tag kube-service:latest azaveri7/docker-labs:kube-demo1
docker push azaveri7/docker-labs:kube-demo1

### Steps to run docker image in minikube:
minikube start
minikube status
minikube dashboard

### Install ingress controller
minikube addons enable ingress
kubectl get pods -n kube-system

### Creating a Deployment using an existing Docker image
kubectl run kube-demo --image=azaveri7/docker-labs:kube-demo1 --port=8080

The above command will use the tag kube-demo1 from the repository docker-labs at
deployment.

### Creating a service for the Deployment created in previous step
kubectl expose deployment kube-demo --target-port=8080 --type=NodePort

minikube service kube-demo --url
output: http://172.17.0.41:32492

### Testing minikube deployment
curl http://172.17.0.41:32492/employees/
output:
```[{"id":1,"firstName":"Pradeep","lastName":"Singh","emailId":"Pradeep.Singh2@gmail.com"},{"id":2,"firstName":"Anand","lastName":"Zaveri","emailId":"Anand.Zaveri@gmail.com"},{"id":3,"firstName":"Akhilesh","lastName":"Juyal","emailId":"Akhilesh.Juyal@gmail.com"},{"id":4,"firstName":"Vaibhav","lastName":"Jha","emailId":"Vaibhav.Jha@outlook.com"},{"id":5,"firstName":"Himanshu","lastName":"Sharma","emailId":"Himanshu.Sharma@yahoo.com"},{"id":6,"firstName":"Jignesh","lastName":"Mehta","emailId":"Jignesh.Mehta@outlook.com"}]```

curl http://172.17..0.41:32492/employees/2
output:
```{"id":2,"firstName":"Anand","lastName":"Zaveri","emailId":"Anand.Zaveri@gmail.com"}```
