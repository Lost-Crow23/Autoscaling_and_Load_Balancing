<h1>Autoscaling and Load Balancing</h1>

These are the following steps, to create an Autoscaling and Load balancing group using our App AMI so if if one instance crashes we will have another within
300 seconds. 

<h3>Step 1</h3>

Go on the EC2 dashboard from the AWS homepage. And Launch a Template which you may use for the ASG further on.

- Click Create Template

<h3>Step 2</h3>

- Once your inside the creation, edit your name to a similar one as illustrated below so it can be easy to navigate.
- Click the Auto-scaling guidance so you may use the template for help.

<h3>Step 3</h3>

- Make sure to use Ubuntu 18.04 from the AMI image as other versions may not work.

<h3>Step 4</h3>

- Follow the normal procedure as follows:
- 1. Use t2 micro since our CPU outtage and sub instances we create isn't going to override the capacity.
- 2. Key-pair name e.g tech221

<h3>Step 5</h3>

Network Settings 

- Use your previous security group created for your app, as it will include the HTTP and SSH ports.

<h3>Step 6</h3>

- Scroll down and edit the User data configuration under the advanced settings with the following commands.

        #!bin/bash
        sudo apt update -y
        sudo apt upgrade -y
        sudo apt install nginx -y
    
 - Create the template
 
 <h2>Autoscaling Group</h2>
 
 Auto scaling group contains a collection of EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management.

- Create an Auto scaling group under the EC2 dashboard 

<h3>Step 1</h3>

- Create a group name to allign with the template then we use the template we just created prior as this contains our instance (AMI)

<h3>Step 2</h3>

- Default VPC is used so that it's easier for us to create quickly rather than using our own VPC as we have to create 3 subnets for our AZ. 
- Select 3 AZs under the `eu-west-1a` so `1a` , `1b`, `1c`.

<h3>Step 3</h3>

- Attach the Load balancer then use the Application Load Balancer to allow the HTTP or HTTPS and choose internet facing as we are allow traffic towards
the internet. 

<h3>Step 4</h3>

- Create a target group name under routing, so that we can allow our LB to direct traffic.

<h3>Step 5</h3>

- We now turn on the health checks so that if any of our instances turns unhealthy it can divert to the next instance by auto scaling.
- We choose 300 seconds until a new instance is running. 

<h3>Step 6</h3>

- Group size is vital as we select the desired capacity, Min capacity, and max capacity, which all meean that we can choose how many instances we want to 
run if the current instance becomes unhealthy or shuts down.

<h3>Step 7</h3>

- Scaling policies is used for the increase or decrease the current capacity of a scalable target based on a set of scaling adjustments, known as step adjustments.
- We chose Target Tracking policy as our target value does not exceed our CPU utilization.

<h3>Final Step</h3>

- We add a tag so we can filter and track our ASG, we choose key `name` and value `name-tech221-asg-alb-app`.
- Create ASG. 

<h2>Instances</h2>

- As we click on our instances, two instances should be running and available.
- As we terminate instance as an example, as it can become unhealthy in real production, it should whip up another instance automatically due to our ASG.
