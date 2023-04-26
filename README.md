Autoscaling and Load Balancing 

These are the following steps, to create an Autoscaling and Load balancing group using our App AMI so if if one instance crashes we will have another within
300 seconds. 

Step 1

Go on the EC2 dashboard from the AWS homepage. And Launch a Template which you may use for the ASG further on.

- Click Create Template

Step 2

- Once your inside the creation, edit your name to a similar one as illustrated below so it can be easy to navigate.
- Click the Auto-scaling guidance so you may use the template for help.

Step 3

- Make sure to use Ubuntu 18.04 from the AMI image as other versions may not work.

Step 4

- Follow the normal procedure as follows:
- 1. Use t2 micro since our CPU outtage and sub instances we create isn't going to override the capacity.
- 2. Key-pair name e.g tech221

Step 5

Network Settings

- Use your previous security group created for your app, as it will include the HTTP and SSH ports.

Step 6

- Scroll down and edit the User data configuration under the advanced settings with the following commands.

    #!bin/bash
    sudo apt update -y
    sudo apt upgrade -y
    sudo apt install nginx -y
    
 Create the template
 
 Auto Scaling Group 
 
 Auto scaling group is 
