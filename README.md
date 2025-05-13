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


## lab 26 Auto scaling - scaling policies

- here the types of scaling policies
![alt text](image-234.png)
- here the forecast 
![alt text](image-235.png)
![alt text](image-236.png)
- here is the dynamic scaling policies
![alt text](image-237.png)
- here the simple scaling 
![alt text](image-238.png)
- here step scaling
![alt text](image-239.png)
- here target tracking scaling
![alt text](image-240.png)
- he created this
![alt text](image-241.png)
- changed this 
![alt text](image-242.png)
![alt text](image-243.png)
- tried to use stress utility to make cpu high 
![alt text](image-244.png)
- installed stress 
![alt text](image-245.png)
- execute stress command
![alt text](image-246.png)
- you can monitor ec2 
![alt text](image-247.png)
- here from history if cpu is high will send to cloud watch then auto scalling create another ec2 
![alt text](image-248.png)
- hera anothe ec2 is created
![alt text](image-249.png)
- if you go to cloud watch you will find two alarms
![alt text](image-250.png)


## lab 27 RDS

- create rds 
![alt text](image-251.png)
- choose standard or easy create
![alt text](image-252.png)
- create mysql
![alt text](image-253.png)
- chooose production to see all settings
![alt text](image-254.png)
- here choose single instance
![alt text](image-255.png)
- put username and password
![alt text](image-256.png)
- if free tier choose the least one
![alt text](image-257.png)
- her as free tier choose gp2 and if you will work in prod choose gp2 
![alt text](image-258.png)
- here if you want to enable auto scaling
![alt text](image-259.png)
- here the conectivity between db and ec2 
![alt text](image-260.png)
- here if you want to enable public access
![alt text](image-261.png)
- create sec group
![alt text](image-262.png)
- from here db authentication
![alt text](image-263.png)
- here if you want to enable monitor
![alt text](image-264.png)
- put a name for db 
![alt text](image-265.png)
- enbale auto bkp for 7 days 
![alt text](image-266.png)
![alt text](image-267.png)
- download sqlectron program
![alt text](image-268.png)
![alt text](image-269.png)
![alt text](image-270.png)
- anfter creation rds copy the endpoint 
![alt text](image-271.png)
- open the app 
![alt text](image-272.png)
- from here create table 
![alt text](image-273.png)
- insert some values
![alt text](image-274.png)
- to create a read replica
![alt text](image-275.png)
- from here to monitor
![alt text](image-276.png)
- if you want to delete you should un check this 
![alt text](image-277.png)

## lab 27 Aurora 


- create db
![alt text](image-278.png)
![alt text](image-279.png)
- choose features
![alt text](image-280.png)
- db name
![alt text](image-281.png)
- choose aurora standard
![alt text](image-282.png)
- instance config
![alt text](image-283.png)
![alt text](image-284.png)
![alt text](image-285.png)
![alt text](image-286.png)
![alt text](image-287.png)
![alt text](image-288.png)
![alt text](image-289.png)
![alt text](image-290.png)
- it should be like this after creation 
![alt text](image-291.png)
- here reader and writer endpoint 
![alt text](image-292.png)
- here all the options 
![alt text](image-293.png)
- from here to create a read replica
![alt text](image-294.png)
![alt text](image-295.png)
![alt text](image-296.png)

## lab 28 ElasticCache (Redis and Memcached)

- Note: elasticache needs a big change in the code 
![alt text](image-297.png)
![alt text](image-298.png)
- choose cluser cache to see all settings
![alt text](image-299.png)
![alt text](image-300.png)
![alt text](image-301.png)
![alt text](image-302.png)
![alt text](image-303.png)
![alt text](image-304.png)
![alt text](image-305.png)
![alt text](image-306.png)
- here after creation
![alt text](image-307.png)
- at the code of developer use this endpoint
![alt text](image-308.png)
- here the nodes of redis
![alt text](image-309.png)

## lab 29 Route 53 

- Note: no need to do this lab , just understand it as you will pay 13 $
![alt text](image-310.png)
- choose a domain not used before
![alt text](image-311.png)
![alt text](image-312.png)
- if enabled this you will not receive spam
![alt text](image-313.png)
![alt text](image-314.png)
- after creation should be like this
![alt text](image-315.png)
- create our first record 
![alt text](image-316.png)
- created a record with name test and value any thing 
![alt text](image-317.png)
- here after creation 
![alt text](image-318.png)
- to test it using nslookup
![alt text](image-319.png)
- here from dig
![alt text](image-320.png)
- he will ceate three EC2s in three diffrent regions and use this script
```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
# updated script to make it work with Amazon Linux 2023
CHECK_IMDSV1_ENABLED=$(curl -s -o /dev/null -w "%{http_code}" http://169.254.169.254/latest/meta-data/)
if [[ "$CHECK_IMDSV1_ENABLED" -eq 200 ]]
then
    EC2_AVAIL_ZONE="$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)"
else
    EC2_AVAIL_ZONE="$(TOKEN=`curl -s -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` && curl -s -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/placement/availability-zone)"
fi
echo "<h1>Hello world from $(hostname -f) in AZ $EC2_AVAIL_ZONE </h1>" > /var/www/html/index.html
```
![alt text](image-321.png)
- here the three ec2 in different regions
![alt text](image-322.png)
- create a load balancer in frankfurt region
![alt text](image-323.png)
- choose all zones and select sec group
![alt text](image-324.png)
- create a target group
![alt text](image-325.png)
![alt text](image-326.png)
- here the load balancer
![alt text](image-327.png)
- get all the ips for the three ec2 and dns for elb
![alt text](image-328.png)
- to check TTL , create a record with 2 mins
![alt text](image-329.png)
![alt text](image-330.png)
- from dig tool you will see the ttl time
![alt text](image-331.png)
- if you changed the ip before the 2 mins finished you will see the old value
![alt text](image-332.png)
- after the 2 mins finished you will see the new value
![alt text](image-333.png)
- here create a record for CNAME and maped it to the load balancer 
![alt text](image-334.png)
- here it is worked iwth myapp.stephaneteacher.com
![alt text](image-335.png)
- here if you use the alias and for your info the alias is for free
![alt text](image-336.png)
- here to test alais
![alt text](image-337.png)
- Note: if you want to do this with CNAME will got error and the solution to use alias
![alt text](image-338.png)
![alt text](image-339.png)
- here worked with alias
![alt text](image-340.png)
- here the routing policies ( simple, weighted, failover, latency based, geolocation, multi-value answer ,geoproximity)
- here the simple policy type and means that it will route the traffic to a single resource 
![alt text](image-341.png)
![alt text](image-342.png)
- if you put more than one ip
![alt text](image-343.png)
![alt text](image-344.png)
- here the weighted policy type, for example 10% of traffic will go to southeast
![alt text](image-345.png)
- and 70% of traffic will go to US east
![alt text](image-346.png)
- and 20% of traffic will go to EU
![alt text](image-347.png)
- here after creatiion 
![alt text](image-348.png)
- here the latency based type
![alt text](image-349.png)
![alt text](image-350.png)
![alt text](image-351.png)
![alt text](image-352.png)
- the result depend on least latency
![alt text](image-353.png)

## lab 30 Route 53 health check

- create health check for every region , here for us-east-1
![alt text](image-354.png)
![alt text](image-355.png)
![alt text](image-356.png)
![alt text](image-357.png)
![alt text](image-358.png)
- here for ap-southeast-1
![alt text](image-359.png)
- here for eu-central-1
![alt text](image-360.png)
![alt text](image-361.png)
- here the three created ones
![alt text](image-362.png)
- to let the security group fail, he will delete this from security group
![alt text](image-363.png)
![alt text](image-364.png)
- here you will see that it is unhealthy
![alt text](image-365.png)
- will create calculted health check 
![alt text](image-366.png)
![alt text](image-367.png)
![alt text](image-368.png)
![alt text](image-369.png)