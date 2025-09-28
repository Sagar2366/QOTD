Answer: The process of integrating Docker with Jenkins involves a series of steps including setting up Docker, Jenkins, creating a Jenkins pipeline, and managing relevant access permissions.

1. First, make sure Docker is installed and running in the system where Jenkins runs. Obtain necessary permissions to run Docker commands from Jenkins.

2. Install the "Docker pipeline" plugin into Jenkins which provides built-in functionality for building and publishing Docker images.

3. In the Jenkinsfile, developers need to specify the respective stages for the pipeline.

Here is a step-by-step description in a typical Jenkinsfile:

- Stage 'Build': Here the application is built. This may vary based on the application's programming language. For example, a Maven 'clean package' command can be used for a Java application.

- Stage 'Docker Build': In this stage, the Docker image is built using the Dockerfile.
```sh
docker.build("my-app:${env.BUILD_ID}")
```
- Stage 'Docker Push': In this stage, the Docker image is pushed to a Docker registry (like DockerHub).
```sh
docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
    docker.image("my-app:${env.BUILD_ID}").push()
}
```
4. Docker daemon access permissions for Jenkins can be managed through Docker group or by using 'sudo'. The Docker group is a unix group. If you add a user to this group that user gets permissions to run Docker commands. Alternatively, Jenkins can be given sudo access to execute Docker commands.

5. After pipeline configuration, each time developers commit the code, the pipeline gets triggered, the Docker image is built and pushed to the Docker registry.

Diagram/Example: 

The Jenkinsfile might look like the following:
```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application'
                //...
            }
        }

        stage('Docker Build') {
            steps {
                script
