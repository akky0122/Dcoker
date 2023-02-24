Step 1: Create a new directory for your Node.js application.
   
     mkdir NodejsApp


Step 2: Create a new file named "package.json" in the directory(NodejsApp) and add the following contents:
    vim package.json

{
      "name": "my-node-app",
      "version": "1.0.0",
      "description": "My Node.js application",
      "main": "index.js",
  
   "dependencies":
     {
          "express": "^4.17.1"
     },

   "scripts":
     {
         "start": "node index.js"
     },

  "repository":
     {
         "type": "git",
         "url": "https://github.com/your-username/my-node-app.git"
     },
 
  "license": "MIT"
}


Step 3: Install Node.js using the NodeSource repository. Here are the steps:
    
        #Install the NodeSource repository:

    curl -sL https://rpm.nodesource.com/setup_14.x | sudo bash -


        #Install Node.js:

    sudo yum install -y nodejs


        #Run the following command in the directory to install the dependencies:

    npm install
    
    
        #To check the version
    
    npm -v


Step 4: Create a new file named "index.js" in the directory and add the following contents: 

    vim index.js

        const express = require('express');
        const app = express();

        app.get('/', (req, res) =>
                {
                    res.send('Hello, world!');
                });

        app.listen(3000, () =>
                 {
        console.log('App listening on port 3000');
                 });
   

Step 5: Create a new file named "Dockerfile" in the directory and add the following contents:

        vim Dockerfile
    
    FROM node:14-alpine
    WORKDIR /app
    COPY package*.json ./
    RUN npm install --only=production
    COPY . .
    EXPOSE 3000
    CMD ["npm", "start"]

    ##This file defines a Dockerfile for your Node.js application. It starts with the official Node.js 14 Alpine base image, sets the working directory to "/app", copies the "package.json" file, installs the production dependencies, copies the application code, exposes port 3000, and sets the command to run the application using the "npm start" command.




Step 6: Build the Docker image using the following command:

    docker build -t my-node-app .


Step 7: Run the Docker container using the same command:

    docker run -p 3000:3000 my-node-app


    #This will run the Docker container for your Node.js application and map port 3000 in the container to port 3000 on the host.

    #You should now be able to access your Node.js application by navigating to http://publicip:3000 in a web browser.

