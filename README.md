# Lab-2md
1. ## verified the project was still active

<img width="675" height="231" alt="image" src="https://github.com/user-attachments/assets/27825556-9949-46fe-9300-ca7af90ad00f" />

I checked my zone and it was unset and then I changed my zone to `us-east1-b.`   I then double checked that the zone was changed and it was set correctly. 

2. ![](http://localhost:9425/images/019c39a5-c72a-710c-ab55-ec06594fdd1a.png)

created google kubernetes engine-cluster w/3 worker nodes with no failures.

3. ![](http://localhost:9425/images/019c39a7-a1fc-7163-a64b-ebe46ef07029.png)

I have a running cluster named gke-cluster and it’s in region  `us-east1-b.`  and it has 3 nodes.

4. ### Configure kubectl access to the cluster & verify connectivity

![](http://localhost:9425/images/019c3b49-88f8-7487-9dc3-07f6f8e278ce.png)

I utilized the kubectl command line tool to talk with the clusters after getting the auth and connect info. I confirmed that the nodes are ready and have been properly configured.

I also see that in the 2nd line that I used to create the cluster nodes where it exactly created the number of nodes I have.

5. ![](http://localhost:9425/images/019c3b5f-772f-7027-819b-1fb804f3ff61.png)

3 pods were created and they act as a backend web server due to its lightweight nature and smart use of resources as well as client will send Http requests and allows me the opportunity to better understand and focus on the structure within Kubernetes. I can see exactly how pod to pod communication is implemented.

6. ![](http://localhost:9425/images/019c3b65-7a2c-7569-b06f-8b1614bae4b2.png)

The container is successfully running and I am getting a local response. I got this tag to verify it `<p>If you see this page, the nginx web server is successfully installed and working. Further configuration is required.</p>`

7. ![](http://localhost:9425/images/019c3b68-a553-769b-8a67-e49459229ac1.png)

```
kubectl describe pod server | grep IP
```

This code allowed me to locate the internal pod IP assigned by Kubernetes 10.104.2.5

8. ![](http://localhost:9425/images/019c3b76-3a01-75d3-ad42-167e4254791d.png)

I’m confused at this step because I put the prompt and i kept getting a syntax error and I double checked w/the get nodes command to see that the nodes are still there but I couldn’t fix it so I just continued with the rest of the lab. 

```
kubectl exec client -- curl <10.104.2.5>
```

This screenshot was before the error incase you see anything strange:![](http://localhost:9425/images/019c3b7b-0383-772b-af14-f72e5a7c50eb.png)

9. ![](http://localhost:9425/images/019c3b7f-46d8-72ea-9b86-a6360943f598.png)

The service was successfully created.

10. ![](http://localhost:9425/images/019c3b80-e7ce-74dc-846d-b7b936bb207e.png)

Type:  ClusterIP  
IP:    34.118.233.84  
Kubernetes assigned my service an internal IP address and is automatically tracking the pods health.

11. ![](http://localhost:9425/images/019c3b86-b3cc-74ad-aa00-99004f980541.png)I made a dubug pod and conducted service discovery using dns.
12. ![](http://localhost:9425/images/019c3b87-d618-73b5-965f-f8ae7040155f.png)I did see the default html page so dns did correctly resolve the service name and kubernetes forwarded the request to the server pod.
13. I ran the command several times

![](http://localhost:9425/images/019c3b8b-0939-763c-bf40-63235921d394.png)![](http://localhost:9425/images/019c3b8b-0952-75cf-9fc2-9f24af1d9a41.png)![](http://localhost:9425/images/019c3b8b-0970-7153-be41-5a783a291987.png)![](http://localhost:9425/images/019c3b8b-0982-71c8-93cb-34c8eb75b256.png)![](http://localhost:9425/images/019c3b8b-098f-7249-951d-b5f7e4a50896.png)![](http://localhost:9425/images/019c3b8b-099e-7438-8e2b-2283bde371ef.png)<br>

it worked everytime and shows that it was working not with the pod IP but with the service name in actuality.

14. 

![](http://localhost:9425/images/019c3b97-404e-7006-a3fb-5d21c116c390.png)![](http://localhost:9425/images/019c3b97-8166-70e8-830c-baa10c05ac03.png)<br>

The Kubernetes service was deleted which removed the stable endpoint used for communication between pods. The pods were deleted which stopped the running containers. While deleting the GKE cluster, I initially received an error saying that one of the location, zone, or region flags had to be supplied. I checked the cluster list and saw that the cluster was located in the us-east1-b zone. I then asked ChatGPT for help troubleshooting the error and learned that I needed to include the zone flag in the delete command. After running the correct command with the zone included, the cluster was successfully deleted. I verified the cleanup by running the cluster list command, which showed that no clusters remained. This confirmed that all Kubernetes resources and compute instances were removed, preventing additional charges.

### Reflection Questions

1) Before Kubernetes, Docker commands would’ve had to have been utilized in order to manage multiple containers. I would’ve been required to manually start containers, connect them, and create the communication between them manually. Management would become nearly impossible as time goes on due to the face that I would have to maintain everything myself as containers increase.

2) A pod is a group of 1+ containers share resources and storage. Containers inside a pod are made to work as one unit together. Kubernetes treats pods as the smallest deployable unit as containers depend on shared resources and have to run together. Managing pods is better than containers individually because Kubernetes maintains the connection between them and enables them to function properly as one app component.

3) Services are needed because pods can be created, destroyed, or restarted at any time which by default means the IP addresses will change. A stable IP and DNS is what a service provides me so I can get pointed to the right pods at any time. The capability is necessary for microservices architecture because constant communication and reliable networks are a necessity to maintain smooth functionality.

4) DNS-based service discovery in Kubernetes allows pods to communicate with services using service names instead of IP addresses. Kubernetes DNS automatically translates the name into the service’s IP address and then I can get to the right pod I was trying to locate. Service discovery is a core requirement for microservices architecture because services are constantly scaling, restarting, and moving so without it I would need to manually make every update if there were any network changes.

5) After completing this lab, running multiple containerized services managed by Kubernetes is more effective. Kubernetes allows applications to scale easily & resilience is improved because Kubernetes allows applications to scale easily and maintain healthy services stay operational if any containers fail. Service communication is also easier because Kubernetes provides built-in networking and service discovery.
