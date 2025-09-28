Difficulty: Complex
Tech Stack: Kubernetes, AWS, Terraform, Jenkins, Ansible, CI/CD
Question: Our website runs on a Kubernetes cluster hosted in AWS. Recently, we've been experiencing brief outages in the middle of the night that last for 5-10 minutes each time. They aren't consistent with the application load, and sometimes they coincide with our nightly job runs. The team looked at logs, but didn't notice any application errors. What are some steps you would take to identify and potentially solve this issue?
Hint: Consider things such as underlying infrastructure issues, Kubernetes configurations and events, network problems, and scheduling of other jobs like backups or maintenance tasks. In AWS specifically, you might also think about EC2 instance types, autoscaling groups, and any capacity issues.
Answer: Given that there were no conspicuous errors in the application logs, the issue might be infrastructure-related. 

1. AWS Monitoring: Check AWS CloudTrail and CloudWatch logs for any kind of API/Operational error associated with the EC2 instances running the Kubernetes nodes. 

2. Kubernetes Events: Use `kubectl describe pods` for any event-driven errors. Kubernetes Events and logs often provide clues about what happened to pods, nodes, and services.

3. Resource Limits: Check if the resource limits of containers or pods are causing the outage. The issues might be due to the kubelet killing the containers/pods due to resource constraints.

4. Autoscaling Groups: Monitor the activities of the EC2 Auto Scaling groups if they have been utilized. Check whether the decrease in load during the night is causing the termination of instances and thereby causing the brief outages as new ones take time to come up.

5. Availability Zones: Validate that the Kubernetes nodes are appropriately distributed across AWS Availability Zones.

6. Network Latency: Validate your network configuration - VPC settings, ingress/egress data, and latency.

7. Nightly Job runs: Analyze the resource consumption of nightly jobs thoroughly. They might be causing an excess drain on specific resources. 

8. Maintenance Tasks: Verify if the outage timing coincides with AWS maintenance windows or during the execution of infrastructure code updates done via Terraform, or configuration changes via Ansible.

9. Scheduling of Backups: If backups are scheduled during the outage times, check if it's causing any resource contention or network bottleneck.

After identifying the issue, solutions could range from adjusting Autoscaling policies, rescheduling nightly jobs, or maintenance tasks to configuring Kubernetes resource allocation more efficiently.

Diagram/Example: Not applicable due to specific scenario and person-to-person difference in the system setup. The diagnosis mentioned might yield varying