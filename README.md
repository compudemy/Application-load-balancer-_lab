# Application-load-balancer-_lab

How Application Load Balancer works
When a client makes a request to our application, the listeners in our AWS Application Load Balancer will receive requests matching the protocol and port we configure. The receiving listener will evaluate the incoming request against the rules we specify, and if applicable, will route the request to the appropriate target group. We can use an HTTPS listener to offload the work of TLS encryption and decryption to our load balancer. Healthy targets in one or more target groups receive traffic based on the load balancing algorithm, and the routing rules we specify in the listener.

Create an EC2 instance
In order to create a load balancer, we need to have EC2 instances. First, we will log in to our AWS console and then type EC2 in our Services tab. From the left pane, we will click on instances. Currently, we don't have any instances.

![image](https://user-images.githubusercontent.com/103466963/175605530-564dca02-73eb-4e15-bc1c-18a56282ea33.png)

Now we will click on Launch instances. The creation of an EC2 instance involves seven steps. We will see each of them one by one.

 




