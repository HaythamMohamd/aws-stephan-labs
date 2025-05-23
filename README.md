 # AWS-stephan-labs

##  VPC

- here will do all these services 
![alt text](image-657.png)
- here is the default vpc
![alt text](image-658.png)
- here three subnets in each zone
![alt text](image-659.png)
![alt text](image-660.png)
![alt text](image-661.png)
![alt text](image-662.png)
![alt text](image-663.png)
- here nacls
![alt text](image-664.png)
- route table
![alt text](image-665.png)
- internet gw
![alt text](image-666.png)
- rounte table their is association between subntes
![alt text](image-667.png)

## lab vpc creation 

- create your vpc
![alt text](image-668.png)

- choose name and cidr
![alt text](image-669.png)
- create a tag
![alt text](image-670.png)
- after creation the vpc if you want to add a secondary cidr
![alt text](image-671.png)
![alt text](image-672.png)

## lab subnet creation 

- create public anc private vpc
![alt text](image-673.png)
- FYI there are 5 IPs are reserved to AWS for each subnet
![alt text](image-674.png)
- create subnet 
![alt text](image-675.png)
- choose which vpc to you want to create the subnet inside it
![alt text](image-676.png)
- create first public subnetA with cidr 10.0.0.0/24
![alt text](image-677.png)
- create first public subnetB with cidr 10.0.1.0/24
![alt text](image-678.png)
- create first private subnetA with cidr 10.0.16.0/20
![alt text](image-679.png)
- create first private subnetB with cidr 10.0.32.0/20
![alt text](image-681.png)
![alt text](image-680.png)
- here the four subnets
![alt text](image-682.png)
- you can see the available ips for each subnet
![alt text](image-683.png)

## lab internet gateway and route table creation 

- the internet gw should be mapped to a vpc
![alt text](image-684.png)
- if you try to create an EC2 this by default is disable
![alt text](image-685.png)
- so we need to enable it at the public subnets only 
![alt text](image-686.png)
![alt text](image-687.png)
![alt text](image-688.png)
- the same at the other subnet 
![alt text](image-689.png)
- he created an EC2 and to reach internet, must create internet gw
![alt text](image-690.png)
- create an internet gw
![alt text](image-691.png)
![alt text](image-692.png)
- attach it to your vpc
![alt text](image-693.png)
![alt text](image-694.png)
- till now will not be able to access internet because there is no route table to point to the internet gw that you created , so create one
![alt text](image-695.png)
- will create two routes one for public and the other for private
![alt text](image-696.png)
![alt text](image-697.png)
- go to the public route table to do the subnet association
![alt text](image-698.png)
- edit it and choose the public subnets
![alt text](image-699.png)
![alt text](image-700.png)
- do the same with private
![alt text](image-701.png)
![alt text](image-702.png)
![alt text](image-703.png)
- last step, go to the route table and edit it then add route for any thing go to internet gw
![alt text](image-704.png)
![alt text](image-705.png)
- test from ec2 and it will work
![alt text](image-706.png)

## lab Bastion host

- idea
![alt text](image-707.png)
- this EC2 should be in the public subnet and any one can access it
![alt text](image-708.png)
- create a key pair
![alt text](image-709.png)
- create an ec2 in the private subnet 
![alt text](image-710.png)
- create a seg group for the private ec2 
![alt text](image-711.png)
- just allow the port 22 and any traffic come from the sec group of bastion host
![alt text](image-712.png)
![alt text](image-713.png)
- here the both EC2s
![alt text](image-714.png)
- so to access the private ec2 you should ssh first to bastion host then ssh to the private one 
![alt text](image-715.png)
- copied the private key for the private ec2 and created a file for it in the bastion host 
![alt text](image-716.png)
- chmod 400
![alt text](image-717.png)
- now we can ssh private ec2 from the bastion host
![alt text](image-718.png)
- at it is normal that the private ec2 can't access internet and will solve this issue by the nat gw
![alt text](image-719.png)

## lab NAT instance

- idea of nat instance, the issue here that you will responsible for all of that and cost more money 
![alt text](image-720.png)
![alt text](image-721.png)
- create ec2 for nat instance 
![alt text](image-722.png)
- selected one from market place
![alt text](image-723.png)
![alt text](image-724.png)
- it should be in public subnet 
![alt text](image-725.png)
- create a sec group for it and open access from anywhere
![alt text](image-726.png)
- also added this
![alt text](image-727.png)
![alt text](image-728.png)
- you must change this and stop source/dest feature to let the ec2 redirect the traffic
![alt text](image-729.png)
![alt text](image-730.png)
- go to the private subnet to edit the routes
![alt text](image-731.png)
![alt text](image-732.png)
- here any traffic should go to the NAT instance 
![alt text](image-733.png)
![alt text](image-734.png)
- confirm at the sec group that the ping is added 
![alt text](image-735.png)
- test the internet from private ec2 
![alt text](image-736.png)
- don't forget to destroy it
![alt text](image-737.png)


## lab NAT gateway

- idea: the responsability of nat gw is on aws not at you
![alt text](image-738.png)
![alt text](image-739.png)
- for high availability should be in each az you have nat gw
![alt text](image-740.png)
- note: once we deleted the NAT insatnce you will find this blackhole 
![alt text](image-741.png)
- create NAT gw
![alt text](image-742.png)
- the NAT gw should have elastic ip
![alt text](image-743.png)
![alt text](image-744.png)
- edit the routes at the private route table
![alt text](image-745.png)
- it should be any traffic will go to the nat gw
![alt text](image-746.png)
![alt text](image-747.png)
- test from private instance and will work
![alt text](image-748.png)


## lab Nacls and sec group
- idea
![alt text](image-749.png)
![alt text](image-750.png)
- here the default nacls in inbound 
![alt text](image-751.png)
- here the default nacls in outbound 
![alt text](image-752.png)
- will install apache in bastion host instance
![alt text](image-753.png)
![alt text](image-754.png)
![alt text](image-755.png)
- at the sec group of bastion host open http for all ips
![alt text](image-756.png)
- here it works
![alt text](image-757.png)
- if you edited the default nacls and dey the http on port 80 
![alt text](image-758.png)
- it will not work, as the request goes firs at the nacl and override the sec group
![alt text](image-759.png)
- if you edit the nacls and the number to be 140, this means that tha allow traffic will be the first so it will work
![alt text](image-760.png)
![alt text](image-761.png)
- here worked
![alt text](image-762.png)
- if you edited the outbound and deny, so it will not work as you know that the nacls is stateless and this mean you should define each rule at inbound and outbound
![alt text](image-763.png)
- here didn't work so he revereted the outbound again to be allow
![alt text](image-764.png)
- to test the sec group, here at inbound
![alt text](image-765.png)
- for the outbound her removed every thing and it will work as the sec group is statefull and this means if the inboud is ok the outbound will be automaticallu ok
![alt text](image-766.png)
- here it worked
![alt text](image-767.png)

## lab VPC peering

- idea
![alt text](image-768.png)
![alt text](image-769.png)
- will create vpc peering between default and demo vpc
![alt text](image-770.png)
- create ec2 in default vpc
![alt text](image-771.png)
- notice here the two ec2s have a different ips in defferent networks
![alt text](image-772.png)
![alt text](image-773.png)
- here the bastion host curl his ip is ok
![alt text](image-774.png)
- but from the ec2 in default vpc can't ping or curl the ip of bastion host 
![alt text](image-775.png)
- solution: create vpc peering between them
![alt text](image-776.png)
![alt text](image-777.png)
- here the both in the same account 
![alt text](image-778.png)
- here the other vpc
![alt text](image-779.png)
![alt text](image-780.png)
- note it is pending till the other vpc accept peering 
![alt text](image-781.png)
- go to the other vpc and accept peering 
![alt text](image-782.png)
![alt text](image-783.png)
- must configure the route table between them 
![alt text](image-784.png)
- go to the public route table 
![alt text](image-785.png)
- add the route that if you want to go to 172.31.0.0/16 should be through vpc peering
![alt text](image-786.png)
![alt text](image-787.png)
- do the same for the other vpc route table
![alt text](image-788.png)
![alt text](image-789.png)
- here is worked 
![alt text](image-790.png)

## lab VPC endpoint (gateway and interface)

- idea: need to access dynamo db not from public but from internal 
![alt text](image-791.png)
- if you accessed it public from ec2 => nat gw => sns , this will cost money 
![alt text](image-792.png)
- here the best option to use vpc endpoint 
![alt text](image-793.png)
- we have two types(interface endpoint and gw endpoint)
![alt text](image-794.png)
- gateway is prefered 
![alt text](image-795.png)
- will delete this instance 
![alt text](image-796.png)
- will ssh to bastion instance then to the private instance 
![alt text](image-797.png)
![alt text](image-798.png)
- to access the s3 should create role 
![alt text](image-799.png)
![alt text](image-800.png)
![alt text](image-801.png)
![alt text](image-802.png)
![alt text](image-803.png)
![alt text](image-804.png)
![alt text](image-805.png)
![alt text](image-806.png)
- here it is working
![alt text](image-807.png)
- if you deleted the route at the internet gw 
![alt text](image-808.png)
![alt text](image-809.png)
- here it is not working 
![alt text](image-810.png)
- the solution: to create endpoint 
![alt text](image-811.png)
- here if you want to choose interface endpoint 
![alt text](image-812.png)
- choose to which vpc
![alt text](image-813.png)
- choose which subnets
![alt text](image-814.png)
- choose the sec group 
![alt text](image-815.png)
- back to the gateway endpoint 
![alt text](image-816.png)
- choose which vpc
![alt text](image-817.png)
- update private route table 
![alt text](image-818.png)
![alt text](image-819.png)
![alt text](image-820.png)
![alt text](image-821.png)
- if go to the route table for endpoint you will find this route is added automatic
![alt text](image-822.png)
- tested again and worked
![alt text](image-823.png)

## lab VPC flow logs and Athena

- idea 
![alt text](image-824.png)
![alt text](image-825.png)
![alt text](image-826.png)
- demo: from vpc create flow logs
![alt text](image-827.png)
- put the name and the filter
![alt text](image-828.png)
![alt text](image-829.png)
- create s3 at the same region of vpc
![alt text](image-830.png)
![alt text](image-831.png)
- take the s3 arn and put here
![alt text](image-832.png)
- here the format of logs
![alt text](image-833.png)
![alt text](image-834.png)
![alt text](image-835.png)
- create another flow logs and send it to cloud watch
![alt text](image-836.png)
- we need to create role and log group
![alt text](image-837.png)
- create policy
![alt text](image-838.png)
![alt text](image-839.png)
![alt text](image-840.png)
![alt text](image-841.png)
![alt text](image-842.png)
![alt text](image-843.png)
- go to cloud watch to creat a log group
![alt text](image-844.png)
![alt text](image-845.png)
![alt text](image-846.png)
- go back to flow log and put the destination log group and IAM role
![alt text](image-847.png)
![alt text](image-848.png)
- now we have two flow logs, one got to s3 and the other go to cloud watch 
![alt text](image-849.png)
- if you go to s3
![alt text](image-850.png)
- here the cloud watch
![alt text](image-851.png)
- here the logs
![alt text](image-852.png)
- go to Athena
![alt text](image-853.png)
![alt text](image-854.png)
![alt text](image-855.png)
- here we need another s3 to send the result to it
![alt text](image-856.png)
- create s3 for athena 
![alt text](image-857.png)
![alt text](image-858.png)
- take the ARN of s3 and go back to athena
![alt text](image-859.png)
- put the ARN here
![alt text](image-860.png)
- here athena after creation
![alt text](image-861.png)
- need to create a db
![alt text](image-862.png)
![alt text](image-863.png)
![alt text](image-864.png)
![alt text](image-865.png)
![alt text](image-866.png)
![alt text](image-867.png)
![alt text](image-868.png)
- here all the code 
```bash
create database s3_access_logs_db;

CREATE EXTERNAL TABLE IF NOT EXISTS s3_access_logs_db.mybucket_logs(
         BucketOwner STRING,
         Bucket STRING,
         RequestDateTime STRING,
         RemoteIP STRING,
         Requester STRING,
         RequestID STRING,
         Operation STRING,
         Key STRING,
         RequestURI_operation STRING,
         RequestURI_key STRING,
         RequestURI_httpProtoversion STRING,
         HTTPstatus STRING,
         ErrorCode STRING,
         BytesSent BIGINT,
         ObjectSize BIGINT,
         TotalTime STRING,
         TurnAroundTime STRING,
         Referrer STRING,
         UserAgent STRING,
         VersionId STRING,
         HostId STRING,
         SigV STRING,
         CipherSuite STRING,
         AuthType STRING,
         EndPoint STRING,
         TLSVersion STRING
) 
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.RegexSerDe'
WITH SERDEPROPERTIES (
         'serialization.format' = '1', 'input.regex' = '([^ ]*) ([^ ]*) \\[(.*?)\\] ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) \\\"([^ ]*) ([^ ]*) (- |[^ ]*)\\\" (-|[0-9]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) (\"[^\"]*\") ([^ ]*)(?: ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*))?.*$' )
LOCATION 's3://target-bucket-name/prefix/';


SELECT requesturi_operation, httpstatus, count(*) FROM "s3_access_logs_db"."mybucket_logs" 
GROUP BY requesturi_operation, httpstatus;

SELECT * FROM "s3_access_logs_db"."mybucket_logs"
where httpstatus='403';
```

## lab site to site vpn 

- idea:
![alt text](image-869.png)
![alt text](image-870.png)
![alt text](image-871.png)
![alt text](image-872.png)
- Lab: create customer gw
![alt text](image-873.png)
- here the info should be known from onprem
![alt text](image-874.png)
- here if there is a cert
![alt text](image-875.png)
![alt text](image-876.png)
- create virtual private gateway
![alt text](image-877.png)
![alt text](image-878.png)
- create vpn connection
![alt text](image-879.png)
![alt text](image-880.png)
![alt text](image-881.png)
![alt text](image-882.png)

## lab direct connect 

- idea: 
![alt text](image-883.png)
![alt text](image-884.png)

## ipv6 for VPC

- from vpc => edit cidr 
![alt text](image-885.png)
![alt text](image-886.png)
![alt text](image-887.png)
![alt text](image-888.png)
- go to subnet
![alt text](image-889.png)
![alt text](image-890.png)
![alt text](image-891.png)
![alt text](image-892.png)
![alt text](image-893.png)
- go to the ec2 
![alt text](image-894.png)
- make it auto sign
![alt text](image-895.png)
![alt text](image-896.png)
- go to the sec group to allow ipv6
![alt text](image-897.png)
![alt text](image-898.png)
- from this site you can test ipv6
![alt text](image-899.png)
![alt text](image-900.png)
- from route table there is aroute is added 
![alt text](image-901.png)

## lab egree-only internet gw

- idea:
![alt text](image-902.png)
![alt text](image-903.png)
- lab, create egress only internet gw
![alt text](image-904.png)
![alt text](image-905.png)
- edit the routes at route table
![alt text](image-906.png)
- choose any thing should go to the ingress only internet gw
![alt text](image-907.png)


## clean up all vpc labs

- stop instances and delete them
![alt text](image-908.png)
- delete all of this 
![alt text](image-909.png)
- see bills
![alt text](image-910.png)
![alt text](image-911.png)
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

## lab 30 Route 53 health check , failover , geolocation and multi value 

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
- for routing policy failover active passive 
![alt text](image-370.png)
![alt text](image-371.png)
![alt text](image-372.png)
- for for routing policy geolocation 
![alt text](image-374.png)
![alt text](image-373.png)
![alt text](image-375.png)
![alt text](image-376.png)
- for for multi value 
![alt text](image-377.png) 
![alt text](image-378.png)
![alt text](image-379.png)
![alt text](image-380.png)
- if you made any of them unhealthy you will see the other two
![alt text](image-381.png)

## lab 31 Elastic Beanstalk

- here the developers interest only at the code and no need for the infra 
![alt text](image-382.png)
- so beantstalk is a good choice 
![alt text](image-383.png)
- choose the environment and the name
![alt text](image-384.png)
![alt text](image-385.png)
- choose the platform that you want
![alt text](image-386.png)
![alt text](image-387.png)
![alt text](image-388.png)
- create a role 
![alt text](image-389.png)
- from iam create the role 
![alt text](image-390.png)
![alt text](image-391.png)
![alt text](image-392.png)
![alt text](image-393.png)
![alt text](image-394.png)
![alt text](image-395.png)
- after creation beanstak here the events
![alt text](image-396.png)
![alt text](image-397.png)
- to access it 
![alt text](image-398.png)
![alt text](image-399.png)


## lab 32 S3 creation and upload file

- create bucket
![alt text](image-400.png)
- choose name of the bucket and region
![alt text](image-401.png)
- recommended to keep acls disabled
![alt text](image-402.png)
- here bloc pulbic access 
![alt text](image-403.png)
![alt text](image-404.png)
- upload this image
![alt text](image-405.png)
- if you open the file from here it will be opened as he encoded credentials
![alt text](image-406.png)
- if you opend from the url will not open as you already disable pulbic access
![alt text](image-407.png)
- create imges folder
![alt text](image-408.png)
![alt text](image-409.png)
- upload this file inside it
![alt text](image-410.png)

## lab 33 S3 bucket policy 

![alt text](image-411.png)
![alt text](image-412.png)
![alt text](image-413.png)
![alt text](image-414.png)
![alt text](image-415.png)
- go to permission from s3 
![alt text](image-416.png)
- open the public access
![alt text](image-417.png)
![alt text](image-418.png)
- edit
![alt text](image-419.png)
- to creat a policy from polic generator
![alt text](image-420.png)
- choose effect , principle , aws service and the arn of s3 end with *
![alt text](image-421.png)
- this is the output , copy it and put it at the policy 
![alt text](image-422.png)
![alt text](image-423.png)
- if you opened the link again it will work
![alt text](image-424.png)

## lab 34 S3 static website

- here th idea of static website 
![alt text](image-425.png)
- upload these files
![alt text](image-426.png)
- go to properities then static web site edit the enable it
![alt text](image-428.png)
- put index.html
![alt text](image-429.png)
![alt text](image-430.png)
- upload index.html
![alt text](image-431.png)
- open from this url
![alt text](image-432.png)
- worked
![alt text](image-433.png)

## lab 35 S3 versioning

- version idea
![alt text](image-434.png)
- to enable versioning from propertoies
![alt text](image-435.png)
![alt text](image-436.png)
- edited html file 
![alt text](image-437.png)
![alt text](image-438.png)
- to see versions
![alt text](image-439.png)
- if you deleted it 
![alt text](image-440.png)
- rolled back to the old one
![alt text](image-441.png)
- if you deleted coffe file , will show delete marker for it and you can delete this delete marker to rollback 
![alt text](image-442.png)

## lab 36 S3 replication 

- will create a two buckets and enable the versioning
![alt text](image-443.png)
![alt text](image-444.png)
![alt text](image-445.png)
- this is the second bucket 
![alt text](image-446.png)
![alt text](image-447.png)
- upload a file in first bucket 
![alt text](image-448.png)
- to create a replication rule 
![alt text](image-449.png)
![alt text](image-450.png)
- name of replication and enable it
![alt text](image-451.png)
- apply to all bucket
![alt text](image-452.png)
- choose the destination to be the second bucket
![alt text](image-453.png)
- create a role
![alt text](image-454.png)
![alt text](image-455.png)
![alt text](image-456.png)
- here upload a file in the first s3
![alt text](image-457.png)
- here it appeared at the second one using replication 
![alt text](image-458.png)
- Note: if you want to replicate delete marker 
![alt text](image-459.png)

## lab 37 S3 storage classess 

- idea
![alt text](image-460.png)
- create a bucket
![alt text](image-461.png)
![alt text](image-462.png)
- when upload any object you will determie which class
![alt text](image-463.png)
- he choose this
![alt text](image-464.png)
- you can change from here 
![alt text](image-465.png)
- from here to ceate the life cycle rule 
![alt text](image-466.png)
![alt text](image-467.png)
![alt text](image-468.png)
![alt text](image-469.png)
![alt text](image-470.png)
![alt text](image-471.png)
![alt text](image-472.png)

## lab 38 S3 life cycle rules  

- ceate rule 
![alt text](image-473.png)
![alt text](image-474.png)
![alt text](image-475.png)
![alt text](image-476.png)
- this is for transition
![alt text](image-477.png)
- this is for  expire 
![alt text](image-478.png)
- ths after creation
![alt text](image-479.png)

## lab 39 S3 Event notification

- idea
![alt text](image-480.png)
![alt text](image-481.png)
- create bucket
![alt text](image-482.png)
![alt text](image-483.png)
![alt text](image-484.png)
![alt text](image-485.png)
- turn on the event bridge feature
![alt text](image-486.png)
- create event notification
![alt text](image-487.png)
- give it a name 
![alt text](image-488.png)
- choose what you need , here all objects create events
![alt text](image-489.png)
- here choose sqs
![alt text](image-490.png)
- will create a new sqs
![alt text](image-491.png)
![alt text](image-492.png)
![alt text](image-493.png)
- go back to event notification and choose this
![alt text](image-494.png)
- here you will get an error and this is normal as the policy is not set
![alt text](image-495.png)
- go to sqs and edit access policy 
![alt text](image-496.png)
- from policy generator
![alt text](image-497.png)
- choose the sqs type policy, and effect allow,  principle * and action sendMessage
![alt text](image-498.png)
- put the arn of s3
![alt text](image-499.png)
- copy this
![alt text](image-500.png)
- and pu it at access policy then save
![alt text](image-501.png)
![alt text](image-502.png)
- if you go back and save here it will work again
![alt text](image-503.png)
![alt text](image-504.png)
![alt text](image-505.png)
- here the test message
![alt text](image-506.png)
- he uploaded a file at the s3 , you should find a message for it at the sqs
![alt text](image-507.png)
![alt text](image-508.png)
![alt text](image-509.png)

## lab 40 S3 Performance

- idea
![alt text](image-510.png)
![alt text](image-511.png)

## lab 41 S3 Encryption

- idea
![alt text](image-512.png)
![alt text](image-513.png)
![alt text](image-514.png)
![alt text](image-515.png)
![alt text](image-516.png)
- create a new s3
![alt text](image-517.png)
- enable versioning
![alt text](image-518.png)
- encryption options
![alt text](image-519.png)
![alt text](image-520.png)
- upload a file
![alt text](image-521.png)
- press on file and see encryption details and you can edit it
![alt text](image-522.png)
- uploaded another file on s3 and you can control encryption options while uploading
![alt text](image-523.png)


## lab 42 S3 CORS

- Idea if you want to get index.html file from server and the file contains images in another server with different origin, to access it so the other server should accept the cors
![alt text](image-524.png)
![alt text](image-525.png)
- the same idea from the client to access our s3 we should enable CORS headers 
![alt text](image-526.png)
- here handson, will test first if the two files in the same origin or same s3 
![alt text](image-527.png)
- this is a script will get this extra-page.html 
![alt text](image-528.png)
![alt text](image-529.png)
- he will upload these two files 
![alt text](image-530.png)
![alt text](image-531.png)
- from properties of s3 you open the static link file 
![alt text](image-532.png)
- it will work as the two files at the same origin
![alt text](image-533.png)
- will test first if the two files in the different origin or same s3, so he will create another s3 in another region
![alt text](image-534.png)
![alt text](image-535.png)
![alt text](image-536.png)
- will enable static web site
![alt text](image-537.png)
![alt text](image-538.png)
![alt text](image-539.png)
![alt text](image-540.png)
![alt text](image-541.png)
- will make this bucket be public
![alt text](image-542.png)
![alt text](image-543.png)
![alt text](image-544.png)
![alt text](image-545.png)
- upload extra-page file
![alt text](image-546.png)
![alt text](image-547.png)
- will delete the file from first s3
![alt text](image-548.png)
- if you tried to refresh the page 
![alt text](image-549.png)
- solution, we want to get the file from the other s3 , so we need the full path for it 
![alt text](image-550.png)
- edit the index.html and put the full path
![alt text](image-551.png)
- upload it again to replace the old one
![alt text](image-552.png)
- if you refresh and opened f12, will get error because the cors, this mean that the request went to the other bucket but didn't accept the request 
![alt text](image-553.png)
- solution : got to the other s3 and enable CORS
![alt text](image-554.png)
![alt text](image-555.png)
- it be like this 
![alt text](image-556.png)
- Note: this is the first s3 url should not have a / at the end like this
![alt text](image-558.png)
![alt text](image-557.png)
- try again and will work
![alt text](image-559.png)

## lab 43 S3 MFA delete

- idea
![alt text](image-561.png)
- create s3 and enable version
![alt text](image-560.png)
![alt text](image-562.png)
- note: it is disabled 
![alt text](image-563.png)
- will open the root account
![alt text](image-564.png)
- create access and secret key
![alt text](image-565.png)
- create a profile
![alt text](image-566.png)
![alt text](image-567.png)
- from this command will enable it 
```bash
# generate root access keys
aws configure --profile root-mfa-delete-demo

# enable mfa delete
aws s3api put-bucket-versioning --bucket mfa-demo-stephane --versioning-configuration Status=Enabled,MFADelete=Enabled --mfa "arn-of-mfa-device mfa-code" --profile root-mfa-delete-demo
```
![alt text](image-568.png)
- here it is enabled
![alt text](image-569.png)
- here he deleted a file but if you tried to delete the delete marker will not allowed
![alt text](image-570.png)
![alt text](image-571.png)
- solution: is to disable MFA or delete it from cli
```bash
# disable mfa delete
aws s3api put-bucket-versioning --bucket mfa-demo-stephane --versioning-configuration Status=Enabled,MFADelete=Disabled --mfa "arn-of-mfa-device mfa-code" --profile root-mfa-delete-demo

# delete the root credentials in the IAM console!!!
```
![alt text](image-572.png)
![alt text](image-573.png)

## lab 44 S3 access logs

- idea
![alt text](image-574.png)
- never ever do the logs in the same s3 as this will do a loop
![alt text](image-575.png)

- create another s3 
![alt text](image-576.png)
- from properities enable logs
![alt text](image-577.png)
![alt text](image-578.png)
- will enable and choose which s3 should be the target and store logs in it
![alt text](image-579.png)
- if you upload any thing in the original s3 , will see logs in dest s3
![alt text](image-580.png)
![alt text](image-581.png)

## lab 45 S3 Pre-Signed URL

- idea
![alt text](image-583.png)
- if the public access is disabled, the url will not work
![alt text](image-584.png)
- if you opened from here , it will work
![alt text](image-585.png)
- from here to share the presigned url
![alt text](image-586.png)
- choose the time you want
![alt text](image-587.png)
![alt text](image-588.png)
![alt text](image-589.png)

## lab 46 CloudFront S3 as origin

- idea
![alt text](image-590.png)
- s3 as origin
![alt text](image-591.png)
- create s3 bucket for cloud front
![alt text](image-592.png)
![alt text](image-593.png)
- uploaded these files
![alt text](image-594.png)
- I need access these files by using the cloudfront
![alt text](image-595.png)
![alt text](image-596.png)
- choose the origin to be the s3 bucket 
![alt text](image-597.png)
- create control setting 
![alt text](image-598.png)
![alt text](image-599.png)
- here you should create a policy at s3 to enbable the cloudfrot tp access th s3
![alt text](image-600.png)
- disable waf
![alt text](image-601.png)
- put index.html
![alt text](image-602.png)
- take copy 
![alt text](image-603.png)
- you can get it again from here
![alt text](image-612.png)
![alt text](image-613.png)
- then go to the s3 to create the policy 
![alt text](image-604.png)
![alt text](image-605.png)
- put what you copied from cloudfront here
![alt text](image-606.png)
![alt text](image-607.png)
- go to cloudfront to access it from this link
![alt text](image-608.png)
- if refresh it get it from cache for cloudfront 
![alt text](image-609.png)
![alt text](image-610.png)
![alt text](image-611.png)

## lab 47 CloudFront ALB/EC2 as origin

- idea
![alt text](image-615.png)
- it is prefered that the origin be loadbalancer not ec2 as we don't want to make the ec2 public 
![alt text](image-614.png)

## lab 48 CloudFront Georestriction 

- to allow or block requests to come from some countries 
![alt text](image-616.png)
![alt text](image-617.png)

## lab 49 AWS Global Accelerator , this lab is not free

- idea
![alt text](image-618.png)
- defference between cloudfront and aws global accelerator
![alt text](image-619.png)
- create ec2 first to run an app in us-east-1a
![alt text](image-620.png)
![alt text](image-621.png)
![alt text](image-622.png)
- created another ec2 at mumbai
![alt text](image-623.png)
- create a global accelerator
![alt text](image-624.png)
![alt text](image-625.png)
- choose port and protocol
![alt text](image-626.png)
![alt text](image-627.png)
- here the health check
![alt text](image-628.png)
- added the other for mumbai
![alt text](image-629.png)
![alt text](image-630.png)
- choose the endpoint for each one
![alt text](image-631.png)
![alt text](image-632.png)
- here it is created 
![alt text](image-633.png)
- to test it , will redirect you to the nearest one to you
![alt text](image-634.png)
- he changed his vpn 
![alt text](image-635.png)
![alt text](image-636.png)
- to test health check he will go to the security group and delete rule
![alt text](image-637.png)
![alt text](image-638.png)
- after some time this will be unhealthy
![alt text](image-639.png)
- for clean up terminate each ec2 then disable global accelerator and delete it 


## lab 50 Snow family

- idea
![alt text](image-640.png)
- from snow family
![alt text](image-641.png)
![alt text](image-642.png)
![alt text](image-643.png)
![alt text](image-644.png)
![alt text](image-645.png)

## lab 51 Amazon FSx

- idea of FSx, managed filesystem on aws 
![alt text](image-646.png)
![alt text](image-647.png)

## lab 52 Storage gatway (hybrid cloud)

- block, file and object storage 
![alt text](image-648.png)
- s3 file gateway
![alt text](image-649.png)
- FSx file gateway
![alt text](image-650.png)
- volume gw
![alt text](image-653.png)
- tape gw
![alt text](image-651.png)
- all of them
![alt text](image-652.png)
- create from here
![alt text](image-654.png)
![alt text](image-655.png)
![alt text](image-656.png)


# IAM service
## lab 53 organization

- Idea:
![alt text](image-912.png)
![alt text](image-913.png)
![alt text](image-914.png)
![alt text](image-915.png)
![alt text](image-916.png)
![alt text](image-917.png)
- Lab
![alt text](image-918.png)
- organization is a global service and here he created the master account  and child account to do the demo
![alt text](image-919.png)
![alt text](image-920.png)
- from master account he created the organization
![alt text](image-921.png)
- here if you want to add an account , create one or invite aws account
![alt text](image-922.png)
![alt text](image-923.png)
- here the invitation is sent from master account to child account
![alt text](image-924.png)
- here from the child
![alt text](image-925.png)
- here after accept invitation
![alt text](image-926.png)
- to organize your account we use OU 
![alt text](image-927.png)
- go to root
![alt text](image-928.png)
- then create OU 
![alt text](image-929.png)
- create DEV OU 
![alt text](image-930.png)
- ceated DEV TEST PROD OUs
![alt text](image-931.png)
- inside prod created these OUs
![alt text](image-932.png)
- to move to child account just selet it and move
![alt text](image-933.png)
![alt text](image-934.png)
![alt text](image-935.png)
- here after moving the child account into finance 
![alt text](image-937.png)

- should be like this 
![alt text](image-936.png)
- FYI: we made all of this to use the service control polic SCP 
- we need to restrict child account for dowing somethings 
- enable first scp 
![alt text](image-938.png)
![alt text](image-939.png)
![alt text](image-940.png)
- just the full control policy us created and we can create another one 
![alt text](image-941.png)
- create a one from deny access s3 
![alt text](image-942.png)
![alt text](image-943.png)
![alt text](image-944.png)
![alt text](image-945.png)
- if you click on root from here 
![alt text](image-946.png)
- will find full access 
![alt text](image-947.png)
- at prod  have two policies, one inherited from root and other is attached directly
![alt text](image-948.png)
![alt text](image-949.png)
- finance
![alt text](image-950.png)
![alt text](image-951.png)
- child
![alt text](image-952.png)
- here the denyAccess is inherited from finance
![alt text](image-953.png)
- to test it, go to child account and try to access s3 
![alt text](image-954.png)


## lab 54 IAM Advanced policies

- at left means deny anyone to do any thing except these two ranges of ips 
- at right means dny anything on ec2 rds dynamodb if you are in these regions eu-central-1 and eu-west-1
![alt text](image-955.png)
- at left means allow to stop or start ec2 if tag is dataAnalytics and user tag is data 
- at right means user can do any thing at ec2 but will deny to stop or terminate without having MFA 
![alt text](image-956.png)
- here it will apply at the bucket level , the above one to allow to list bucket , the bottom one is on object level 
![alt text](image-957.png)
- this will allow only the user which be part from the organization only 
![alt text](image-958.png)

## lab 55 IAM resource policy and role 

- here if you want to access s3 by using cross account , you have two options, first one to assume a role or to create a bucket policy at the s3 and identify who can access 
![alt text](image-959.png)
- here the difference between them, for assume role you will take all permissions from the account and your orginal permissions will not work, but with resource policy in this situation is more efficient 
![alt text](image-960.png)
- here some services need role and some others need resource based policy
![alt text](image-961.png)

## la 56 IAM permissions boundaries

- Idea: it is appplied only at roles and users not groups,
![alt text](image-962.png)
![alt text](image-970.png)
- for example here created a user with admin access 
![alt text](image-963.png)
![alt text](image-964.png)
![alt text](image-965.png)
![alt text](image-966.png)
- if he set the boundaries, will execute only what you give him at boundaries
![alt text](image-967.png)
- here he give only s3 access 
![alt text](image-968.png)
- here what will be effictive for john is the s3 access although he have full admin 
![alt text](image-969.png)
- here all the evaluation that be done 
![alt text](image-971.png)
- example
![alt text](image-972.png)


## lab 57 IAM Identity center 

- Idea: from one place can single signe one to your accounts
![alt text](image-973.png)
![alt text](image-974.png)
- here once login to th iam identity center then retrieve or restore user identiy from active directory or iam identuy center 
![alt text](image-975.png)
- here for example we have two users, will put them in a group and to give them permissions with permission set , full access on dev and read only on prod 
![alt text](image-976.png)
![alt text](image-977.png)

## lab 58 AWS Directory service

- idea of AD 
![alt text](image-978.png)
- here thwe aws managed microfsoft AD , trust between onprem AD and aws manged AD 
![alt text](image-979.png)
- AD connector : here if the request try to authenticate throug cloud, it will proxy it to the on prem AD 
![alt text](image-980.png)
- simple AD : if you don't have onprem AD 
![alt text](image-981.png)
- to integrate IAM identity center with active direcory 
![alt text](image-982.png)
- here if you connect to self managed direcory
![alt text](image-983.png)

## lab 59 AWS control tower 

- idea :
![alt text](image-984.png)
![alt text](image-985.png)


## Containers on AWS: ECS, Fargate, ECR, and EKS 
## Docker 
- Idea:
![alt text](image-986.png)
![alt text](image-987.png)
![alt text](image-988.png)
![alt text](image-989.png)
![alt text](image-990.png)
![alt text](image-991.png)

## ECS Idea

- you are responsible for the ECS2s which Containers are created on , each ec2 should have ECS agent 
![alt text](image-992.png)
- the other type is Fargate, here you don't provison the infra , it is serverless 
![alt text](image-993.png)
- IAM roles for ECS are two types (EC2 instance profile and ECS task role)
- EC2 instance profile: this for agent one ec2 to be aball to do api calls to ecs service, send container logs to cloud watch , pull images from ECR
- ECS task role: each task has a speceific role to enable you to acces other aws service like s3 or dynamodb 
![alt text](image-994.png)
- here integration between ECS and loadbalancer
![alt text](image-995.png)
- here between ECS and EFS 
![alt text](image-996.png)

## ECS handson

- create ecs
![alt text](image-997.png)
![alt text](image-998.png)
- here choose the type you want 
![alt text](image-999.png)
- create auto scaling group
![alt text](image-1000.png)
- choose t2.micro  and desired capacity 
![alt text](image-1001.png)
- didn't choose ssh key pair 
![alt text](image-1002.png)
- choose the default vpc and sec group setting
![alt text](image-1003.png)
![alt text](image-1004.png)
- if you go to the auto scaling group you will find a one is created for you by ECS
![alt text](image-1005.png)
- here the desired capacity that we already configured 
![alt text](image-1006.png)
- go back to the ECS, here the cluster is created
![alt text](image-1007.png)
- press on the name of ECS cluster , here at the infra there are three capacity providers 
![alt text](image-1008.png)
- if you go to auto scaling and edit this to be 1 
![alt text](image-1010.png)
![alt text](image-1009.png)
- in this moment an ec2 will be created by auto scaling service and will register itself to be a part of ECS cluster 
- here it is in service at the auto scaling 
![alt text](image-1011.png)
- and here it is part of the cluster 
![alt text](image-1012.png)


## ECS Create service and task definition 

- create a task definition
![alt text](image-1013.png)
- create nginx demo and will get the image from dockerhub
![alt text](image-1014.png)
![alt text](image-1015.png)
- chaoose launch type 
![alt text](image-1016.png)
- choose your task size 
![alt text](image-1017.png)
- here you can create task role if you want your containers to use AWS at for our demo no need  , and task execution role will be created automatic
![alt text](image-1018.png)
- here put the name and the image uri 
![alt text](image-1019.png)
- here port mapping 
![alt text](image-1020.png)
![alt text](image-1021.png)
- here after creation
![alt text](image-1022.png)
- let's launch this task definition as service from ECS cluser, go to ecs cluser and create a service 
![alt text](image-1023.png)
- choose launch type, will be fargate and the platform is latest 
![alt text](image-1024.png)
![alt text](image-1025.png)
![alt text](image-1026.png)
- for sec group 
![alt text](image-1027.png)
- create a loadbalancer
![alt text](image-1028.png)
- target group 
![alt text](image-1029.png)
![alt text](image-1031.png)
- here the service after creation 
![alt text](image-1030.png)
- here the details of it 
![alt text](image-1032.png)
- in the target group it is linked with the loadbalancer
![alt text](image-1033.png) 
- this is the ip address of the container
![alt text](image-1034.png)
- here the load balancer
![alt text](image-1035.png)
- copy the dns of load balancer and paste here 
![alt text](image-1036.png)
- this the task
![alt text](image-1037.png)
- and the logs 
![alt text](image-1038.png)
- events of the service 
![alt text](image-1039.png)
- here from service we can update there repolicas 
![alt text](image-1040.png)
![alt text](image-1041.png)
![alt text](image-1042.png)
- here the tasks
![alt text](image-1043.png)
- if you opend the dns again you will find more than containers are running 
![alt text](image-1044.png)
![alt text](image-1045.png)
- update the service again to be 0 because billing
![alt text](image-1046.png)
![alt text](image-1047.png)
![alt text](image-1049.png)
- and insure at the auto scaling that the desired is 0 
![alt text](image-1048.png)

## ECS service autoscaling 

- Idea
![alt text](image-1050.png)
![alt text](image-1051.png)
- here if the laod of the cpu increaesed so the cloudwatch metric will be triggred to cloudwatch alarm for the auto scaling service to created a new task 
![alt text](image-1052.png)

##   ECS - Solutions Architectures

- here an example
- 01 user upload any object to s3 
- 02 an event will sent to amzaon event bridge 
- 03 amazon event bridge have a rule to run ecs task 
- 04 the ecs task should have ecs task role to let the containers have  read and write for s3 and dynamo dab 
- 05 the task can now get data from s3 and put the result on dynamodb
![alt text](image-1053.png)
- another example
- here every one hour the amazon event bridge trigger a rule to create ECS task which should also have a task role to let containers access s3 
![alt text](image-1054.png)
- another example
- the ecs service haave more than one tasks whihc pull messages from sqs 
![alt text](image-1055.png)
- another example
![alt text](image-1056.png)

## ECS clean up 

- stop the service first and enusre that the desired tasks is 0 
![alt text](image-1057.png)
![alt text](image-1058.png)
![alt text](image-1059.png)
- then delete it. 
![alt text](image-1060.png)
- note that the cloudformation service will do this 
![alt text](image-1061.png)
![alt text](image-1062.png)
- after deleteion the service we can delete the cluster 
![alt text](image-1063.png)
- for the task definition dergister them 
![alt text](image-1064.png)

## ECR 

- here the ECR service is for saving images, and if ec2 wanted to pull images should the ec2 instances on it have IAM role 
![alt text](image-1065.png)

## EKS 

- here it is the k8s service 
![alt text](image-1066.png)
- here diagram 
![alt text](image-1067.png)
- EKS node type
- Manged node groups => aws create masters for you and you manage workers 
- self-managed nodes => you are responsible of it 
- fargate => all managed by aws 
![alt text](image-1068.png)
- here eks data volume 
![alt text](image-1069.png)

## EKS HandsOn

- here the eks will cost you money, don't do it with free tier
![alt text](image-1070.png)
![alt text](image-1071.png)
- put name ane version and create a cluser service role
![alt text](image-1072.png)
- will open a link and here the. steps you should follow 
![alt text](image-1073.png)
- 01 create a role 
![alt text](image-1074.png)
![alt text](image-1076.png)
![alt text](image-1075.png)
![alt text](image-1077.png)
![alt text](image-1078.png)
![alt text](image-1079.png)
- 02 go back to eks and choose the role 
![alt text](image-1080.png)
- 03 here where to deploy the cluser 
![alt text](image-1081.png)
- 04 choose the default sec group 
![alt text](image-1082.png)
- 05 cluster endpoint access here made it public 
![alt text](image-1083.png)
![alt text](image-1084.png)
- note: here after creating the cluster you should choose managed node group or fargate 
![alt text](image-1085.png)
- here if you go to resources 
![alt text](image-1086.png)
- 06 go to the compute to add node group (workers) 
![alt text](image-1087.png)
- put the name and create a role for node group 
![alt text](image-1088.png)
- create a role and the type should be ec2
![alt text](image-1089.png)
![alt text](image-1090.png)
- need AmazonEKSWorkrNodePolicy  
![alt text](image-1092.png)
- from the decomentation we need these also 
![alt text](image-1093.png)
![alt text](image-1094.png)
- 07 go back to eks and choose the role 
![alt text](image-1095.png)
- choose what you want here
![alt text](image-1096.png)
![alt text](image-1097.png)
- here means when you update how many nodes should be down
![alt text](image-1098.png)
- here the subnets
![alt text](image-1099.png)
![alt text](image-1100.png)
- here the other option if you want to creat nodes with fargate
![alt text](image-1101.png)
- here addons
![alt text](image-1103.png)
- from here the addons and if you want to install ebs addons
![alt text](image-1102.png)
- delete node group first then delete the cluster
![alt text](image-1104.png)


## Aws app runner 

- you don't need anything for infra , you can build and deploy your web app 
![alt text](image-1105.png)
- handson:  not free to do 
![alt text](image-1106.png)

- will get from ecr gallery
![alt text](image-1107.png)
![alt text](image-1108.png)
![alt text](image-1109.png)

- here to know the port
![alt text](image-1110.png)
![alt text](image-1111.png)
- auto scaling
![alt text](image-1112.png)
![alt text](image-1113.png)
- after creation
![alt text](image-1114.png)
![alt text](image-1115.png)
- here the logs 
![alt text](image-1116.png)
- delete app
![alt text](image-1117.png)

## Aws App2Container A2C

- this a cli tool to migrate and moderninzing java adn .net apps 
- lift and shift apps from onprem to cloud 
![alt text](image-1118.png)
![alt text](image-1119.png)


## Serverless Overviews from a Solution Architect Perspective

## Serverless 

- serverless menas that there are servers but you don'y manage them 
![alt text](image-1120.png)
- all of these services are serverless 
![alt text](image-1121.png)

## Lambda 

- here the need for lambda to do some task and here a compare with ec2
![alt text](image-1122.png)
![alt text](image-1123.png)
![alt text](image-1124.png)
- integration between lambda and all these services 
![alt text](image-1125.png)
- examples
![alt text](image-1126.png)
![alt text](image-1127.png)
- lambda prices 
![alt text](image-1128.png)

## lambda HandsOn

- if you go to lambda and at the end /begin , you will find that lambda support a lot of programming language 
![alt text](image-1129.png)
- here before 1 millions is free
![alt text](image-1130.png)
- after 1 million will pay
![alt text](image-1131.png)
- 01 create function
![alt text](image-1132.png)
- 02 choose the name and which progarming language 
![alt text](image-1133.png)
- 03 create an execution role 
![alt text](image-1134.png)
- this is the function code that is created automaticaly 
![alt text](image-1135.png)
- here after creation
![alt text](image-1136.png)
- here the code which be executed when to call the lambda function
![alt text](image-1137.png)
- to test function 
![alt text](image-1138.png)
- succeeded and git this value as a result
![alt text](image-1139.png)
- here the inputs of the function and if you remove a one and test again will fail
![alt text](image-1140.png)
- will fail
![alt text](image-1141.png)
- rolled back and save
![alt text](image-1142.png)
- from here to monitor
![alt text](image-1143.png)
- here the cloudwatch logs 
![alt text](image-1144.png)
![alt text](image-1145.png)
- logs of the first time for sucess
![alt text](image-1146.png)
- logs of the error
![alt text](image-1147.png)
- here the config of lambda 
![alt text](image-1148.png)
- here the role that allow lambda to access cloud watch
![alt text](image-1149.png)

## lambda limits

![alt text](image-1150.png)

## lambda concurreny
![alt text](image-1151.png)
- here you should caclulate your limit before this issue is done
![alt text](image-1152.png)
![alt text](image-1153.png)
![alt text](image-1154.png)
![alt text](image-1155.png)
- HandsOn
![alt text](image-1156.png)
![alt text](image-1158.png)
- to test it he make this 0
![alt text](image-1159.png)
- tried to test 
![alt text](image-1160.png)
![alt text](image-1161.png)
- to fix it go back and fix concurrency 
![alt text](image-1162.png)
![alt text](image-1163.png)

## lambda snap start 

- improve lambda function performance
![alt text](image-1165.png)

## lambda at VPC 

- network fundamental for lambda
- here by default the lambda can't access anything to your vpc
![alt text](image-1166.png)
- solution: you must define vpc id, subents and sec group, so lambda will create ENI in your subnets
![alt text](image-1167.png)
- we need this scenraio to ise the lambda with rds proxy as the rds proxy is not accesable pulbic
![alt text](image-1168.png)

## lambda with rds 

- here if we need the user once inset to rds so the rds invoke lambda function to send mail by using SES serrvice to users
![alt text](image-1169.png)
- here the notification about the data base itself not the data inside it 
![alt text](image-1170.png)

## Dynamodb

- it is nosql db 
![alt text](image-1172.png)
- dynamodb is rabidly evolve schema 
![alt text](image-1173.png)
- here example for it  
![alt text](image-1174.png)
- here the modes of dynamodb
![alt text](image-1175.png)

## Dynamodb lab (not free)

- create table
![alt text](image-1176.png)
- put the name of table, then put the partion key 
![alt text](image-1177.png)
- choose this for more options 
![alt text](image-1178.png)
- if you choose the on-demand so the pay will be as the actual read and write for app and this option is a good choice if you working on unpredectable workload  
![alt text](image-1179.png)
- here the second option if you want to put RCU and WCU 
![alt text](image-1180.png)
- here he siabled auto scaling and put the provisioned capacity uints for read and write
![alt text](image-1181.png)
- if you don't know you can let the system do it  
![alt text](image-1182.png)
- he made the example as this 
![alt text](image-1183.png)
- here the bills till now 
![alt text](image-1184.png)
![alt text](image-1185.png)
- after creation 
![alt text](image-1186.png)
- to create items 
![alt text](image-1187.png)
![alt text](image-1188.png)
- create another item 
![alt text](image-1189.png)
![alt text](image-1190.png)


## Dynamodb Advanced features


### dynamodb accelerator DAX

- it is goo for read congestion by caching and doesn'y require app logic modification 
![alt text](image-1191.png)

- difference between dynamodb and elasticache
![alt text](image-1192.png)

### dynamodb steam processing 
- here
![alt text](image-1193.png)
![alt text](image-1194.png)

### dynamodb global tables 
- here 
![alt text](image-1195.png)

### dynamodb TTL 

- here 
![alt text](image-1196.png)

### dynamodb bkp
- here 
![alt text](image-1197.png)

### dynamo db with s3 
- here 
![alt text](image-1198.png)


## API gateway

- the main idea that all REST APIs go to api gw then proxy these reuests to lambda function which do some processing then make CRUD to dynamodb
![alt text](image-1199.png)
- api gw have many features
![alt text](image-1200.png)
- api gw integrate with three things (lambda, http and aws service)
![alt text](image-1201.png)
- here an example
![alt text](image-1202.png)
- api gw endpoints (edge-opteimized, regional and prrivate)
![alt text](image-1203.png)
- api ge security
![alt text](image-1204.png)

### API gateway lab

- 01 we have more choices and choose REST api public 
![alt text](image-1205.png)
- put a name 
![alt text](image-1206.png)
- here the three endpoints 
![alt text](image-1207.png)
- choosed regional and create 
![alt text](image-1208.png)
- 02 create method 
![alt text](image-1209.png)
- here choose with lambda
![alt text](image-1210.png)
- will create a lambda function 
![alt text](image-1211.png)
![alt text](image-1212.png)
![alt text](image-1214.png)
- will use this code 
```bash 
import json

def lambda_handler(event, context):
    body = "Hello from Lambda!"
    statusCode = 200
    return {
        "statusCode": statusCode,
        "body": json.dumps(body),
        "headers": {
            "Content-Type": "application/json"
        }
    }
``` 
![alt text](image-1215.png)
- put here 
![alt text](image-1216.png)
- deploy this function
![alt text](image-1217.png)
- then test 
![alt text](image-1218.png)
![alt text](image-1219.png)
![alt text](image-1220.png)
- the test is working fine 
![alt text](image-1221.png)
- copy the arn of lambda
![alt text](image-1222.png)
- go back to the api gw 
![alt text](image-1223.png)
![alt text](image-1224.png)
- if you go to lambda 
![alt text](image-1225.png)
- if you go to configuration then permissions
![alt text](image-1226.png)
![alt text](image-1227.png)
- here the policy that created 
![alt text](image-1228.png)
- here from api gw , request go from client as a method request then integration request to lambda and the response from lambda till come back to customer 
![alt text](image-1229.png)
- to test it. 
![alt text](image-1230.png)
- here the result of the test 
![alt text](image-1231.png)
- from lambda he change the code and deploy again 
![alt text](image-1232.png)
- to onvoke lambda function again from api gw 
![alt text](image-1233.png)
- so if we go to cloudwatch service will get the logs 
![alt text](image-1234.png)
![alt text](image-1235.png)
- will create a new resource
![alt text](image-1236.png)
![alt text](image-1237.png)
- in /housed will create a new method
![alt text](image-1238.png)
![alt text](image-1239.png)
- will ctreate another lambda
![alt text](image-1240.png)
- go to lambda 
![alt text](image-1241.png)
![alt text](image-1242.png)
![alt text](image-1243.png)
- copy the arn and go to the api gw 
![alt text](image-1244.png)
- to test it. 
![alt text](image-1245.png)
![alt text](image-1246.png)
- to access them from UI , deploy API 
![alt text](image-1247.png)
![alt text](image-1248.png)
- copy this url
![alt text](image-1249.png)
- here /dev
![alt text](image-1250.png)
- here /houses
![alt text](image-1251.png)
- anything else 
![alt text](image-1252.png)

## AWS step function

- build serverless visual workflow 
![alt text](image-1253.png)

## Amazon Cognito 

- to give user an identity to interact with web and mobile app
![alt text](image-1254.png)
![alt text](image-1255.png)
![alt text](image-1256.png)
![alt text](image-1257.png)
![alt text](image-1258.png)
![alt text](image-1259.png)

## Serverless solution architect 

### first example my todo list

- need to do Architecture for this 
![alt text](image-1260.png)
- here the mobile client should authenticate for temp credentials from cognito then got to api gw wich verify the authentication from cogneto , then invoke lambda which query data from Dynamodb
![alt text](image-1261.png)
- here here the mobile client should authenticate for temp credentials from cognito then store and retrieve files on s3 
![alt text](image-1262.png)
- here the same but for high read throughput we use DAX before Dynamodb
![alt text](image-1263.png)
- here we can cache at the api gw 
![alt text](image-1264.png)
- conclusion 
![alt text](image-1265.png)

### second example my blog.com 

- this what we need to do 
![alt text](image-1266.png)
- as he saiad static content so we will use s3 and for global , we should use cloudfront
![alt text](image-1267.png)
- here for security will creat OAC at the s3 to ensure that the CloudFront will only access the s3 
![alt text](image-1268.png)
- for public REST API will user the api gw then lambdat then DAX then Dynamodb
![alt text](image-1269.png)
- for global tables will use Dynamodb global tables
![alt text](image-1270.png)
- to send a user a welcome msg, will use dynamodb stream which invoke lambda which should have IAM role to integrate with SES service to send mails
![alt text](image-1271.png)
- here if the user upload a file to s3 direct or using cloudfront , s3 will trigger a lambda to create thumbnails photos to othere s3 and from s3 we can integrate with sqs or sns 
![alt text](image-1272.png)
- conclusion
![alt text](image-1273.png)

## Microservices Architecture

- intro for Microservices
![alt text](image-1274.png)
- here if we have more than service and each one depends on other
![alt text](image-1275.png)
![alt text](image-1276.png)

## Software updates distribution
- if we have an app running on ec2 and each time you want to update it 
![alt text](image-1277.png)
- the issue here the updates at the efs 
![alt text](image-1278.png)
- it is better to use cloudfront
![alt text](image-1279.png)
- features for using cloudfront
![alt text](image-1280.png)

## Databases on aws 

- you need to answer these questions to determine which db is suitable for you 
![alt text](image-1281.png)
- here all the types of db 
![alt text](image-1282.png)

### RDS summary 

- it is managed Postgresql,mysql,oracle,sql server, db2, mariadb, custom 
![alt text](image-1283.png)

### Aurora summary

- compatible with api for Postgresql and mysql
![alt text](image-1284.png)

### elasticache

- it is a managed reedis and Memcached 
![alt text](image-1285.png)

### s3 

- here 
![alt text](image-1286.png)

### document db 
- here 
![alt text](image-1287.png)

### amazon neptun 
- here 
![alt text](image-1288.png)

### amazon keyspaces 
- here 
![alt text](image-1289.png)

### amazon QLDB 
- here 
![alt text](image-1290.png)

### amazon timestream 
- here 
![alt text](image-1291.png)
![alt text](image-1292.png)


## ection 22: Data & Analytics

### Athena (5$ per TB)
- this is a serverless service used to analyze data stored in s3 , and usd sql to query the files using the Presto engine
![alt text](image-1558.png)
- athena performance improve
  - columnar data
  - copress data 
  - partiion data sets
![alt text](image-1559.png)
- athena use lambda which integrate with alot of services and store the results at end at s3 
![alt text](image-1560.png)

### Athena Hands On (create db then create a table then query data from s3 and save it in another s3 )
- 01 go to Athena service 
![alt text](image-1562.png)
- 02 you should create s3 before to save results on it
![alt text](image-1561.png)
- creat s3
![alt text](image-1563.png)
![alt text](image-1564.png)
![alt text](image-1565.png)
- 03 go back to athena and select the s3 
![alt text](image-1566.png)
- so the results of the query should be at this bucket
![alt text](image-1567.png)
- 04 he already have another bucket which have more logs 
![alt text](image-1568.png)
- 05 he will use these commands 
```bash
create database s3_access_logs_db;

CREATE EXTERNAL TABLE IF NOT EXISTS s3_access_logs_db.mybucket_logs(
         BucketOwner STRING,
         Bucket STRING,
         RequestDateTime STRING,
         RemoteIP STRING,
         Requester STRING,
         RequestID STRING,
         Operation STRING,
         Key STRING,
         RequestURI_operation STRING,
         RequestURI_key STRING,
         RequestURI_httpProtoversion STRING,
         HTTPstatus STRING,
         ErrorCode STRING,
         BytesSent BIGINT,
         ObjectSize BIGINT,
         TotalTime STRING,
         TurnAroundTime STRING,
         Referrer STRING,
         UserAgent STRING,
         VersionId STRING,
         HostId STRING,
         SigV STRING,
         CipherSuite STRING,
         AuthType STRING,
         EndPoint STRING,
         TLSVersion STRING
) 
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.RegexSerDe'
WITH SERDEPROPERTIES (
         'serialization.format' = '1', 'input.regex' = '([^ ]*) ([^ ]*) \\[(.*?)\\] ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) \\\"([^ ]*) ([^ ]*) (- |[^ ]*)\\\" (-|[0-9]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) (\"[^\"]*\") ([^ ]*)(?: ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*))?.*$' )
LOCATION 's3://target-bucket-name/prefix/';


SELECT requesturi_operation, httpstatus, count(*) FROM "s3_access_logs_db"."mybucket_logs" 
GROUP BY requesturi_operation, httpstatus;

SELECT * FROM "s3_access_logs_db"."mybucket_logs"
where httpstatus='403';
```
- 06 create db 
![alt text](image-1570.png)
- 07 create a table on db 
![alt text](image-1571.png)
- FYI he got the command from documentation 
![alt text](image-1572.png)
![alt text](image-1573.png)
- here the table which is created and we can preview it 
![alt text](image-1574.png)
- select data from table 
![alt text](image-1575.png)
- results
![alt text](image-1576.png)
- another complex query
![alt text](image-1577.png)
![alt text](image-1578.png)
- another query to get unauthorized access 
![alt text](image-1579.png)


### Redshift (Analytics and dataware house )
- it is based on Postgresql but used at the OLAP not OLTP
![alt text](image-1580.png)
- architecture of readshift like k8s - leader and compute node , the query  is go to the leader then sent to the compute node 
![alt text](image-1581.png)
- Redshift  ha Multi-az mode for some cluster, for example here if you took a snapshot from origina cluster in a region the copy it to other regio and restore 
 ![alt text](image-1582.png)
- here three types of loading data into redshift 
  - from kinesis data firehouse: the data are come from services to kinesis data firehouse then sent to redshift 
  - copy data from s3 to redshift using gui or cli
  - app running on ec2 and send to redshift
![alt text](image-1583.png)
- here amazon redshif spectrum: using it to query data which on s3 without loading it in the cluster 
![alt text](image-1584.png)

### Opensearch - elastic search
- here the name become elastic search 
![alt text](image-1585.png)
- here if you made CRUD on dynamodb then dynamodb stream will call lambda func which call amazon open search and we can find from app on ec2 for example item id and retrieve it from dynamodb table
![alt text](image-1586.png)
- open saerch with cloud watch logs 
![alt text](image-1587.png)
- open search patterns 
![alt text](image-1588.png)

### EMR (Elastic MapReduce) - Help for Hadoop Cluster(Big data)

- Help for Hadoop Cluster(Big data)
![alt text](image-1589.png)
- nodes types and purchasing 
  - master node
  - core node
  - task node 
![alt text](image-1590.png)

### Quicksight 
- it is a service for creating interactive dashboards, in exam you will find quicksight with athena or redshift 
![alt text](image-1591.png)
- integration with some services 
![alt text](image-1592.png)
![alt text](image-1593.png)

### Glue 
- it is a serverless service used to extract data from s3 or rds then transform it then load it in redshift 
![alt text](image-1594.png)
- another example to convert data to parquet format 
  - put the data onto s3 then the Glue will import the data from s3 then the parquet will be saved on s3 , then athena will analyza it
  - or from first s3 will trigger lambda function which trigget Glue
![alt text](image-1595.png)
- here gluw data crawler get the data from s3, rds, dynamodb and write the data to glue data catalog 
![alt text](image-1596.png)
![alt text](image-1597.png)

### lake formation 
- is a central place to have all your data for analytics
![alt text](image-1598.png)
- data comes from alot of sources and ingest into data lake which stpre in s3 and the other services like, athena redshifrt emr and spark working on it 
 ![alt text](image-1599.png)
- the big advantage here you can manage the sec from one place on aws data lake 
![alt text](image-1600.png)

### managed serveices for apache flink
- Flink is a framework for processing data streams , here managed flink is reading dat from kinesis data streas and amazon msk 
![alt text](image-1601.png)

### managed serveices for apache flink lab
- here 
![alt text](image-1602.png)
![alt text](image-1603.png)

### MSK - Managed Streaming for Apache Kafka  
- this is alternative to amazon kinesis, both of them for stream data 
![alt text](image-1604.png)
![alt text](image-1605.png)
![alt text](image-1606.png)
![alt text](image-1607.png)
### Bigdata ingestion pipeline 
- like cicd but for big data , here what we want to do 
![alt text](image-1608.png)
- here all the integrated services 
![alt text](image-1609.png)
![alt text](image-1610.png)
## Machine Learning 


## Section 24: AWS Monitoring & Audit: CloudWatch, CloudTrail & Config

### CloudWatch Metrics
- cloud watch provides metrics for wvery service in aws 
![alt text](image-1428.png)
- here cloudwatch metric streams 
![alt text](image-1429.png)
- here all metrics 
![alt text](image-1430.png)
- metric for cpu 
![alt text](image-1431.png)

### CloudWatch Logs
- log group , log stream, log exiration policy , send logs to other services 
![alt text](image-1432.png)
- cloudwatch logs sources 
![alt text](image-1433.png)
- cloud logs insights 
![alt text](image-1434.png)
![alt text](image-1435.png)
- cloudwatch logs s3 export 
![alt text](image-1436.png)
- cloudwatch logs supscriptions 
![alt text](image-1437.png)
- cloudwatch logs aggregation multo account and multi regions
![alt text](image-1438.png)
- cloudwatch logs cross account 
![alt text](image-1439.png)

### CloudWatch Logs - Hands On
- here the log groups which created by other services 
![alt text](image-1440.png)
- one of them have 6 live streams, (run command id / instance id / stdout or stderr)
![alt text](image-1441.png)
- here the logs 
![alt text](image-1442.png)
- here to search inside logs 
![alt text](image-1443.png)
- here to create metric filters 
![alt text](image-1444.png)
- the pattern for example installing 
![alt text](image-1445.png)
- select from which log stream and test pattern 
![alt text](image-1446.png)
![alt text](image-1447.png)
![alt text](image-1448.png)
![alt text](image-1449.png)
![alt text](image-1450.png)
![alt text](image-1451.png)
![alt text](image-1452.png)
- to create an alarm
![alt text](image-1453.png)
- from here to subscription filters
![alt text](image-1454.png)
- here to edit retention settig 
![alt text](image-1455.png)
- here to export data to s3 
![alt text](image-1456.png)
- create log group 
![alt text](image-1457.png)
![alt text](image-1458.png)
- here log insights
![alt text](image-1459.png)

### CloudWatch Logs - Live Tail - Hands On
- will create log group 
![alt text](image-1460.png)
![alt text](image-1461.png)
- create a log stream 
![alt text](image-1462.png)
![alt text](image-1463.png)
- click on it 
![alt text](image-1464.png)
- start trailing and this is helpfull for debugging 
![alt text](image-1465.png)
- if you apply your filter 
![alt text](image-1466.png)
- go back to demologstream and from action - create log event 
![alt text](image-1467.png)
![alt text](image-1468.png)
![alt text](image-1469.png)
- if you go to the live tail it will appear 
![alt text](image-1470.png)


### CloudWatch Agent & CloudWatch Logs Agent

- cloud watch agent should be at the ec2 and it push the logs, make sure that IAM permissions are correct , the agent can be set up also at the onprem servers 
![alt text](image-1471.png)
- cloudwatch agent
  - cloudwatch logs agent: this is the old version and just only send to cloudwatch logs 
  - cloudwatch unfied agent: this is the newer version and can collet also other metrics
![alt text](image-1472.png)
- cloudwatch unified agent metrics 
![alt text](image-1473.png)

### CloudWatch Alarms
- here cloudwatch alarm
![alt text](image-1474.png)
- cloudwatch alarm target 
![alt text](image-1475.png)
- composit alarm
![alt text](image-1476.png)
- EC2 instance recovery
![alt text](image-1477.png)
![alt text](image-1478.png)

###  CloudWatch Alarms Hands On
- create ec2 
![alt text](image-1481.png)
- create alarm
![alt text](image-1480.png)
- select a metric 
![alt text](image-1482.png)
- with instance id seach
![alt text](image-1483.png)
- select cpu metric 
![alt text](image-1484.png)
![alt text](image-1485.png)
- here condition, if more than 95% , 3 times
![alt text](image-1486.png)
- here at ec2 action, will terniat the instance if the alarm in alarm status 
![alt text](image-1487.png)
![alt text](image-1488.png)
![alt text](image-1489.png)
- we should wait about 15 mins ، to do it quickly , so will do it with cloudshell 
![alt text](image-1490.png)
![alt text](image-1491.png)
- here it is in alarm
![alt text](image-1492.png)
![alt text](image-1493.png)
![alt text](image-1494.png)

## Amazon EventBridge 

- you can make cron jobs, event pattern , trigger lambda ,...
![alt text](image-1495.png)
- all at the lift cab send events so with amazon eventbridge you can make filter on these events and will generate json ducoment which describe these events then sent to many destinations 
![alt text](image-1496.png)
- here we have default event bus and also partner event bus , also there is custom event bus 
![alt text](image-1497.png)
- schema registery 
![alt text](image-1498.png)
- resource based policy for event bridge 
![alt text](image-1499.png)

###  Amazon EventBridge - Hands On

- here cloud watch events 
![alt text](image-1500.png)
- here the default bus that is created by default at your account and we can define rules on it 
![alt text](image-1501.png)
- create your own bus 
![alt text](image-1502.png)
![alt text](image-1503.png)
![alt text](image-1504.png)

- here the partener events , for example catch all events which come from auth0
![alt text](image-1505.png)
- go to rules and create a one 
![alt text](image-1507.png)
- put a name and rule type 
![alt text](image-1506.png)
- select a source
![alt text](image-1508.png)
- sample event 
![alt text](image-1509.png)
![alt text](image-1510.png)
![alt text](image-1511.png)
- but if you choose 
![alt text](image-1512.png)
![alt text](image-1513.png)
![alt text](image-1514.png)
![alt text](image-1515.png)
![alt text](image-1516.png)


## CloudWatch Insights and Operational Visibility

- here for containers 
![alt text](image-1517.png)
- here for lambda 
![alt text](image-1518.png)
- cloudwatch contributor 
![alt text](image-1519.png)
- app insihts 
![alt text](image-1520.png)
- summary
![alt text](image-1521.png)

##  CloudTrail Overview 

- is a sevice which collect in api at the account for any service 
![alt text](image-1522.png)
![alt text](image-1523.png)
- three types ov cloudTrain events 
![alt text](image-1524.png)
- cloudtrain insughts 
![alt text](image-1525.png)
- cloudtrail events retention

## CloudTrail Hands On
- at the event history, what happened last 90 days 
![alt text](image-1526.png)
- for exapmle will terminate the instance 
![alt text](image-1527.png)
- after 5 mins , here an api call for terminate instance and who did it 
![alt text](image-1528.png)
- all details 
![alt text](image-1529.png)


### CloudTrail - EventBridge Integration
- here an example 
![alt text](image-1530.png)
- another example 
![alt text](image-1531.png)


## AWS Config - Overview (not free)
- used it for auditing and compliance for aws resources
![alt text](image-1532.png)
- config rules 
![alt text](image-1533.png)
- config resources
![alt text](image-1534.png)
- remmediations 
![alt text](image-1535.png)
- notififcation 
![alt text](image-1536.png)

### AWS Config - Hands On(not free)

- go to config service 
![alt text](image-1537.png)
![alt text](image-1538.png)
![alt text](image-1539.png)
![alt text](image-1540.png)
![alt text](image-1541.png)
![alt text](image-1542.png)
- serched for example at sec groups 
![alt text](image-1543.png)
- there is no compliance till now 
![alt text](image-1544.png)
- create a rule 
![alt text](image-1545.png)
![alt text](image-1547.png)
![alt text](image-1548.png)
![alt text](image-1549.png)
![alt text](image-1550.png)
- if you go to resources 
![alt text](image-1551.png)
- here an exapmle of non compliant 
![alt text](image-1552.png)
- he deleted it 
![alt text](image-1553.png)
![alt text](image-1554.png)
- to change remeditation
![alt text](image-1555.png)

### CloudTrail vs CloudWatch vs Config
- here defference
![alt text](image-1556.png)
![alt text](image-1557.png)

## Section 26: AWS Security & Encryption: KMS, SSM Parameter Store, Shield, WAF
### encryption 101 

- TLS is the newer version of ssl, date is encrypted before sending it to the server , the examp le here if the client want to login to the server with user and pass so should be incrypted in the client and decrypted in the server 
![alt text](image-1293.png)
- Server side encryption: here the encryption at server side, the data is encrypted after send to the server then decrypted before go back to client
![alt text](image-1294.png)
- client side encryption: here the encryption and decryption are happen at the client side
![alt text](image-1295.png)

### KMS 

- here the concept of KMS 
![alt text](image-1296.png)
- KMS key types
  - Symmetric: single key is used for ecrypt and decrypt, services which is integrate with kms are using Symmetric key 
  - Asymmetric: public and private keys are using
![alt text](image-1297.png)
- AWS KMS keys 
  - AWS owned keys
  - AWS managed keys 
![alt text](image-1298.png)
- here to copy snapshot between two regions
  - ebs is encrypted with kms with key a
  - after create a snapshot form ebs it also encrypted with key a 
  - once transfet to the other region the snapshot should be rencrypted with key b
  - create ebs from snapshot in the other region with key b 
  ![alt text](image-1299.png) 
- kms key policies: like s3 policies
  - default kms key policy
  - custom kms key policy
  ![alt text](image-1300.png)
- here an example for copying snapshot across accounts 
![alt text](image-1301.png)

#### KMS lab
- here the kms managed keys
![alt text](image-1302.png)
- for example here the ebs key and here the key policy which define what should access this key 
![alt text](image-1303.png)
- here at the conditions should be your account and the service ec2 which acces ebs 
![alt text](image-1304.png)
- FYI: custom key store is for HMS and this out if scope 
![alt text](image-1305.png)
- let's create customer managed key , this cost 1 $ per month 
![alt text](image-1306.png)
- here will do it Symmetric
![alt text](image-1307.png)
![alt text](image-1308.png)
![alt text](image-1309.png)
- here he used the deafult key policy
![alt text](image-1310.png)
- here after createion 
![alt text](image-1311.png)
- here the key policy 
![alt text](image-1312.png)
- from here to configure key rotation 
![alt text](image-1313.png)
![alt text](image-1314.png)
![alt text](image-1315.png)
- here the on demand key rotation 
![alt text](image-1316.png)
- from here you can disable or schedual key deleteion
![alt text](image-1317.png)

### use the cli to encrypt or decrypt some data 

```bash
# 1) encryption
aws kms encrypt --key-id alias/tutorial --plaintext fileb://ExampleSecretFile.txt --output text --query CiphertextBlob  --region eu-west-2 > ExampleSecretFileEncrypted.base64

# base64 decode for Linux or Mac OS 
cat ExampleSecretFileEncrypted.base64 | base64 --decode > ExampleSecretFileEncrypted

# base64 decode for Windows
certutil -decode .\ExampleSecretFileEncrypted.base64 .\ExampleSecretFileEncrypted


# 2) decryption

aws kms decrypt --ciphertext-blob fileb://ExampleSecretFileEncrypted   --output text --query Plaintext > ExampleFileDecrypted.base64  --region eu-west-2

# base64 decode for Linux or Mac OS 
cat ExampleFileDecrypted.base64 | base64 --decode > ExampleFileDecrypted.txt


# base64 decode for Windows
certutil -decode .\ExampleFileDecrypted.base64 .\ExampleFileDecrypted.txt
```
- creat a file `ExampleSecretFile.txt` and put on it `SuperSecretPassword`
- this is the key that we created 
![alt text](image-1318.png)
- execut this 
```bash
aws kms encrypt --key-id alias/tutorial --plaintext fileb://ExampleSecretFile.txt --output text --query CiphertextBlob  --region eu-west-2 > ExampleSecretFileEncrypted.base64
```
![alt text](image-1319.png)
- this is the ecrypted file 
![alt text](image-1320.png)
- to encrypt it with base64 
```bash
cat ExampleFileDecrypted.base64 | base64 --decode > ExampleFileDecrypted.txt
```
![alt text](image-1321.png)
![alt text](image-1322.png)
- to decrypt it with base64 
```bash
aws kms decrypt --ciphertext-blob fileb://ExampleSecretFileEncrypted   --output text --query Plaintext > ExampleFileDecrypted.base64  --region eu-west-2
```
![alt text](image-1323.png)
![alt text](image-1324.png)
- base64 decode for Linux or Mac OS 
```bash
cat ExampleFileDecrypted.base64 | base64 --decode > ExampleFileDecrypted.txt
```
![alt text](image-1325.png)
![alt text](image-1326.png)

### KMS multi region key
- the idea here that the key is replicated to another regions
![alt text](image-1327.png)
- note: it is not recommended to use multi region key execpt at some use cases 
![alt text](image-1328.png)
- here if we want to encrypt some attributes 
![alt text](image-1329.png)
- same at global tables 
![alt text](image-1330.png)

### S3 replication with encryption
- here by default the unecrypted and ecrypted objects are replicated by default
![alt text](image-1331.png)

### Encrypted AMI sharing process 
- here the steps. 
![alt text](image-1332.png)


### SSM parameter store 
- it is a secure storage for configuration and secrets 
- here the app save some plain text or encrypted config on ssm parameter strore , which integrate with kms for encryption
![alt text](image-1333.png)
- hierarchy of parameter store 
![alt text](image-1334.png)
- price
![alt text](image-1335.png)
- some Advanced parameter tiers 
![alt text](image-1336.png)

### SSM parameter store  lab on CLI 
- 01 go to system manager then parameter store 
![alt text](image-1337.png)
![alt text](image-1339.png)
![alt text](image-1338.png)
- put a name and descriptiion 
![alt text](image-1340.png)
![alt text](image-1341.png)
- here after creation 
![alt text](image-1342.png)
- create another one with ssecure string 
![alt text](image-1343.png)
- he used the key that he created before at kms 
![alt text](image-1344.png)
![alt text](image-1345.png)
- create third one for prod 
![alt text](image-1346.png)
- creae fourth one for password 
![alt text](image-1347.png)
- here all of them 
![alt text](image-1348.png)
- let's get them from cli 
```bash
# GET PARAMETERS
aws ssm get-parameters --names /my-app/dev/db-url /my-app/dev/db-password
# GET PARAMETERS WITH DECRYPTION
aws ssm get-parameters --names /my-app/dev/db-url /my-app/dev/db-password --with-decryption

# GET PARAMETERS BY PATH
aws ssm get-parameters-by-path --path /my-app/dev/
# GET PARAMETERS BY PATH RECURSIVE
aws ssm get-parameters-by-path --path /my-app/ --recursive
# GET PARAMETERS BY PATH WITH DECRYPTION
aws ssm get-parameters-by-path --path /my-app/ --recursive --with-decryption
```
![alt text](image-1349.png)
![alt text](image-1350.png)
![alt text](image-1351.png)
![alt text](image-1352.png)
![alt text](image-1353.png)

### SSM Parameter Store Hands On (AWS Lambda)
- create a lambda function 
![alt text](image-1354.png)
![alt text](image-1355.png)
![alt text](image-1356.png)
- create a role for lambda which give permissions for lambda for cloudwatch logs 
![alt text](image-1357.png)
- put this code using boto3 
```bash
import json
import boto3
import os

ssm = boto3.client('ssm', region_name="eu-west-3")
dev_or_prod = os.environ['DEV_OR_PROD']

def lambda_handler(event, context):
    db_url = ssm.get_parameters(Names=["/my-app/" + dev_or_prod + "/db-url"])
    print(db_url)   
    db_password = ssm.get_parameters(Names=["/my-app/" + dev_or_prod + "/db-password"], WithDecryption=True)
    print(db_password)
    return "worked!"

```
![alt text](image-1358.png)
- test it. 
![alt text](image-1359.png)
![alt text](image-1360.png)
![alt text](image-1361.png)
- to test it again we got an error 
![alt text](image-1363.png)
![alt text](image-1362.png)
- it should boto3 
![alt text](image-1364.png)
- here another error as you don't have permission
![alt text](image-1365.png)
- solution: go to roles and search about hello-world-ssm-role 
![alt text](image-1366.png)
- will add inline policy 
![alt text](image-1367.png)
- choose service and search about system manager
![alt text](image-1368.png)
- put the action as this 
![alt text](image-1369.png)
![alt text](image-1370.png)
- and add the resources will allow anything under my-app/*
![alt text](image-1371.png)
![alt text](image-1372.png)
![alt text](image-1373.png)
![alt text](image-1374.png)
- if you go back to lambda
![alt text](image-1375.png)
- wait about 5 mins and test again 
![alt text](image-1376.png)
- here the logs 
![alt text](image-1377.png)
- add withDecryption=true parameter
![alt text](image-1378.png)
- he tested it again but we got an error as you don't have access for kms 
![alt text](image-1379.png)
![alt text](image-1380.png)
- solution: go to the role and add policies
![alt text](image-1381.png)
- add form kms 
![alt text](image-1382.png)
- FYI he used this key 
![alt text](image-1383.png)
![alt text](image-1384.png)
![alt text](image-1385.png)
- go back to lambda 
![alt text](image-1386.png)
- test again and worked 
![alt text](image-1387.png)
- here added this environment variable 
![alt text](image-1388.png)
- put it in the code 
![alt text](image-1389.png)
- save and test 
![alt text](image-1390.png)
- if put it as prod 
![alt text](image-1391.png)
![alt text](image-1392.png)

## AWS Secrets Manager Overview
- using it for store secrets 
![alt text](image-1393.png)
- secret manager for multi region
![alt text](image-1394.png)

### AWS Secrets Manager lab
- create a secret 
![alt text](image-1395.png)
- create other system type 
![alt text](image-1396.png)
![alt text](image-1397.png)
![alt text](image-1398.png)
- here if you want to replicat your secrets 
![alt text](image-1399.png)
- here another option if you create a secret with rds 
![alt text](image-1400.png)

## AWS certificate Manager ACM 
- used for easily provision, manage and deploy TLS certs 
- here the loadbalcner call ACM for certs and clients can access the loadbalancer with https 
![alt text](image-1401.png)
- here steps for requesting public cert 
![alt text](image-1402.png)
- here if the cert is out the ACM 
![alt text](image-1403.png)
- here a redirect rule on loadbalancer from http to https 
![alt text](image-1404.png)
- api gw endpoints 
![alt text](image-1405.png)
- api integration with api gw 
![alt text](image-1406.png)

## AWS WAF
- here WAF is deployed on ALB as it is layer 7 but not NLB as it is layer 4 
![alt text](image-1407.png)
- waf rules 
![alt text](image-1408.png)
- to use fixed ip with waf we can use global accelerator 
![alt text](image-1409.png)

## AWS Shield 

- protect you from DDOS 
![alt text](image-1410.png)

## AWS Firewall manager  
- manage rules in all accounts on aws organization
![alt text](image-1411.png)
- difference between them 
![alt text](image-1412.png)

## AWS Firewall manager and shield  lab 
- create a web acl 
![alt text](image-1413.png)
![alt text](image-1414.png)
- to add elb resource from here 
![alt text](image-1415.png)
- here to add rules 
![alt text](image-1416.png)
![alt text](image-1417.png)
![alt text](image-1418.png)
![alt text](image-1419.png)
![alt text](image-1420.png)
![alt text](image-1421.png)
![alt text](image-1422.png)
![alt text](image-1423.png)
![alt text](image-1424.png)
![alt text](image-1425.png)
- from here to create shield it is 3000$ per month :D
![alt text](image-1426.png)
![alt text](image-1427.png)
## Section 28: Disaster Recovery & Migrations


## CloudFormation (Infra as code )

- here what is cloudformation
![alt text](image-1611.png)
- benefits of cloudformatin
![alt text](image-1612.png)
![alt text](image-1613.png)
- visualize 
![alt text](image-1614.png)

## CloudFormation lab

- 01 create a stack 
![alt text](image-1615.png)
- 02 from a template uplaod this file , this will create an ec2 
```bash
---
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0453ec754f44f9a4a
      InstanceType: t2.micro

```
![alt text](image-1616.png)
- you can view it from app composer 
![alt text](image-1618.png)
![alt text](image-1617.png)
- 03 put the stack name 
![alt text](image-1619.png)
- 04 put a tag
![alt text](image-1620.png)
![alt text](image-1621.png)
- from here you can see the events
![alt text](image-1622.png)
- here you can see the resource 
![alt text](image-1624.png)
- here the template you uploaded
![alt text](image-1623.png)
- at the ec2 you find the created one by cloudformation
![alt text](image-1625.png)
- here at the tag you will find the tag that we put and also some tags the cloudformation put 
![alt text](image-1626.png)
- 05 you will update this stack
![alt text](image-1627.png)
- replace with this file
```bash
---
Parameters:
  SecurityGroupDescription:
    Description: Security Group Description
    Type: String

Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0453ec754f44f9a4a
      InstanceType: t2.micro
      SecurityGroups:
        - !Ref SSHSecurityGroup
        - !Ref ServerSecurityGroup

  # an elastic IP for our instance
  MyEIP:
    Type: AWS::EC2::EIP
    Properties:
      InstanceId: !Ref MyInstance

  # our EC2 security group
  SSHSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Enable SSH access via port 22
      SecurityGroupIngress:
        - CidrIp: 0.0.0.0/0
          FromPort: 22
          IpProtocol: tcp
          ToPort: 22

  # our second EC2 security group
  ServerSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: !Ref SecurityGroupDescription
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 192.168.1.1/32

Outputs:
  ElasticIP:
    Description: Elastic IP Value
    Value: !Ref MyEIP

```
![alt text](image-1628.png)
- 06 put the parameter of sec group description 
![alt text](image-1629.png)
- here at the change set , what will be change by the cloudformation
![alt text](image-1630.png)
- these are the events 
![alt text](image-1631.png)
- this the created ec2
![alt text](image-1635.png)
- here the created elastic ip 
![alt text](image-1633.png)
- here all resources
![alt text](image-1634.png)
- from template then view in composer
![alt text](image-1636.png)
![alt text](image-1637.png)
- FYI: delete from the cloudformation not the console 
![alt text](image-1638.png)

### CloudFormation - Service Role

- here means that you should as a user to have the rigt permission, then IAM role to cloudformation to to can creat/delete/update 
![alt text](image-1639.png)
- from IAM => roles => create role
![alt text](image-1640.png)
- choose aws service, cloudformation
![alt text](image-1641.png)
- for exaple give it full access for s3  
![alt text](image-1642.png)
- put a name
![alt text](image-1643.png)
![alt text](image-1644.png)
- go to cloudformation and create a stack 
![alt text](image-1645.png)
![alt text](image-1646.png)
![alt text](image-1647.png)
- here if you don't choose IAM role it will take your own permission as a user, so will choose the role that we created, so this role will be used in all stack operation 
![alt text](image-1648.png)

## Terrafrom

- here the link of the other repo `https://github.com/HaythamMohamd/nana-terraform-haytham.git`