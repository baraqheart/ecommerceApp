## kubernetes best practices

1. use of tags 
2. Tcp probes
a. liveness probe is used to know and handle crashed containers using the code, 
   after the pod has been create
   
   ```
   InitialDelaySeconds: 5
   livenessProbe:
     periodSeconds: 5 
     exec: 
       command: ["/bin/grpc_health", "-addr=:8080"]
   ```
    
b. Readiness probe helps kubernetes know the app is ready to recieve traffic during startup process
   ```
   
   readinesProbe:
     initialDelayseconds:5
     periodSeconds: 5
     exec:
       command: ["/bin/grpc_health", "-addr=:8080"]
    ```
add the env variables to the container

```
- name: DISBALE_TRACING
  value: "1"
- name: DISBALE_PROFILER
  value: "1"
- name: DISBALE_DEBUGGER
  value: "1"

```

 c. HTTP probes: kubelet sends an HTTP request to specified path and port,
 checking application endpoint to determine is application is healthy or not

 ```
 httpGEt:
   path: /health
   port: 8080

command exec or tcpsocket or http probes on port which tries to establish a connection the port specified, then the application is consider to be healthy

3. Resource management
using requests and limits, could be used to prevent an app taking off other pods in your cluster, hereby causing bigger issues 

```
resources:
  requests:
    cpu: 100m
    memory: 64Mi
  limits:
    cpu: 200m
    memory: 128Mi
```

4. Elimanate Nodeport
nodeport promotes vulnerabiliby in your cluster, this should be avoided at all cost

use internal services like clusterIP and Loadbalancer

5. Use more than 1 replica count
this promotes availability of your app

6. replicate your pods on multiple nodes this dramatically increased availability

7. use labels

8. organize your resources in namespaces this also  promotes security, by using roles and role bindings

9. scan third party images to determine vulnurabilities in your clusster

10. update kubernetes versions node by node to prevent application down time