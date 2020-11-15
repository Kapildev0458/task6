# task6
# #vimaldaga #righteducation #educationredefine #rightmentor #worldrecordholder #linuxworld #makingindiafutureready #righeudcation #arthbylw
1.Webserver configured on EC2 Instance

![0](https://user-images.githubusercontent.com/69908356/99188417-d0116f00-2781-11eb-9c28-44397b08bd1f.png)


2.Document Root(/var/www/html) made persistent by mounting on EBS Block Device.

![1](https://user-images.githubusercontent.com/69908356/99188492-4c0bb700-2782-11eb-8e43-cef8fc66f48a.png)
![2](https://user-images.githubusercontent.com/69908356/99188500-5af26980-2782-11eb-9a68-0e46a4668176.png)


3. Static objects used in code such as pictures stored in S3

![3](https://user-images.githubusercontent.com/69908356/99188556-82493680-2782-11eb-824d-50b897427ae3.png)
![4](https://user-images.githubusercontent.com/69908356/99188567-8f662580-2782-11eb-996c-3bf30db3f76e.png)
![5](https://user-images.githubusercontent.com/69908356/99188577-9c831480-2782-11eb-88ee-5fa33bd85f06.png)


4. Setting up Content Delivery Network using CloudFront and using the origin domain as S3 bucket.

![6](https://user-images.githubusercontent.com/69908356/99188600-b4f32f00-2782-11eb-8b71-c9d3a7d2b6e3.png)


5. Finally place the Cloud Front URL on the webapp code for security and low latency.

Before starting this task I want to tell you some thing like …in this task we half of the part we discussed in earlier practical i.e configuring ec2-instance.

Now in remaining task I have created entire infrastructure via aws cli like

1.Partition , formatting,mounting

2.Creating S3 bucket via cli and make it public

3. Putting object in s3-bucket and make it public via cli

4. Creating Cloud-Front Distribution via cli.

Now we can proceed:

Start the Instance:

![7](https://user-images.githubusercontent.com/69908356/99188636-f71c7080-2782-11eb-9840-1cf331fb5c6b.png)

Creating Volume:

b)aws ec2 create-volume --availability-zone ap-south-1b --size 1 --volume-type gp2

![8](https://user-images.githubusercontent.com/69908356/99188653-10252180-2783-11eb-9c56-b0532825bccd.png)

Attaching Volume:

c)aws ec2 attach-volume --volume-id vol-04f06a070e8618d64 --instance-id i-0fa5e4208a4ecbc34 --device /dev/xvdb

![9](https://user-images.githubusercontent.com/69908356/99188663-2337f180-2783-11eb-9197-7253850b5bee.png)

Creating Partition:



Formatting partition:

e)mkfs.ext4 /dev/xvdb

Mounting a directory:

f)mount /dev/xvdb/ var/www/html

Installing apache webserver:

g) yum install httpd

Start httpd and status of httpd:

h)systemctl start httpd

i)systemctl status httpd

Now Here I am going to create s3 bucket via cli and putting object in it also cli

Create S3 bucket:

aws s3api create-bucket --bucket rang12 --region ap-south-1 --create-bucket-configuration LocationConstraint=ap-south-1

This is the step of making s3 bucket public:

Making Bucket Public:

aws s3api put-bucket-acl --acl public-read --bucket rang12

Here I am making bucket object public but here access policy is only download and read instead of read on webserver. Here this policy download object first and after download we can read it. You can change this policy by changing –acl rule like private,public-read,public-read-write etc

Creating Cloudfront Distribution:

aws cloudfront create-distribution --origin-domain-name rang12.s3.amazonaws.com

![10](https://user-images.githubusercontent.com/69908356/99188705-62fed900-2783-11eb-801a-0f3ac6b10e8b.png)
![11](https://user-images.githubusercontent.com/69908356/99188711-6db96e00-2783-11eb-9b36-03fe20de1e17.png)
![12](https://user-images.githubusercontent.com/69908356/99188722-7e69e400-2783-11eb-92c2-6ed25a96cfc6.png)
![13](https://user-images.githubusercontent.com/69908356/99188751-a35e5700-2783-11eb-94ec-6f43a884511d.png)
![14](https://user-images.githubusercontent.com/69908356/99188749-a0fbfd00-2783-11eb-8f5f-45fd48fe6bc1.png)
