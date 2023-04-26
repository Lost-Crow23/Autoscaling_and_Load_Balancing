<h1>Autoscaling and Load Balancing</h1>

These are the following steps, to create an Autoscaling and Load balancing group using our App AMI so if if one instance crashes we will have another within
300 seconds. 

<h3>Step 1</h3>

Go on the EC2 dashboard from the AWS homepage. And Launch a Template which you may use for the ASG further on.

- Click Create Template

<img width="889" alt="Step 1 launch template in ASG group" src="https://user-images.githubusercontent.com/126012715/234707674-a670cc13-ec95-421c-8cc1-781f8833919c.png">

<h3>Step 2</h3>

- Once your inside the creation, edit your name to a similar one as illustrated below so it can be easy to navigate.
- Click the Auto-scaling guidance so you may use the template for help.

<img width="861" alt="step 2 CREATE launch template" src="https://user-images.githubusercontent.com/126012715/234709508-d8e65c73-0289-418e-8c46-98c399396156.png">

<h3>Step 3</h3>

- Make sure to use Ubuntu 18.04 from the AMI image as other versions may not work.

<img width="817" alt="ubuntu 18 04 ASG" src="https://user-images.githubusercontent.com/126012715/234709663-a45e4141-960a-44cb-a534-315f43da00b3.png">

<h3>Step 4</h3>

- Follow the normal procedure as follows:
- 1. Use t2 micro since our CPU outtage and sub instances we create isn't going to override the capacity.
- 2. Key-pair name e.g tech221

<h3>Step 5</h3>

Network Settings 

- Use your previous security group created for your app, as it will include the HTTP and SSH ports.

<img width="798" alt="Step 4 Template Network settings" src="https://user-images.githubusercontent.com/126012715/234710179-1b776c3c-f09d-4300-bafb-eb455b62d49a.png">

<h3>Step 6</h3>

- Scroll down and edit the User data configuration under the advanced settings with the following commands.

        #!bin/bash
        sudo apt update -y
        sudo apt upgrade -y
        sudo apt install nginx -y
    
 <img width="636" alt="Step 5 template user data" src="https://user-images.githubusercontent.com/126012715/234710317-7aaf780c-cb96-47b4-8d59-15b11b2f9a90.png">

 - Create the template
 
 <h2>Autoscaling Group</h2>
 
 Auto scaling group contains a collection of EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management.

- Create an Auto scaling group under the EC2 dashboard 

<h3>Step 1</h3>

- Create a group name to allign with the template then we use the template we just created prior as this contains our instance (AMI).

<img width="689" alt="Step 1 Auto scaling group name" src="https://user-images.githubusercontent.com/126012715/234712400-0894ad2d-2713-4dfc-a2fc-e10fafa4a44b.png">

<img width="786" alt="step 1 1 ASG launch template" src="https://user-images.githubusercontent.com/126012715/234712376-a7eb0c7c-6afa-4651-9445-74fd95c08be3.png">

<h3>Step 2</h3>

- Default VPC is used so that it's easier for us to create quickly rather than using our own VPC as we have to create 3 subnets for our AZ. 
- Select 3 AZs under the `eu-west-1a` so `1a` , `1b`, `1c`.

<img width="540" alt="Step 2 ASG vpc subnets" src="https://user-images.githubusercontent.com/126012715/234712661-af09389f-873a-4647-b7d5-1b1b5d76f66e.png">

<h3>Step 3</h3>

- Attach the Load balancer then use the Application Load Balancer to allow the HTTP or HTTPS and choose internet facing as we are allow traffic towards
the internet. 

<img width="891" alt="Step 3 Load balancing ASG" src="https://user-images.githubusercontent.com/126012715/234712727-7b5e283c-4359-4d37-946e-853a559660c8.png">

<h3>Step 4</h3>

- Create a target group name under routing, so that we can allow our LB to direct traffic.

<img width="808" alt="step 4 LB AWG create new target group" src="https://user-images.githubusercontent.com/126012715/234712880-6176339d-f458-4a34-aabc-a93631d499cc.png">

<h3>Step 5</h3>

- We now turn on the health checks so that if any of our instances turns unhealthy it can divert to the next instance by auto scaling.
- We choose 300 seconds until a new instance is running. 

<img width="794" alt="Step 5 ASG health checks" src="https://user-images.githubusercontent.com/126012715/234712949-89f6eecd-4771-4552-8a1b-ec0994b09f59.png">

<h3>Step 6</h3>

- Group size is vital as we select the desired capacity, Min capacity, and max capacity, which all meean that we can choose how many instances we want to run if the current instance becomes unhealthy or shuts down.

<img width="855" alt="Step 4 capacity ASG" src="https://user-images.githubusercontent.com/126012715/234714252-8b1f3c84-bf79-4c71-91fd-1eb380b25e14.png">

<h3>Step 7</h3>

- Scaling policies is used for the increase or decrease the current capacity of a scalable target based on a set of scaling adjustments, known as step adjustments.
- We chose Target Tracking policy as our target value does not exceed our CPU utilization.

<img width="794" alt="Step 7 AWG Scaling policies" src="https://user-images.githubusercontent.com/126012715/234714667-a17fd12b-f3d8-4ea9-a351-2b86eaca9dce.png">

<h3>Final Step</h3>

- We add a tag so we can filter and track our ASG, we choose key `name` and value `name-tech221-asg-alb-app`.
- Create ASG. 

<img width="796" alt="step 8 Tag ASG" src="https://user-images.githubusercontent.com/126012715/234714735-fc42f479-aa32-4e77-85e4-06affdc77524.png">

<h2>Instances</h2>

- As we click on our instances, two instances should be running and available.
- As we terminate instance as an example, as it can become unhealthy in real production, it should whip up another instance automatically due to our ASG.

<img width="1188" alt="Final Steps running " src="https://user-images.githubusercontent.com/126012715/234714769-7ae8e6a1-a00e-45a1-8aa1-223e3d174d4d.png">
