Difficulty: Complex
Tech Stack: Kubernetes, Terraform, AWS
Question: Let's imagine you inherit a complex environment setup. You have 50 microservices running in a Kubernetes cluster hosted on AWS, and the architecture of these microservices keeps changing frequently. The team pushed all these configurations manually in Kubernetes, leading to different versions of configurations, discrepancies, and misconfigurations. How would you design a solution which ensures all the application configuration is version controlled and switchover to new configurations is automatic, minimal risk, and rollback is easiest if things don't go well? Also, while setting up this, what are some of the security checkpoints you should consider to avoid any breaches?
Hint: You might want to consider treating infrastructure as code (IaC) using Terraform, as well as introducing GitOps. Kubernetes inherently supports rolling deployments and rollbacks. Describe your answer considering these points. You should also consider the possibility of sensitive data in config files, role-based access control, and ensuring pipeline security.
Answer: The foremost step is to implement Infrastructure as Code (IaC) using tools like Terraform, which can store the configuration files that describe the infrastructure setup. It will help to standardize each microservice's configuration, decrease discrepancies, and improve reliability.

GitOps should be brought in to automatically apply changes to the live Kubernetes environment whenever changes are pushed to the git repository. A GitOps workflow includes a git repository for storing configurations, a pipeline that triggers a rollout on changes, and a Kubernetes cluster to rollout changes. Git repository acts as the source of truth, ensuring there's a record of all changes, enabling easy rollbacks, and providing an audit trail.

Kubernetes supports rolling updates, which will slowly roll out a change to a small percentage of instances, and if everything seems working, will gradually rollout to other instances. Kubectl rollout command can be used to manage the deployments and rollbacks.

For security considerations:

1. Mask sensitive data: Consider using Kubernetes secrets or external secret management tools like Vault to store sensitive data like passwords, tokens, API keys, etc. These shouldn't be part of plaintext configs.

2. Role-Based Access Control (RBAC): Set up RBAC in Kubernetes to control who can access what resources and perform certain operations.

3. Secure pipeline: The pipeline that detects changes to the git repository and automatically triggers rollouts needs to be secure. Principle of least privilege should be applied, meaning it should only have permissions to perform the necessary tasks.

4. Security Scans: You should ensure that security scanning is part of your pipeline for both your code and docker images.

5. Encryption: Options for both at-rest and in-transit encryption of data should be enabled.

The combination of GitOps with IaC makes it easy to keep track of changes, reduces risk, increases repeatability, and provides mechanisms for