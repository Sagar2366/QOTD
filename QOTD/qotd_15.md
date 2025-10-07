Difficulty: Moderate
Tech Stack: Docker, Kubernetes, AWS
Question: You currently have a Dockerized application that you are deploying to a local Kubernetes cluster, but you want to move your deployment to an Amazon EKS cluster. What steps would you take to accomplish this?
Hint: Consider the lifecycle including Docker image storage, EKS configuration (like IAM roles, VPC, Security Groups), as well as Cluster setup and service deployment. You might also want to think about any changes you would need to make in your CI/CD pipeline to accommodate this change.
Answer: 

The following steps outline how to move a Dockerized application from a local Kubernetes cluster to an Amazon EKS (Elastic Kubernetes Service) cluster, while considering the lifecycle, including Docker image storage, EKS configuration, and service deployment:

1. Docker Image Storage: Create a repository in Amazon Elastic Container Registry (ECR), then push the Docker image onto this repository. This includes steps of building the image, tagging it, and pushing it onto the newly created ECR repository.

2. EKS Configuration: Create an Amazon EKS cluster with AWS Management Console or AWS CLI. Consider IAM roles, VPC, and security groups during this setup.
- IAM Roles: Create a new IAM role with the `AmazonEKSClusterPolicy` attached, to be used by the EKS cluster.
- VPC: Configure a VPC according to the EKS requirements. 
- Security Groups: Assign appropriate security groups to control the inbound and outbound traffic to the EKS cluster.

3. Cluster Setup: Run the `aws eks update-kubeconfig` command to update your kubeconfig file with the necessary credentials and endpoint details to access your new EKS cluster.

4. Service Deployment: Use kubectl to apply your application's deployment and service files the same way as on your local Kubernetes setup. You could adjust them before, if required (e.g., if you have hardcoded local IP address or other local-specific parameters).

5. CI/CD Pipeline: Update your CI/CD pipeline to target the new EKS cluster. Integrate it with ECR, so every new pushed Docker image triggers an update in your deployment on the EKS cluster. Using tools like Jenkins or AWS CodePipeline can help automate this.

During all these steps, be diligent on access controls and security best practices, as you're now dealing with a cloud environment that is accessible over the internet, unlike your local setup.

Diagram/Example: 

Unfortunately, due to the format, a diagram or specific code examples can't be provided here. However, all AWS CLI comm