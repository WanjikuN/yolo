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
   
   
   

