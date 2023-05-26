# Running Docker Compose
Following the steps on the README.md , update the react scripts from the client side
```
npm uninstall react-scripts
npm install react-scripts

```
# Steps
1. Client side
    * Create a Dockerfile 
        ```
        cd client/
        touch Dockerfile
        ```
    * Populate the Dockerfile using the best base image
    * (Optional) Build the image
        ```
        sudo docker build . -t <dockerhubUsername\imageName:tag>

        ```
     * Push to Docker Hub
        ```
        sudo docker login
        sudo docker push <dockerhubUsername\imageName:tag>
        ```
  
  
2. Backend side
    * Create a Dockerfile 
        ```
        cd backend/
        touch Dockerfile
        ```
    * Populate the Dockerfile using the best base image
    * (Optional) Build the image
        ```
        sudo docker build . -t <dockerhubUsername\imageName:tag>

        ```
     * Push to Docker Hub
        ```
        sudo docker login
        sudo docker push <dockerhubUsername\imageName:tag>
        ```
  ---
  > Bulding an image at this stage allows you to push to Dockerhub so on running Docker compose it will be pulled.
  > Optionally we build from Docker Compose.
  > Use Multistage builds to reduce the size of the images.
  
3. Docker Compose
  We have 3 services running
    * Database
        1. We pull an image from Docker Hub
        1. Has Volumes to persist data in the case where we remove our containers.
    * Client
    * Backend
   > Client communicates to the backend , backend communicates to the database and vice versa

       ```
       sudo docker compose up
       ```
  In the case where you clone this repo and run the previous command, a link to the website network will allow you to view and add products that persist.
  
 ---  
 # Ansible Playbooks
 We run the conteinerized app through playbooks 
 # Steps
 1. Create required files
     * ansible.cfg -this states our inventory location
     * Vagrantfile 
     * hosts -this is our inventory that has the defined servers
     * playbook.yml - this has our main play
     * vars.yml - we define our variables in this file and import them into playbook.yml
 2. Initialize roles for abstraction purposes
     ```
     ansible-galaxy init <roleName>
     ```
     We will use 3 roles in this case and add them to a role folder
     1. git - Installs git
     1. docker -Installs dependencies, docker and docker-compose
     1. docker-compose -Starts our docker compose
    
 3. Run the playbook through vagrant provision
      ```
      vagrant up
      ```
    This autmatically provisions as stated in the Vagrantfile.
   
      ```
      vagrant provision
      ```
 4. After the play runs to completion, yoou can access the app through the browser
      [http://localhost:3000](http://localhost:3000)
      This is made possible by the forwarded ports added in Vagrantfile
      ```
      config.vm.network "forwarded_port", guest: 3000, host: 3000, protocol: "tcp"
      config.vm.network "forwarded_port", guest: 5000, host: 5000, protocol: "tcp"
  
      ```
 5. Add products to the app and confirm data persistence
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
    
    1. Deploy the resource to the cluster
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
        
  ## View Deployed app
  ```
   http://EXTERNAL_IP
  ```
  ---
