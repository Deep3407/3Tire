3-Tier Architecture In AWS
Motive of the task. 
involves setting up a three-tier architecture in AWS, including a presentation tier (front-end), application tier (back-end logic), and database tier. You'll create a Virtual Private Cloud (VPC), subnets, internet gateway (IG), NAT gateway, route table, EC2 instances, launch templates, and auto scaling groups to distribute the workload across different tiers.
Architectural Diagram

 
Steps :
Login to your Console Navigate to VPC services
Create a VPC and give CIDR value = 10.0.0.0/16

 

 
Go to subnet section and create subnets for web-tier  , Application-tier , and Db tier 

 




Put a set of subnets of web tier , App tier and DB tier in one avaliblity zone us-east 1a
Put a another set of subnets of web tier , App tier and DB tier in one avaliblity zone us-east 1b
 

 
 


 
 


 

Thus subnets are created in two different availblity zone




Then create a route table for each tier , thus 3 – route table for each web , app ,DB tier , a route table will connect within two different availbility zone 

 
Associate the route table with subnets 
 



 


 


 
Create a internet gate way to attach internet to the created VPC , 
 


 
 


 

 

Create a NAT gateway by allocating elastic IP , select the public subnet 
 
 

 
 
Add route for each rote table and point it to IG and NAT
Select the route table click routes and edit route
 
Click add route and select internet gate way and select the created internet gateway

Select the route table click routes and edit route
 


 
Click add rule and select 0.0.0./0 and select nat gateway
Web tier to pointed to Internet gateway , and rest are pointed to NAT 

Navigate to EC2 console
Create a instance in the web subnet that would be our Jump server and create a new security group 
 


And create a instances in the app subnets and create a new security group and configure the same for both app subnet instances.
 

 


 

Create a application load balancer with following requsites
Application load balancer
Internet facing 
Security group – 80 
App subnet instances 
Target group with app subnet instances
  
Click target group and selct the two app instances
 
Select instances
 






And select my-vpc
 

And select the target which is our two app instances
 



And click create target group
 

Navigate to RDB console 

 




Create a new subnet groups 

 
 
 
 

Select the created VPC , availablity zone , and DB subnets,

Create a database and ,
Give a name to the database and select mysql,
Give master passwords,
Select created VPC and DB subnets and click create Database.


 
 
 
 
 

A 3-tier architecture is created

