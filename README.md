 # AWS-stephan-labs

## lab 01 Iam user and groups

- IAM => users
![alt text](image.png)
- put the username and confirm pass
![alt text](image-1.png)
- put the name and attached policy
![alt text](image-2.png)
- add user to group
![alt text](image-3.png)
- git him permission
![alt text](image-4.png)
- to create alias
![alt text](image-5.png)
![alt text](image-6.png)
- should be like this 
![alt text](image-7.png)
![alt text](image-8.png)


## lab 02 IAM policies

- the left pic is root account and right pic is user that you ceated
![alt text](image-9.png)
- if you delete the permissions
![alt text](image-10.png)
- to add permission
![alt text](image-11.png)
- add read only access
![alt text](image-12.png)
![alt text](image-13.png)
- here you just read only
![alt text](image-14.png)
- if you try to creat any thing you will got this error
![alt text](image-15.png)
- create a group name developers
![alt text](image-16.png)
- add the user stephan to it
![alt text](image-17.png)
- to create a policy
![alt text](image-18.png)
- press to this policy
![alt text](image-19.png)
- this mean that allow any action to any resource
![alt text](image-20.png)
- this is another one
![alt text](image-21.png)
- to create your own policy
![alt text](image-22.png)
- you can create it as json or visual
![alt text](image-23.png)
- this visual
![alt text](image-24.png)
![alt text](image-25.png)
![alt text](image-26.png)
![alt text](image-27.png)
![alt text](image-28.png)
- this is the output for the created policy
![alt text](image-29.png)

## lab 03 MFA

- if you want to change password policy
![alt text](image-30.png)
![alt text](image-31.png)
- to enable MFA
![alt text](image-32.png)
![alt text](image-33.png)
![alt text](image-34.png)
![alt text](image-35.png)
![alt text](image-36.png)


## lab 04 Access and secret access key 

- IAM => users => name of the user
![alt text](image-37.png)
![alt text](image-38.png)
![alt text](image-39.png)
![alt text](image-40.png)
![alt text](image-41.png)
![alt text](image-43.png)
![alt text](image-42.png)
![alt text](image-44.png)

## lab 05 IAM roles and attach it to ec2

- create role and select aws service 
![alt text](image-45.png)
- choose ec2
![alt text](image-46.png)
- choose readonly 
![alt text](image-47.png)
![alt text](image-48.png)
![alt text](image-49.png)
- to use the role create ec2 first
![alt text](image-53.png)
- attach the role to ec2
![alt text](image-54.png)
- test it by using aws iam lust-uers
![alt text](image-55.png)

## lab 05 IAM Security tools (credential report and access advisor)

- IAM => credential report
![alt text](image-50.png)
![alt text](image-51.png)
- IAM => user => access advisor
![alt text](image-52.png)

## lab 06 billing and cost management and budget 

- from billing and cost managment => cost explorer
![alt text](image-56.png)
- to can see bills you should make it from root account then activate IAM acess to make normal users see bills 
![alt text](image-58.png)
![alt text](image-59.png)
![alt text](image-60.png)
![alt text](image-61.png)
- create budget 
![alt text](image-62.png)
![alt text](image-63.png)

## lab 07 launch ec2 linux

- create ec2
![alt text](image-64.png)
- choose linux
![alt text](image-65.png)
![alt text](image-66.png)
![alt text](image-67.png)
![alt text](image-68.png)
```bash
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```
![alt text](image-69.png)
![alt text](image-71.png)

![alt text](image-72.png)

## lab 08 security group

- configure the inbound 
![alt text](image-73.png)

## lab 09 ec2 with role
![alt text](image-74.png)
![alt text](image-75.png)
![alt text](image-76.png)
![alt text](image-77.png)
![alt text](image-78.png)
![alt text](image-79.png)
![alt text](image-80.png)
![alt text](image-81.png)

## lab 10 ec2 launch types

![alt text](image-82.png)
![alt text](image-83.png)
![alt text](image-84.png)

## lab 11 placement group

![alt text](image-85.png)
![alt text](image-86.png)
![alt text](image-87.png)
![alt text](image-88.png)
![alt text](image-89.png)
![alt text](image-90.png)
![alt text](image-91.png)

## lab 12 placement group
- create two ec2s
![alt text](image-92.png)
- network interfaces for both
![alt text](image-93.png)

## lab 13 ec2 Hibernate 

- only these tupes support hibernate
![alt text](image-96.png)
- when creating ec2 choose this
![alt text](image-94.png)
- here to hibernate instance
![alt text](image-95.png)

## lab 14 EBS creation and attachment 

- note that the ec2 and ebs should be in same az
- here the eb2 which is attached to ec2
![alt text](image-97.png)
![alt text](image-98.png)
- create another ebs
![alt text](image-99.png)
- create it in another zone
![alt text](image-100.png)
![alt text](image-101.png)
- note it is available
![alt text](image-102.png)
- to attach it 
![alt text](image-103.png)
![alt text](image-104.png)
- note the instance has two ebs
![alt text](image-105.png)
- create third volume in another zone
![alt text](image-106.png)
![alt text](image-107.png)
- tried to attach but there is no ec2 in this zone
![alt text](image-108.png)
- when delete the ec2 , the main one is checked on delete on termination
![alt text](image-109.png)

## lab 15 EBS snapshots

- to creat snapshot from EBS , select it and create snapshot
![alt text](image-110.png)
![alt text](image-111.png)
- here the created snapshot
![alt text](image-112.png)
- you copy this snapshot to other region and then create ebs from this snapshot
![alt text](image-113.png)
![alt text](image-114.png)
- here you can create ebs from snpshot 
![alt text](image-115.png)
- here you can move it to other az 
![alt text](image-116.png)
![alt text](image-117.png)
- here the recycle bin 
![alt text](image-118.png)
- create retention role and this mean how much time should be kept before permenant deletion 
![alt text](image-119.png)
![alt text](image-120.png)
![alt text](image-121.png)
![alt text](image-122.png)
- tried to delete the snapshot
![alt text](image-123.png)
- will appear at the recycle bin
![alt text](image-124.png)
- you can recover it 
![alt text](image-125.png)

## lab 16 AMI

- create ec2 with this script
```bash
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```
![alt text](image-126.png)
- create an image from ec2
![alt text](image-127.png)
![alt text](image-128.png)
![alt text](image-129.png)
- from here you will find AMIs
![alt text](image-130.png)
- create ec2 from this AMI
![alt text](image-131.png)
- put this script
```bash
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)

echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```
![alt text](image-132.png)
- test it
![alt text](image-133.png)

## lab 17 EBS encryption 

![alt text](image-134.png)
![alt text](image-135.png)
![alt text](image-136.png)
![alt text](image-137.png)
![alt text](image-138.png)
![alt text](image-139.png)
![alt text](image-140.png)
![alt text](image-141.png)
![alt text](image-142.png)

## lab 18 EFS

- create EFS
![alt text](image-143.png)
- customize it 
![alt text](image-144.png)
- choose lifecycle managment
![alt text](image-145.png)
- choose performance setting
![alt text](image-146.png)
![alt text](image-147.png)
- network setting 
![alt text](image-148.png)
![alt text](image-149.png)
![alt text](image-150.png)
- create ec2 and when creating choose the EFS 
![alt text](image-151.png)
- create another ec2 in other az
![alt text](image-152.png)
- login to each ec2  and mount the efs 
![alt text](image-153.png)
![alt text](image-154.png)

## lab 19 App load balancer part 01

- creat 2 EC2s with this script
![alt text](image-155.png)
- create app load balancer
![alt text](image-156.png)
![alt text](image-157.png)
- name of load balancer
![alt text](image-158.png)
- choose three zones
![alt text](image-159.png)
- create a sec group for load balancer
![alt text](image-160.png)
- creat inbound rule and means that any one can reach the load balancer
![alt text](image-161.png)
![alt text](image-162.png)
- choose the sec group
![alt text](image-163.png)
- create a target group
![alt text](image-164.png)
![alt text](image-165.png)
- name of target group and which protocol the EC2s are listening on 
![alt text](image-166.png)
- choose which EC2s to be member in target group
![alt text](image-167.png)
![alt text](image-168.png)
- create listener and choose which target group
![alt text](image-169.png)
![alt text](image-170.png)
- open with dns name
![alt text](image-171.png)
![alt text](image-172.png)

## lab 20 App load balancer part 02

- I need the load balancer only to access the ec2 so with create inbound role and choose the lb sec group 
![alt text](image-174.png)
![alt text](image-173.png)
- create a listener rule
![alt text](image-175.png)
![alt text](image-176.png)
- here the rules conditions
![alt text](image-177.png)
- for example here the path for error
![alt text](image-178.png)
![alt text](image-179.png)
- from here choose the pariority
![alt text](image-180.png)
- to test the error
![alt text](image-181.png)

## lab 21 network load balancer

- create network lb
![alt text](image-182.png)
- create name for it
![alt text](image-183.png)
- choose all az and creat a security group for it
![alt text](image-184.png)
- create a target group
![alt text](image-185.png)
- at health check chooose http 
![alt text](image-186.png)
- choose health check parameters
![alt text](image-187.png)
- choose the EC2s to be part of target group
![alt text](image-188.png)
![alt text](image-189.png)
![alt text](image-190.png)
![alt text](image-191.png)
- note it didn't work as the ec2 are unhealthy
![alt text](image-192.png)
- solution: add a security group rule to allow ec2 
![alt text](image-193.png)
![alt text](image-194.png)
- after adding sec group rule , the EC2s are healty
![alt text](image-195.png)
- worked here
![alt text](image-196.png)

## lab 22 sticky session 

- from target group 
![alt text](image-197.png)
![alt text](image-198.png)
![alt text](image-199.png)
- to know details about it
![alt text](image-200.png)

## lab 23 cross zone load balancing

- here the three types of load balancer
![alt text](image-201.png)
- at network lb is disabled by default and if you enable it you will pay 
![alt text](image-202.png)
- the same at GLB
![alt text](image-203.png)
- but the app lb os enabled by default
![alt text](image-204.png)
- this at the level of target group
![alt text](image-205.png)

## lab 24 elastic load balancer with ssl certificate

- here a network and app load balancer
![alt text](image-206.png)
- from app lb will create a listener
![alt text](image-207.png)
- the protocol will be 433
![alt text](image-208.png)
- forward traffic to new target group
![alt text](image-209.png)
- chooose security policy
![alt text](image-210.png)
- here the certificate 
![alt text](image-211.png)
- the same steps he did them at the network lb

## lab 25 Auto scaling 

- create auto scaling group
![alt text](image-212.png)
- put a name and create the launch template
![alt text](image-213.png)
- put a name for launch template
![alt text](image-214.png)
- choose the image
![alt text](image-215.png)
- type of ec2
![alt text](image-216.png)
- key pair 
![alt text](image-217.png)
- sec group
![alt text](image-218.png)
- user data
```bash
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```
![alt text](image-219.png)
![alt text](image-220.png)
- go back to the auto scaling
![alt text](image-221.png)
- at the network chooose the VPC
![alt text](image-222.png)
- from here if you want to override the launch template
![alt text](image-223.png)
- here attach the auto scaling with en exsiting load balancer
![alt text](image-224.png)
![alt text](image-225.png)
- here it is created 
![alt text](image-226.png)
- this is the created ec2 from auto scaling
![alt text](image-228.png)
- here the history 
![alt text](image-229.png)
- if you go to target group you will find that ec2 is healty
![alt text](image-230.png)
- tested it
![alt text](image-231.png)
- from here if you want to edit the desired, min and max
![alt text](image-232.png)
- you can check the history
![alt text](image-233.png)