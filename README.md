# Application-load-balancer-_lab

How Application Load Balancer works
When a client makes a request to our application, the listeners in our AWS Application Load Balancer will receive requests matching the protocol and port we configure. The receiving listener will evaluate the incoming request against the rules we specify, and if applicable, will route the request to the appropriate target group. We can use an HTTPS listener to offload the work of TLS encryption and decryption to our load balancer. Healthy targets in one or more target groups receive traffic based on the load balancing algorithm, and the routing rules we specify in the listener.

Create an EC2 instance
In order to create a load balancer, we need to have EC2 instances. First, we will log in to our AWS console and then type EC2 in our Services tab. From the left pane, we will click on instances. Currently, we don't have any instances.

![image](https://user-images.githubusercontent.com/103466963/175605530-564dca02-73eb-4e15-bc1c-18a56282ea33.png)

Now we will click on Launch instances. The creation of an EC2 instance involves seven steps. We will see each of them one by one.

# Step-1: Choose AMI
An Amazon Machine Image is a template that contains the software configuration (operating system, application server, and applications) required to launch our instance. We have different options to choose from AMI either by AWS, user community, or the AWS Marketplace; or we can select one of our own AMIs. For now, we will select Amazon Linux 2 AMI (HVM) - Kernel 5.10, SSD Volume Type. Note that it's free tier eligible.

![image](https://user-images.githubusercontent.com/103466963/175607722-ceafbad4-7f4e-43a2-94df-2255be44c658.png)

# Step-2: Choose Instance Type
Amazon EC2 provides us with a wide selection of instance types optimized to fit different use cases so we can choose one according to our requirements. Instances are virtual servers that can run applications and have varying combinations of CPU, memory, storage, and networking capacity. For now, we will select t2.micro that is free tier eligible.

![image](https://user-images.githubusercontent.com/103466963/175608078-c9253b96-0147-433b-a600-1fbbc49c1534.png)
