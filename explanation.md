## About.

This file explains roles and choice of the 'kind' parameter of the manifest file used in hosting Yolomy site in Google Cloud Platform via kubernetes orchestration.

## Manifest files:

All manifest file are declared via yaml format. The order of execution of the manifests informed by docker containers dependency on each other, ie, starting from database which is depended upon by backend which is in turn depended upon by the frontend.

### 1. mongo_deployment.yml
Database of kind Deployment is created. Deployment kind is selected as it will create replica set(s) which auto create in case of a  pod failure.
Mongo image version 4.0 from docker hub is selected, and containerPort 27017, on which mongo db listens is exposed. 

### 2. mongo_service.yml
Services enable communication between different sets of pods, and between pods and external users. Services enable loose-coupling between microservices in the application. 
This service of kind "NodePort" listens to mongo database pods on port 27017 exposes them via port 27017 and by the name "db", enabling backend microservice to connect to the database via its native port (27017).

### 3. backend_deployment.yml
A kind of Deployments is used just like in the mongo_deployment above, for similar reasons. 
A custom image (josphatn/yolo_backend:1.0.0) of the dockerized backend microservice hosted on docker hub is used and a container port 5000 exposed.

### 4. backend_service.yml
A service of kind "NodePort" with the name backend which listens on backend pods on port 5000 is created to allow connection with frontend microservice which connects to backend on port 5000.

### 5. client_deployment.yml
Similar to mongo and backend deployments, a kind "Deployment" is used for frontend microservice.
A custom image (josphatn/yolo_client:1.0.1) of the dockerized frontend microservice hosted on docker hub is used and a container port 3000 exposed.

### 5. yolomy_app_service.yml
A kind "Service" but of type "LoadBalancer" is used. The advantage of LoadBalancer is that it creates an external IP which can be used to access any of the pods that it exposes.
