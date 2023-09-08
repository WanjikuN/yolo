[Yolo URL]()
---
# Deploying to GKE

## Steps
Using the cloudshell:
* Get your Google cloud project ID
   ```
   gcloud config get-value project
   ```
* Clone the App
   ```
   git clone <repoName>
   ```
* Create a cluster
   ```
   gcloud container clusters create-auto yolo --region us-central1
   ```
* Deploy to GKE
    > Two objects . Deployment and Service
    1. Create manifest directory
        ```
        mkdir manifest
        ```
    1. Add directories to objects
        > deployments , services, Configmap, Secrets, StatefulSets
    1. Create a cluster
        ```
        gcloud container clusters create-auto yolo-app --region us-central1
        kubectl get nodes
        ```
    1. Deploy the resource to the cluster (Example)
        ```
        kubectl apply -f deployment.yaml
        kubectl get deployments
        kubectl get pods
        ```
    1. Create service
        ```
        kubectl apply -f service.yaml
        kubectl get services
        ```
      
        
   
  
---
# Requirements
Make sure that you have the following installed:
- [node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04) 
- npm 
- [MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) and start the mongodb service with `sudo service mongod start`

## Navigate to the Client Folder 
 `cd client`

## Run the folllowing command to install the dependencies 
 `npm install`

## Run the folllowing to start the app
 `npm start`

## Open a new terminal and run the same commands in the backend folder
 `cd ../backend`

 `npm install`

 `npm start`

 ### Go ahead a nd add a product (note that the price field only takes a numeric input)
