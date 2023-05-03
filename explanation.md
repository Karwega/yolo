Dockerfile directives used in the creation and running of each container.
Docker-compose Networking (Application port allocation and a bridge network implementation) where necessary.
Docker-compose volume definition and usage (where necessary).
Git workflow used to achieve the task.

# Yolomy Microservice Setup (explained)
Yolomy is a business that trades clothing. It has a microservice which helps in running of the business on an online instance. The microservice is divided into two parts of it that work together to assist in the seamless functionality of the service:
    <p>- Client (frontend)</p>
    <p>- Backend</p>
*NOTE: This project has already been bootstrapped*

## 1. Running the client-end and the back-end microservice on your localhost
The instructions are clearly stated in the README.md file of the repository and are illustrated as follows:
* Navigate to the Client folder `cd ../client`
* Run the folllowing command to install the dependencies `npm install`
* Run the folllowing to start the app `npm start`
* Navigate to the backend folder `cd ../backend`
* Run the folllowing command to install the dependencies `npm install`
* Run the folllowing to start the app `npm start`

## 2. Creating the Dockerfile
For the microservice to run accordingly, a Dockerfile should be created in the client directory (*client/...*) as well as the backend directory (*backend/...*). The following steps illustrate how to go about it.
* Choose a base image on which to build each container, preferably, the Alpine for Node.js image variant might, because it provides an overall small image size, and even smaller vulnerabilities count.
* Set the port for mongo_db to `2717:27017` , backend to `5000:5000` and client to `3000:3000`
* Set the appropriate parameters in the Dockerfile and makre sure to include the command `RUN npm install`
* Make sure to include the `CMD [ "npm", "run" , "start" ]` in order to get the service up and running

## 3. Creating and configuring the docker-compose.yml
This file is responsible for the orchestration of the e-commerce platform, as well as pulling of the mongodb image to be used, because the backend functionality requires a mongodb database. The following steps illustrate how to go about it
* Start by specifying the version used by writing `version: "3.9"`
* This file consists of two parts; **services** and **volumes**
* In the services section, configure the mongo_db, client and backend sections
* In the volumes section, configure the mongo_db section
<p>*NOTE: Make sure to include `depends_on: - mongo_db` in the backend section of the services configured*</p>

## 4. Pushing the images to Docker Hub
Once the above procedures are followed, 
* Note the tag names of the created images. If not sure of the tags, run `sudo docker images ls` to list all the images you have.
* Log in to Docker Hub on your computer (if not already done) running `sudo docker login` in terminal. This will prompt you to input your Docker Hub username and password.
* Once logged in and the image names and versions noted, push both the **.../yolo_client:v.0.0.1** and the **.../yolo_backend:v.0.0.1** images to Docker Hub by running `sudo docker push .../yolo_client:v.0.0.1` and `sudo docker push .../yolo_backend:v.0.0.1` respectively.

## 5. Testing the microservice
To confirm correct funtioning of the system, follow the below instructions, and if they run accordingly, the microservice is good to go!
* Open a terminal and run the command `sudo docker compose up` to run the containers from the images. The website of the microservice should be up and running on the local address: <a href="http://localhost:3000/"><font color="blue">http://localhost:3000/</font></a>

* Add a product or two in the site, and refresh the page to confirm that they have been added successfully
