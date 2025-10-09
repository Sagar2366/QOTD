Difficulty: Moderate
Tech Stack: Kubernetes, Docker
Question: You are deploying a new application using Docker containers which are managed by Kubernetes. After some time you find that your application pod is not running and exits frequently with crash loopback off error. How will you debug this issue?
Hint: Think about common reasons why a container might crash, and the tools Kubernetes and Docker provide for troubleshooting such issues. Start with the 'kubectl' commands that might help you gather more information about the error.
Answer: First, you should understand that a 'CrashLoopBackOff' error in Kubernetes indicates that a particular container is continuously crashing. There could be various reasons why a container might crash such as application-level issues, misconfiguration, or a lack of resources.

To debug this issue, you would want to start by inspecting the events associated with the affected pod. You can do that with the following command:

```bash
kubectl describe pod <pod_name>
```

This will give you an overview of the events that have occurred within the pod, which may include useful error messages. 

Then, you should look at the logs of the crashed container. To get the logs, run:

```bash
kubectl logs <pod_name> --previous
```

--previous flag gives the logs from a pod that has crashed. If your pod has multiple containers, you'll want to specify the container:

```bash
kubectl logs <pod_name> -c <container_name> --previous
```

With this information, you should be able to determine why the container is crashing. It could be an application error, a faulty deployment descriptor, or a misconfiguration in your Kubernetes environment.

In case you still can't fix it, you might want to get a shell to the running container using:

```bash
kubectl exec -it <pod_name> -- /bin/sh
```
This command will prompt a shell where you can execute commands and verify the environment variables, dependencies, storage volumes, etc.

Remember the root cause could range from resource limits, liveness probe failures, to application-level errors or Docker image errors.

Remember to continually implement proper logging within your applications to easily troubleshoot these issues. If the issue is persisting, consider getting support from your team or public communities.