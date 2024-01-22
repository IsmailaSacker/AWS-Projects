**This project demonstrates how you can create VPC that can be used server in production environment. This will help improve resilience, by deploying servers in two Available Zones, by using Auto Scaling group and an Application Load Balancer. To strengthen the security, we will deploy the servers in a private subnet.
The servers receive requests through the load balancer, and they also connect to the internet by using NAT Gateway. To improve resiliency, we will deploy NAT Gateway in both Availability zones. An application will be deployed on the ec2 instance in the private subnet. User will access the application through the load balancer. The load balancer will then forward the request to application on the ec2 instance.
The main services for this project are: EC2 instance, Auto scaling group, Load balancers and Target group.**

![Alt text](/public_and_private%20subnet%20project/simple_image.png)

**Let first dive into the project.**

## 1. We create VPC that will contain our resources like the ec2, subnet, load balancers, auto scaling group, security groups, jum server.

    - a. Below is the VPC configuration. We choose VPC and more to automatically create the subnets, the NAT gateway and the IG gateway.

## 2. We created the Auto scaling group. But we need to first create a lunch template because we will need it in the auto scaling group creation.

    - a. Below is the configuration of the lunch template.

**At all the above is configured correctly, you click on the create launch template button to create the launch template.** - Below is the configuration of the Auto scaling group.

    - click on the next button to move on to next page.

    - click on the next button to move on to next page.

    - click on the next button to move on to next page.

    - click on the next button to move on to next page.

    - click on the next button to move on to next page.

- On the next page you review all the configuration you did and click on create Auto scaling group and confirm if it’s created successfully.

## 3. We now move on to create the jump server that we will use to login to the ec2-instance created by the auto scaling group. We move to the ec2 dashboard to create the instance. Below is the configuration of the jump server.

    - click on the launch instance button to create the jump server.
    - Now lets confirm if the auto scaling group has created the ec2-instances and the jump server by navigating to the dashboard.

## 4. Let’s go ahead and login to the jump server and connect to the ec2 instances in each private subnet. In my case am using mobaxterm terminal client.

- a. Below command is what I used to login to jump server

  - i. ssh -i ish_xxx.pem ubuntu@34.79.90xxx

- b. We proceed to login to the ec2 instance in each availability zone using the same key_pair file.

## 5. We now deploy the application on each ec2 instance in each availability zone and run python http server on each ec2 instance as well.

- a. Deploy the application on each instance.

  - i. Create an html file using vim editor and put in your html blocks of code in it and save it.
    - vim index.html

- The above is done on each ec2 instance.
- b. Let’s run python http server on port 5000 on each ec2 instance by using the below command.
  - i. python3 -m http.server 5000

## 6. Now that the applications are deployed on each ec2 instance. We can go ahead to create the load balancer that will distribute the traffic to each ec2 instance.

- a. Before we create the load balancer, we need to create the target group that will be used by the load balancer. Below is the configuration of the target group.

- click on the next button to move on to next page.

- click on the include as pending below button to add the select instance to the targets and click on the create target group button to create the target group.

- Now that the target is created, let go ahead to create the load balancer.
  - a. We select the Application Load Balancer. Below is the configuration.

**Make sure the target group you created is selected on the required place before you click on the create load balancer.
Now that all the configurations and the resource are created, let’s test the application we deploy on the ec2 instances. The application can be tested by copying the ARN of the load balancer and pasting it on the browser to check if you can access the application.**

**Below shows that my applications on each ec2 instance are working perfectly.**

**If you are able to reach this step, then well done. You have done a great job. Hurray.**
