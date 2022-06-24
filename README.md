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

# Step-3: Configure Instance
Here we will configure the instance according to the requirements of the application. Through this, we can launch multiple instances from the same AMI, request Spot instances to take advantage of the lower pricing, assign an access management role to the instance, assign a VPC in which the instances will reside, and more. For now, we will keep all the configurations to default except for User Data under Advanced Details. We will set User Data to the following.

![image](https://user-images.githubusercontent.com/103466963/175608555-bc405f4c-4afd-433b-b801-1857834bf62c.png)

# Step-4: Add Storage
Here we will define storage device settings for our EC2 instance. We can attach additional EBS volumes that are durable, block-level storage devices that we can attach to your instances and instance store volumes that are ideal for temporary storage to our instance, or edit the settings of the root volume. For now, we will keep the configurations to default.

![image](https://user-images.githubusercontent.com/103466963/175608902-18142e29-d692-4f7c-8852-916947b8f04b.png)

# Step-5: Add Tags
A tag consists of a case-sensitive key-value pair. Here we will define a tag with key Name and value My First EC2 Instance.

![image](https://user-images.githubusercontent.com/103466963/175609013-9f5a288b-2c07-4e57-8037-06eda69e99f3.png)


# Step-6: Configure Security Group
Here we can create a new Security Group that is a set of firewall rules that control the traffic for your instance or select from an existing one below. We can add rules to allow specific traffic to reach our instance according to the requirements of the application. For example, if we want to set up a web server and allow Internet traffic to reach our instance, we will add rules that allow unrestricted access to the HTTP and HTTPS ports. Here we have created a new Security Group launch-wizard-1 and allowed unrestricted access to HTTP ports only.

![image](https://user-images.githubusercontent.com/103466963/175609121-cdaa852f-65ea-4101-96db-5b68e06d1c34.png)

Step-7: Review your configuration
Here we will review the instance launch details we configured earlier. We can also go back to edit changes for each step if needed.

![image](https://user-images.githubusercontent.com/103466963/175609197-7567a473-22da-4bb2-9bc8-f632ba5da7fd.png)

Now we will click Launch to assign a key pair to our instance and complete the launch process. Note that we can either create a new key pair or use an existing one. Here we have used an existing key pair EC2 Tutorial.

![image](https://user-images.githubusercontent.com/103466963/175609407-f3214f47-4fb9-49be-bd95-a594a90a8476.png)

Now we will repeat the same steps for two more EC2 instances. After a few minutes, we can see that all our three instances are in the Running state.

 ![image](https://user-images.githubusercontent.com/103466963/175609549-eebf9058-b6c3-4e90-9f31-243a4d671ca1.png)

Create an AWS Application Load Balancer
From the left pane under Load Balancing click on Load Balancers. Here we can find four types of Load Balancers that are Application Load Balancer, Network Load Balancer, Gateway Load Balancer, and Classic Load Balancer(previous generation). We will create an Application Load Balancer for our tutorial.


![image](https://user-images.githubusercontent.com/103466963/175609675-f7e8a3e4-8beb-42c4-b9de-b923b4211949.png)

![image](https://user-images.githubusercontent.com/103466963/175609760-f235a179-c2c0-4b75-b6ec-859c73fc3674.png)

# Step-1: Basic Configuration
Here we will provide the name of our Load Balancer i.e. My-Test-ALB. We will keep it to be Internet-facing as we want our load balancer to route requests from clients over the internet to target that in our case will be EC2 instances. We can select the type of IP addresses that our subnets will use, for now, we will leave it to IPV4.

 ![image](https://user-images.githubusercontent.com/103466963/175610402-de1a52ee-511f-4424-98a1-9af2af22826b.png)


# step-2: Network Mapping
Here we will select at least two Availability Zones and one subnet per zone so that the load balancer will route traffic to targets in these Availability Zones only. We will select us-east-2a, us-east-2b, and us-east-2c and one subnet in them accordingly.

![image](https://user-images.githubusercontent.com/103466963/175610564-f1571f0c-7928-4f30-bae6-8d6c75f6bdfa.png)

# Step-3: Security Groups
Here we can either create a new Security Group or choose from the existing ones. We will use the same Security Group i.e. launch-wizard-1 which we created while configuring our EC2 instance.

![image](https://user-images.githubusercontent.com/103466963/175610702-8fa272a0-151f-403a-89ac-8f5c82cdde43.png)

# Step-4: Listeners and Routing
A listener is a process that checks for connection requests, using the protocol and port we configure while creating our AWS Application Load Balancer. Traffic received by the listener is then routed per our specification. Here we can either create a new Target Group or choose from the existing ones. For creating a new Target Group we will click on Create a target group. Note that here traffic on port 80 will be forwarded to the Target Group created.

![image](https://user-images.githubusercontent.com/103466963/175610830-1344b45b-037e-4114-9c81-1806d4e78ad4.png)

First, we will specify group details. Note that our load balancer will route requests to the targets in a target group and performs health checks on the targets as well. Targets can be of different types such as Instances, IP addresses, Lambda function, and even an AWS Application Load Balancer. We will keep our target to be Instances that we created above.

![image](https://user-images.githubusercontent.com/103466963/175610937-badc9ec9-3637-47ad-8939-9fc5185b72d9.png)

Here we will provide the name of our Target Group. In our case, we will keep it to My-Test-Target-Group.

![image](https://user-images.githubusercontent.com/103466963/175611016-2a1e8a18-a102-4be1-9c4a-8567c224b0f9.png)

We will keep the remaining configurations as it is. Note that here we can also set the value of Unhealthy threshold, Timeout, and Interval for health checks according to our requirements. Currently, we will keep them to default values. Now we will click on Next.

![image](https://user-images.githubusercontent.com/103466963/175611359-e887201d-b7ad-472f-a945-d6968d0a2270.png)
 
![image](https://user-images.githubusercontent.com/103466963/175611424-2f917315-7997-4aef-bf17-96aa9ed48a79.png)

Now the next step in the creation of Target Group is to register targets. We must register our targets to ensure that our AWS Application Load Balancer routes traffic to this target group. Here we can see the instances we created initially. Now we will click on Include as pending below to register them.

![image](https://user-images.githubusercontent.com/103466963/175611541-0c9ba124-55a7-4a10-9b8c-534bce666650.png)

Then we will click on Create target group.

![image](https://user-images.githubusercontent.com/103466963/175611595-72240163-89d0-41b0-885b-ff4fa770f2fe.png)


Now our Target group can be viewed in the list of available Target Groups.

![image](https://user-images.githubusercontent.com/103466963/175611715-67f483fa-4359-45d0-9fba-2e165c2992c9.png)

We will again get back to the configuration of our AWS Application Load Balancer and select the Target Group created.

![image](https://user-images.githubusercontent.com/103466963/175611968-bf8795d2-55f1-4296-9b1d-f7fa51aa2de0.png)

# Step-5: Add Tags
We can also add tags to our load balancer like we did while creating our EC2 instance but we will leave it for now. Tags enable us to categorize our AWS resources so we can more easily manage them.

 # Step-6: Summary
Here we can review and confirm configurations of our load balancer and then click on Create load balancer.
 
![image](https://user-images.githubusercontent.com/103466963/175612522-a7abc548-f58b-40cf-a646-a0e14ad1a54c.png)

# Testing AWS Application Load Balancer

Now our AWS Application Load Balancer can be seen in the list of available load balancers. Here we can view all the details related to the load balancer like Description, Listeners, Monitoring, Integrated Services, and Tags. Note that our load balancer is currently in the Provisioning state.

![image](https://user-images.githubusercontent.com/103466963/175617181-63097fd1-c2a4-44d6-9565-23bd14252d8d.png)

After a while, we can see that the state has changed to Active.

![image](https://user-images.githubusercontent.com/103466963/175617262-3e2e1311-7e0c-4330-8b48-b6e11cc70a4c.png)

Now we will copy the DNS name of AWS Application Load Balancer from the description and enter it in the browser to see the magic happening!

![image](https://user-images.githubusercontent.com/103466963/175617399-6d8f10b0-b0ba-46d0-bdc6-c7752e0b2236.png)

Here we can clearly see from the hostname that the request from the Application Load Balancer is routed to all the three instances we attached to it as Targets.

# Conclusion
In this tutorial, we learned about AWS Application Load Balancer and how it works. Then we walked through the process of creation of EC2 instances as they were to be used as Target Groups for our Application Load Balancer. After that, we created our AWS Application Load Balancer in which we discussed each configuration step briefly. In the end, we witnessed the behaviour of our AWS Application Load Balancer by viewing it distributing traffic to all three instances. 
