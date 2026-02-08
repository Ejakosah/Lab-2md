# Lab-2md
1. ## verified the project was still active

<img width="675" height="231" alt="image" src="https://github.com/user-attachments/assets/27825556-9949-46fe-9300-ca7af90ad00f" />

I checked my zone and it was unset and then I changed my zone to `us-east1-b.`   I then double checked that the zone was changed and it was set correctly. 

2.<img width="893" height="400" alt="image" src="https://github.com/user-attachments/assets/2c6de137-0f68-4db9-a138-dbde326d8cca" />


created google kubernetes engine-cluster w/3 worker nodes with no failures.

3.<img width="630" height="153" alt="image" src="https://github.com/user-attachments/assets/a17cf59e-e669-4841-a2fc-8c3f2ae66d92" />



I have a running cluster named gke-cluster and it’s in region  `us-east1-b.`  and it has 3 nodes.

4. ### Configure kubectl access to the cluster & verify connectivity

<img width="669" height="145" alt="image" src="https://github.com/user-attachments/assets/b8898deb-c5c5-44d1-bd6d-ec779d5afb0b" />


I utilized the kubectl command line tool to talk with the clusters after getting the auth and connect info. I confirmed that the nodes are ready and have been properly configured.

I also see that in the 2nd line that I used to create the cluster nodes where it exactly created the number of nodes I have.

5. <img width="603" height="295" alt="image" src="https://github.com/user-attachments/assets/2d24ab03-eb6e-4809-a8bf-0cf1bffe3fa1" />


3 pods were created and they act as a backend web server due to its lightweight nature and smart use of resources as well as client will send Http requests and allows me the opportunity to better understand and focus on the structure within Kubernetes. I can see exactly how pod to pod communication is implemented.

6. <img width="713" height="377" alt="image" src="https://github.com/user-attachments/assets/8ae9a40e-c1a4-488e-b7e4-421248802bf2" />


The container is successfully running and I am getting a local response. I got this tag to verify it `<p>If you see this page, the nginx web server is successfully installed and working. Further configuration is required.</p>`

7.<img width="645" height="64" alt="image" src="https://github.com/user-attachments/assets/7bde52d1-e091-40b3-95ab-1905a9abbd4a" />


```
kubectl describe pod server | grep IP
```

This code allowed me to locate the internal pod IP assigned by Kubernetes 10.104.2.5

8.<img width="587" height="108" alt="image" src="https://github.com/user-attachments/assets/ead60906-5f11-4ed3-8744-ad363fe27d2f" />


I’m confused at this step because I put the prompt and i kept getting a syntax error and I double checked w/the get nodes command to see that the nodes are still there but I couldn’t fix it so I just continued with the rest of the lab. 

```
kubectl exec client -- curl <10.104.2.5>
```

This screenshot was before the error incase you see anything strange:<img width="518" height="560" alt="image" src="https://github.com/user-attachments/assets/73041ae4-2349-41d9-aa55-efa9fcb60ef0" />


9. <img width="802" height="299" alt="image" src="https://github.com/user-attachments/assets/037bc4fd-340d-424d-be4a-eccf124d3d7d" />


The service was successfully created.

10.<img width="785" height="310" alt="image" src="https://github.com/user-attachments/assets/b8a6314c-91da-4252-b755-8b2966aedcc8" />


Type:  ClusterIP  
IP:    34.118.233.84  
Kubernetes assigned my service an internal IP address and is automatically tracking the pods health.

11. <img width="868" height="499" alt="image" src="https://github.com/user-attachments/assets/1884a76f-bb36-46d5-bf32-219b9621b39c" />
 I made a dubug pod and conducted service discovery using dns.
12. <img width="843" height="495" alt="image" src="https://github.com/user-attachments/assets/a8763860-5ef7-44a6-a2bc-d56fd5eb9c8f" />
 I did see the default html page so dns did correctly resolve the service name and kubernetes forwarded the request to the server pod.
13. I ran the command several times

<img width="846" height="459" alt="image" src="https://github.com/user-attachments/assets/010b0ade-7832-4dfc-93a6-bcc008930da9" />  <img width="882" height="463" alt="image" src="https://github.com/user-attachments/assets/a2c87c25-39eb-41fc-8720-0df9fec2033a" />  <img width="849" height="464" alt="image" src="https://github.com/user-attachments/assets/debe9e37-73e9-4732-a903-277725fd4fe9" />  <img width="840" height="460" alt="image" src="https://github.com/user-attachments/assets/d469fa6f-38d2-4798-b588-fc58d4bce255" /> <img width="859" height="463" alt="image" src="https://github.com/user-attachments/assets/372d1885-7e73-4a28-9496-6736d8ca6dc5" />


it worked everytime and shows that it was working not with the pod IP but with the service name in actuality.

14. 

<img width="573" height="363" alt="image" src="https://github.com/user-attachments/assets/e8cd340c-e18a-42dd-9ad3-fb45ff45d359" />  <img width="532" height="76" alt="image" src="https://github.com/user-attachments/assets/5d360aba-ce69-41d4-b121-45b30a46b94c" />


The Kubernetes service was deleted which removed the stable endpoint used for communication between pods. The pods were deleted which stopped the running containers. While deleting the GKE cluster, I initially received an error saying that one of the location, zone, or region flags had to be supplied. I checked the cluster list and saw that the cluster was located in the us-east1-b zone. I then asked ChatGPT for help troubleshooting the error and learned that I needed to include the zone flag in the delete command. After running the correct command with the zone included, the cluster was successfully deleted. I verified the cleanup by running the cluster list command, which showed that no clusters remained. This confirmed that all Kubernetes resources and compute instances were removed, preventing additional charges.

### Reflection Questions

1) Before Kubernetes, Docker commands would’ve had to have been utilized in order to manage multiple containers. I would’ve been required to manually start containers, connect them, and create the communication between them manually. Management would become nearly impossible as time goes on due to the face that I would have to maintain everything myself as containers increase.

2) A pod is a group of 1+ containers share resources and storage. Containers inside a pod are made to work as one unit together. Kubernetes treats pods as the smallest deployable unit as containers depend on shared resources and have to run together. Managing pods is better than containers individually because Kubernetes maintains the connection between them and enables them to function properly as one app component.

3) Services are needed because pods can be created, destroyed, or restarted at any time which by default means the IP addresses will change. A stable IP and DNS is what a service provides me so I can get pointed to the right pods at any time. The capability is necessary for microservices architecture because constant communication and reliable networks are a necessity to maintain smooth functionality.

4) DNS-based service discovery in Kubernetes allows pods to communicate with services using service names instead of IP addresses. Kubernetes DNS automatically translates the name into the service’s IP address and then I can get to the right pod I was trying to locate. Service discovery is a core requirement for microservices architecture because services are constantly scaling, restarting, and moving so without it I would need to manually make every update if there were any network changes.

5) After completing this lab, running multiple containerized services managed by Kubernetes is more effective. Kubernetes allows applications to scale easily & resilience is improved because Kubernetes allows applications to scale easily and maintain healthy services stay operational if any containers fail. Service communication is also easier because Kubernetes provides built-in networking and service discovery.
