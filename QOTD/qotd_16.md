Difficulty: Moderate
Tech Stack: Docker, Kubernetes, Jenkins, CI/CD
Question: Suppose you have an application that's containerized with Docker and deployed on a Kubernetes cluster. The application is built and deployed using a Jenkins pipeline. Now, one day your application starts experiencing high latency and the response time increases dramatically. Where do you start troubleshooting and how do you track down the issue?
Hint: You might want to start with monitoring tools. Think about what metrics you would look at and how you would assess the health of your Kubernetes cluster and the containerized application. How would you use Jenkins' logs in your troubleshooting process?
Answer: I would start by looking at the Prometheus metrics, which is a monitoring tool often used in Kubernetes environments. The metrics could present CPU usage, memory usage, disk I/O, and network traffic, which might shed light on where the bottleneck is. If I notice any spike in resource usage, it may signal a problem with the application code or cloud resource allocation.

Next, I would check the Kubernetes (K8s) cluster health. For this, I would first look at the pod statuses by running “kubectl get pods”. If there are crashes or never starting pods, it’s likely to impact the application performance. Next, checking the nodes by running “kubectl get nodes” would help identify any underlying node issues such as a memory leak or CPU throttling.

Then move on to application logs and Docker logs to see if there are any error messages or exceptions. These logs can be accessed within the Kubernetes dashboard or can be port-forwarded via “kubectl logs” or “kubectl logs --follow [pod_name]” commands.

Next, I'd check Jenkins build logs to evaluate if there were any recent changes deployed that might have impacted the app, or if there was a failure in the CI/CD pipeline that caused a faulty deployment.

Finally, if all this does not lead to the root cause, I would use tracing tools such as Jaeger to trace the request flow and identify slow services or methods within the application.

Diagram/Example: Unfortunately, a diagram or specific example would not be practical in this context as the troubleshooting steps are highly dependent on the specific system and issue. However, the sequence of steps listed above should provide a good outline.