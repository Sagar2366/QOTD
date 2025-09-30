Difficulty: Moderate
Tech Stack: Docker, Kubernetes
Question: You are working on a production Kubernetes cluster and you find that one of the applications is getting killed by itself randomly. The application doesn't log anything that suggests any error. As a SRE, what steps would you take to diagnose the issue and fix it?
Hint: Think about using Kubernetes built-in debugging tools, checking system resource utilization, and validating the application's configuration. Kubernetes Events and pod's status could be very beneficial.
Answer: I would approach the issue using the following steps:

1. **Checking the status of the pods**: The status of pods can provide a lot of details about the application. Using the `kubectl get pods` command will provide information about the status of all pods, and `kubectl describe pod [pod name]` will provide the events and details associated with a particular pod. 

2. **Checking Kubernetes Events**: Kubernetes events are a resource type in Kubernetes that are automatically created when other resources have state changes, errors, or other messages to report. These can be accessed by the `kubectl get events` command. 

3. **Checking system resource utilization**: If the pods are getting OOMKilled, it might be because the application is trying to consume more memory than it’s allotted. If the system runs out of resources, it might also kill off processes to free up resources. The `kubectl top pods` command can be useful to check the resource utilization.

4. **Look at the pod's logs**: Even if the application is not logging errors, Kubernetes might. Look for warning or error messages. You can use `kubectl logs [pod name]` to check the logs.

5. **Validating application’s configuration**: There could be errors in the PodSpec that might be causing unexpected kills. Running a linter on the Kubernetes configuration files could help identify these types of errors.

Diagram/Example:
```shell
$ kubectl get pods
$ kubectl describe pod my-pod
$ kubectl get events
$ kubectl top pods
$ kubectl logs my-pod
```
Keep in mind the above steps would vary based on the actual issue and more steps might be required for a complete diagnosis.