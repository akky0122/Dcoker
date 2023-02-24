Step 1: Install Docker

    sudo yum update -y                          #This command updates the package list
    sudo amazon-linux-extras install docker     #This command installs Docker
    sudo service docker start                   #This command starts the Docker service
    sudo usermod -a -G docker ec2-user          #This command adds the ec2-user to the docker group to allow running Docker commands without using sudo


Step 2: Configure Docker daemon:

    sudo vi /etc/docker/daemon.json

        #Add the following content to the file:

    {      
      "dns": ["8.8.8.8", "8.8.4.4"]             #This example adds Google's DNS servers to Docker daemon configuration. You can add other configuration options as requi                                                red.
    }

        #Save and exit the file. Then, restart the Docker service:
        
        sudo service docker restart

Step 3: Create Dockerfile:

        #Create a new file named Dockerfile in your project directory using a text editor. Add the following content to the file:

    FROM ubuntu:latest
    RUN apt-get update && apt-get install -y nginx
    COPY index.html /var/www/html/
    EXPOSE 80
    CMD ["nginx", "-g", "daemon off;"]

        #This Dockerfile will create a Docker image based on the latest Ubuntu version, install nginx web server, copy the index.html file to the web server root directory, expose port 80, and start the nginx server.


Step 4: Build Docker image:
        
        #Navigate to the directory containing the Dockerfile and run the following command:
    
    sudo docker build -t my-nginx-image .
    
        #This command will build the Docker image with the name "my-nginx-image" using the Dockerfile in the current directory.


Step 5: Run Docker container:

    sudo docker run -p 80:80 my-nginx-image
    
        #This command will start a Docker container from the "my-nginx-image" Docker image, map the host port 80 to the container port 80, and run the nginx server.


Step 6: Publish Docker image:

        #To publish the Docker image to a registry such as Docker Hub, you need to tag the image with your Docker Hub username and repository name and then push the image to the registry.

    sudo docker login                                           #command logs in to Docker Hub
    sudo docker tag my-nginx-image username/my-nginx-image      #command tags the Docker image with the username/my-nginx-image name
    sudo docker push username/my-nginx-image                    #command pushes the image to Docker Hub. Replace "username" with your Docker Hub username.

    

