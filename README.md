# MERN-WEB-STACK-PROJECT
## Introduction

This is a documentation that explain the implementation, setup, configuration of my MERN stack project (Todo Web App) in AWS cloud. MERN stack is one of the types of web stack that comprises of  MongoDB as the database for application data storage, ExpressJS as the server Web Application Framework for Node.js, ReactJS as the frontend framework for user interface components and NodeJS as Javascritt runtime Environment to run Javascript on a machine.

## PROJECT ARCHITECTURE


> AWS EC2 (Ubuntu 26.04) 
>    
> Backend Configuration
>
> Installing ExpressJS
> 
> Installing MongoDB
>
> MongoDB Database
>
> Testing backend Code without Frontend using RESTful API
>
> Frontend Creation
>
> Create React Componenets




# STEP 1 - PREREQUISITES
1. Login into AWS to create an Ec2 instance (LEMP SERVER) of t3.micro and Ubuntu Server 26.04 LTS (HVM), which was launched in eu-north 1b, using the command 
```
ssh -i <sshkey.pem> Ubuntu@ipaddress
```
![Ec2 ssh Login](<Images/1 ec2 ssh login.png>)
2. Server update and upgrade
```
sudo apt update
sudo apt upgrade
```
![server update](<Images/2- SERVER UPDATE.png>)

# STEP 2 - Backend Configuration


1. Get the location of Node.js software from Ubuntu repositories
```
curl fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
![Location of Node.js](<Images/4- get location of node.js.png>)

2. Install Node.js on the server
```
sudo apt-get install -y nodejs
```
![install nodejs](<Images/5 node.js installation.png>)

3. check for node and npm version
```
node -v
npm -v
```
![node & npm version](<Images/6- node & npm version.png>)

4. Create Todo directory
```
mkdir Todo
```
![Todo directory](<Images/7- create todo directory.png>)

5. Initialize our project to create a new file in the Todo directory using npm init
```
npm init
```
![npm init](<Images/8- todo npm init.png>)


# STEP 3 - Installing ExpressJs

1. Install Express using npm
```
npm install express
```
![express installation](<Images/9- install express.png>)

2.  create new index.js file in the Todo directory
![index.js](Images/10-index.js.png)
![index.js code block](<Images/11- index.js code.png>)

3.  Run/server the server to check if it works
```
node index.js
```
![run server](<Images/14- express webpage.png>)

4.  Add port 5000 to our ec2 inbound rule, so our server and ec2 instance can be able to connect

![port 5000](<Images/13- adding port 5000.png>)

5.  Access server public IP through web browser
```
http://51.20.8.17:5000
```
![express](<Images/14- express webpage.png>)

6.  Create Routes folder tht will define various endpoints that the Todo app will depend on
   ![routes folder](<Images/15- create route directory.png>)

7.  create new Api.js file, using the vim text editor, input the code for Api.js
```
touch Api.js
vi Api.js
```
![create Api.js](<Images/16- create app.js.png>)
![Api.js code](<Images/17 - api.js code file.png>)

# STEP 4 - Installing MongoDB

1. Install Mongodb
```
npm install mongoose
```
![install Mongodb](<Images/18- install mongodb.png>)

2.  create new folder for models, change to the models directory and create a file name Todo.js
```
mkdir models
cd models
touch Todo.js
```
![models](<Images/19- create models & todo.js.png>)

3.  Open the newly created Todo.js file and input the code.
   ![Todo.js code](<Images/20- todo.js code file.png>)

4.  change to routes directory and update the Api.js code
```
cd routes
vim api.js
```
![routes folder](<Images/21- update api.js.png>)
![Api.js code](<Images/22- api.js new code.png>)

# STEP 5 - MongoDB Database

1. Create account on mLab
![create database](<Images/23 mongodb cluster.png>)

2.  Add 0.0..0.0/0 to the the IP Access List to be able to serve data from anywhere
   ![.](<Images/24 access mongodb.png>)
   ![.](<Images/24b access mongodb.png>)

3.  Create MongoDB database and collection inside mLab
  ![Database](<Images/25 todo db creation.png>) 

4.  Create .env file in the Todo directory and input the code using vim.
```
touch .env
vi .env
```
![.env](<Images/26 .ev file.png>)
![.env code](<Images/27 .env code block.png>)

5.  Update the Index.js file to reflect the use of .env
![index.js](<Images/28 update index.js code.png>)

6.  Start server
```
node index.js
```
![database connected](<Images/29 database connected successfully.png>)

# STEP 6 - Testing backend Code without Frontend using RESTful API

1. Create a GET request to API on 
```
http://51.20.8.17:5000/api/todos
```
![postman](<Images/30- postman rsponse 1.png>)

2.  Create a POST task 
![post task](<Images/31- first post task.png>)

3.  Verify task using GET response
![GET](<Images/32- verify task on get.png>)

4.  Got to mLab and confirm if the task  added are showing in the database
![mLab](<Images/33 verify task on Mlab.png>)

5.  Delete task
![delete task](<Images/34-delete task.png>)

# STEP 7 - Frontend Creation

We need to create a user interface for a web client to interact with the application via API

1.  Create frontend of the To-do app in the same root directory as the backend code.
```
npx create-react-app client
```
![react frontend](<Images/35- create frontend directory.png>)

2.  installing the react app dependencies
![react concurrently](<Images/36-install concurrently.png>)
![nodemon](<Images/37-install nodemon.png>)

3.  Open the Package.json file and input the code
```
vi package.json
```
![package.json](<Images/38- editting package.json file.png>)

4.  Configure proxy in package.json in the client directory
```
cd client
vi package.json
```
![package.json](<Images/39- client folder.png>)
![proxy](<Images/40-adding proxy.png>)

5.  run server app
```
npm run dev
```
![server app](<Images/41- app running error.png>)
The server was unable to run due to an error in the Package.json file. 
6.  Edit package.json file
![package.json](<Images/43-correct package.json file.png>)
After making correction/editing the package.json file, we can noe rerun the server app.
![app running](<Images/44- app running.png>)
App running successfully on port 3000

7.  open port 3000 on the EC2 by adding it to the security group inbound rules
![port 3000](<Images/45-port 3000.png>)

# STEP 8 - Create React Componenets

1.  Go to the src directory, create a newdirectory called components and create files named, Input.js, ListTodo.js and Todo.js.
```
cd src
mkdir components
touch Input.js ListTodo.js Todo.js
```
![src comp](<Images/46-create src components.png>)

2.  Input the Input.js code
 ![input.js](Images/47-input.js.png)

 3. Go to the clients folder and install Axios
```
cd ..
cd ..
npm install axios
```
![Axios](<Images/48-install axios.png>)
   
4.  Input the ListTodo.js code
![ListTodo.js](Images/50-ListTodo.js.png)

5.  Input the Todo.js code
![Todo.js](<Images/51- Todo.js.png>)

6.  Make an adjustment to the App.js file in the the src folder   
![App.js](<Images/52-change directory for app.js.png>)
![App.js](Images/52-app.js.png)

7.  input the App.css code
![App.css](<Images/53-app.css code.png>)

8.  Input the Index.css code
![Index.css](Images/54-index.css.png)

9.  Go back to the root directory, which is the Todo directory and start the server
```
npm run dev
```
![run server](<Images/55- server running successful.png>)

10. Confirm if the server runs using the web browser
![Todo web](<Images/56- Todo web running.png>)

11. Add more task
![Todo](<Images/57- Todos.png>)
12. Verify on the mLab if the database stores correctly
![mLab](<Images/58-verify on mlab.png>)

# Conclusion
## Conclusion

Building this MERN application provided practical experience in developing, deploying, and managing a full-stack web application on AWS. It serves as a solid foundation for future projects involving cloud computing, DevOps, and scalable web application development.