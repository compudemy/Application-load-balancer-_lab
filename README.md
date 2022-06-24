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




