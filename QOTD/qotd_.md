Answer: 

To meet the requirements, I would follow below steps:

1. Install Docker: Ensure Docker is installed on the Jenkins server. 

2. Install Jenkins Docker Plugin: Once Docker is successfully installed, install the Docker plugin in Jenkins. This plugin helps in automating building and configuring Docker images.

3. Dockerfile: A Dockerfile is a script that contains collections of commands and instructions which will be automatically executed in sequence in the Docker environment for building a new docker image. Create a Dockerfile that specifies the base image, dependencies, and provides instructions on how your application should be packaged and run. Have a Dockerfile for each application.

4. Jenkins Job configuration: Set up Jenkins jobs for each application. The Jenkins Job must be configured to pull the code from the repository, build the Docker image using the Dockerfile specific to the application, and then run the image in a Docker container.

5. Push the Docker image: Once Jenkins successfully builds and tests the dockerized applications, push the Docker image to a Docker registry.

6. Webhooks: Set up a webhook in your git repository to trigger the Jenkins job whenever there is a new push. Webhooks provide a mechanism to notify Jenkins about code changes, triggering Jenkins job automatically.

7. Pipeline: Create a Jenkins pipeline that comprises of all the above stages i.e., Pull code -> Build Image -> Run Image -> Push Image -> Notify Success/Failure.

Diagram/Example:

A basic Dockerfile might look like this:

```
# Use an official Python runtime as a parent image
FROM python:3.7-slim

# Set the working directory in the container to /app
WORKDIR /app

# Add the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment vari

