Difficulty: Moderate
Tech Stack: Docker, Jenkins, CI/CD
Question: You're working in a project where the development team follows Agile methodologies and they are constantly delivering new features. The organization has decided to use Docker for application deployment and Jenkins for CI/CD. So, everytime a developer pushes the code to the repository, Jenkins build process gets triggered and Docker image should get created. Can you explain a high level process of how you'd integrate Docker with Jenkins to ensure that a new Docker image is built every time a build is triggered?
Hint: Think about how you'd configure Docker in a Jenkinsfile and the necessary commands you'd need to build and tag Docker images. Consider discussing how you'd manage Docker daemon access permissions for Jenkins too.
Answer: To ensure that a new Docker image is built every time a build is triggered in Jenkins, we need to first install the "Docker plugin" into Jenkins. This plugin allows Jenkins to build and use Docker images directly.

We'll also need to configure Jenkins to have access to the Docker daemon. This usually involves adding the Jenkins user to the 'docker' group, depending on your security requirements.

Within the Jenkins job configuration, we specify the Dockerfile path and Docker image name under the "Docker Build and Publish" option, which are necessary to build and tag Docker images. 

The high-level process, when code is pushed to the repository, could look something like this:

1. A developer commits and pushes code to the repository, triggering the Jenkins build job via a webhook.

2. Jenkins server, which has access to the code repository, pulls the latest committed code.

3. Jenkins follows the Build, Publish, Deploy steps defined in the Jenkinsfile.

4. In the 'Build' stage, Jenkins makes use of a Dockerfile in the codebase. It initiates a Docker Build command (`docker build -t my-app:1.0 .`) to create a Docker image.

5. In the 'Publish' stage, the Docker image created in the previous step is tagged with the build number or other identifiers for traceability (`docker tag my-app:1.0 my-app:tag`). Then, it is pushed to a Docker Registry (like DockerHub, ECR, GCR) using `docker push my-app:tag`.

6. In the 'Deploy' stage, this new Docker image is pulled from the Docker Registry and deployed to the respective environment (test, staging, production etc).

Keep in mind that these stages can vary largely based on your specific project and organizational needs, and the Jenkinsfile should be modified accordingly.
