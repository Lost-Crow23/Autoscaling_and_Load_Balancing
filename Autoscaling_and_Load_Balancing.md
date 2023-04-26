<h1>Autoscaling and Load Balancing</h1>

![New diagram AS and LB](https://user-images.githubusercontent.com/126012715/234576506-5f85a8d2-b628-4fd1-b246-711bd02c69f7.png)

<h3>What is Autoscaling?</h3>

- Feature of cloud computing that automatically adjusts the amount of resources allocated to an application or service within it's demand
- Handles changes in user traffic without manual intervention or the need to provision additional resources manually
- Works using predefined rules to monitor an application or service metrics, such as CPU usage or network traffic then auto scales the resources up or down
accordingly 
- Increases or decreases the number of instances of an appliaction, increasing or decreasing the size of VMs, adds or removes container instances
- Triggered by changes in user traffic, workload, and infrastructure 
- Improves applications performance and reliability by ensuring there is enough resources available to handle workload.
- Used within AWS, Microsoft Azure, Google Cloud platform. 

<h3>What is Load balancing?</h3>

Load balancing distributes traffic between the EC2 instances so that no one instance gets overwhelemed. 

- Can be implemented using software or hardware components that benches between the client and server and distributes incoming requests across multiple servers based on predefined users.
- Often imporoves the application's availablility by detecting when a server is unavailable or not respoonding and redirects traffic to healthy servers.
- Performance is improved by distributing traffic to servers that have the most available resources, such as CPU, memory or bandwidth.
- improves the sacalabilty by auto adding or removing computing resources as demand fluctuates
- configured to use different alogorithms such as round-robin, least connections, IP hash to distribute the traffic across the servers.
- can be implemented using AWS, Elastic load balancing Application load balancing or network load balancing
- integrated with other AWS services such as Auto Scaling and Amazon route 53, to automate scaling and DNS routing based on traffic patterns

<h3>What is ALB?</h3>

- Application Load Balancing is a service that provides layer 7, for HTTP or HTTPS traffic.
- Distributes incoming requests for targets, such as EC2 instances, containers, IP addresses.
- Supports features like path based routing

<h3>What is Scaling up?</h3>

Scaling up is when you need to scale up for the sake of a bigger server for the developers so it does not crash
- you can't scale up if a bigger cpu is needed

<h3>What is Scale into?</h3>

Scale into is when have multiple instances running from the load balancer so if one crashes it will take 300 second for the next one too run .
