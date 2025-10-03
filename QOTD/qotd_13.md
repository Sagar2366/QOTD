Difficulty: Moderate
Tech Stack: Docker, Jenkins
Question: Imagine you are using Jenkins and Docker together in a CI/CD pipeline. During a production deployment, you noticed that the Jenkins job failed due to Docker's 'image not found' error. How would you go about investigating this issue and what steps would you take to resolve it?
Hint: Think about how Docker images are built and stored, and how Jenkins retrieves them. You might want to consider if the Docker image was properly pushed into the Docker registry and also check Jenkins logs for more detailed error information.
Answer: There could be several reasons why you're encountering the 'image not found' error when trying to deploy using Jenkins and Docker. Here are the steps you can take to troubleshoot:

1. Check Jenkins Logs: Start with identifying the exact error message from Jenkins logs, it would provide more details about the issue. If Jenkins failed to find the Docker image, the issue could be with incorrect image name or tag.

2. Verify Docker Image Name: Cross-check the Docker image repository name and tag against your Docker registry. Ensure you have not made any typo errors or used the incorrect image name or tag in your Jenkins job.

3. Check Docker Registry: Verify that Docker registry server is up and running, you may be unable to pull the image because the server is down.

4. Docker Image Existence: Use 'docker image ls' or navigate to Docker registry to confirm that the Docker image in question exists.

5. Verify Docker Push operation: If the Docker image doesn’t exist, ensure that CI pipeline is correctly building and pushing Docker image to the registry. Re-run the job responsible for the build and push operations if necessary.

6. Proxy Issues: If you're fetching Docker images from a remote repository behind a proxy, make sure that the proxy settings are correctly configured in your environment.

7. Docker Daemon Running: Ensure the Docker daemon is running in the server where Jenkins job is running.

8. Access Privileges: Ensure that Jenkins has required permissions to pull the Docker image.

To resolve the issue:

- Fix any identified typos or mistakes in the Docker image name or tag used in your Jenkins job.
- If Docker image doesn’t exist, fix the failed CI jobs responsible for building and pushing the Docker image.
- If the server is down, bring the Docker registry server back up.
- If permissions are the issue, configure appropriate access rights for Jenkins.

Diagram/Example: Not applicable for this response.