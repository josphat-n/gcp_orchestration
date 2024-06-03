## About.
This project contains orchestration manifests for hosting [yolomy e-commerce microservices](https://github.com/Vinge1718/yolo) via kubernetes in Google Cloud Platform.

## Requirements.
Google Cloud Platform (GCP) account with enough credits to run a kubernetes cluster. Familiarity with GCP is an added advantage.

## Installation instructions.
1. Log into your GCP account and create a project.
2. On the main navigation menu select "Kubernetes Engine".
3. Create a new cluster and give it a favourable name.
4. When the cluster is 'ready' connect to it via the command-line access, and run it in cloud shell.
5. Clone this repo via the now available cloud shell terminal.
6. Run `cd yolo_orchestration` to navigate into the cloned repo.
7. Run `kubectl appply -f .` to execute all the manifests.  
8. Run `kubectl get all` and copy the EXTERNAL-IP associated with 'yolomy-service'.

## Interacting with the application.
- Paste the IP on your favourite browser in your host machine and access Yolomy e-commerce site in GCP via that IP.
- Go ahead and add a product (note that the price field only takes a numeric input). 
- You should also view all added products upon refreshing the page.