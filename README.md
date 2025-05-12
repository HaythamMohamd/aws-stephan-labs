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