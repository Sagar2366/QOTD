Answer: To address the goal of achieving zero downtime during the deployment of microservices to AWS using Jenkins, Docker, and Kubernetes, we can employ the blue/green deployment strategy in our Jenkins pipeline. This approach involves two replicated environments called Blue and Green. We use the Blue environment for active live traffic, and the Green environment is used to roll out a new deployment. 

1. Jenkins pipeline automates the process by triggering a build on receiving the updated code in the Git repository, generating a new Docker image. 

2. The newly built Docker image is then pushed to the Docker registry.

3. Jenkins pipeline will then deploy the new Docker image in the Green environment on Kubernetes.

4. Next, a series of automated tests are performed in the Green environment to validate the deployment.

5. If the tests pass, traffic routing is reconfigured from the Blue environment to the Green environment using Kubernetes service.

6. The Blue environment will be ready for the next deployment. If there is a failure or issue with the Green environment, we can quickly revert the traffic routing back to Blue with zer/(a very small) downtime.

Regarding database schema changes, we can use the concept of "Database Migrations". Here, each change to the database schema is captured as a migration file. These files are version-controlled and applied in order to the database to reach the desired state. During the deployment process, the Migration tool is executed to apply any new migrations. 

If we need to return to a previous application version (Blue environment), we keep “backward compatibility” by making sure changes in the new version don’t disrupt the old one. This could mean not deleting database columns immediately and managing the deprecation time to ensure smooth transitions.

Diagram/Example: 
In this case, a diagram or code example isn't applicable as the processes mentioned are more operational and visualized through the orchestration of multi



Counter: 