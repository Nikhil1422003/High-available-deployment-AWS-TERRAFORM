# High-available-deployment-AWS-TERRAFORM
High availability deployment in AWS using TERRAFORM
# Project Description
 This project demonstrates the implementation of a high availability infrastructure in AWS using Auto Scaling Groups (ASG) and Elastic Load Balancers (ELB) with Terraform. It also includes the setup of VPC, subnets, Internet Gateway (IG), and route tables.This project will showcase the creation of a robust and highly available infrastructure on Amazon Web Services (AWS) using Terraform.

# Key features of this project 
1.**Auto Scaling Groups (ASG)**: I set up Auto Scaling Groups to dynamically adjust the number of instances based on traffic patterns, ensuring optimal resource utilization and reliability.

2.**Elastic Load Balancers (ELB)**: Elastic Load Balancers are used to evenly distribute incoming traffic across multiple instances, eliminating single points of failure and enhancing availability.

3.**Fault Tolerance**: Our infrastructure is designed to be fault-tolerant, capable of withstanding component failures without causing downtime. This is achieved through redundancy and failover mechanisms & situations.

4.**Virtual Private Cloud (VPC)**: For a dedicated virtual network for my resources

5.**Internet Gateway (IG)**: To allow communication between your VPC and the public internet.

6.**Route Tables**: Defining routing rules to direct traffic within the VPC and to the IG

5.**Subnets**: For subdivisions of the VPC to host my instances in different availability zones.
# Prerequistes
 1.Basic knowledge of AWS services
 
 2.Knowedge about Terraform and infrastructure as code principles

# Terraform Configuration
The Terraform configuration files with(*.tf) in this repository define the AWS resources and settings required to create the high availability infrastructure.

#### Step 1 : Setting up the Environment

We need a ec-2 instance to create this infrastructure then after connecting the instance we need create a directory inside it and we need to configure our credentials throught this command (aws configure) then provide access key and secret key to get configure then we need to install terraform from hashicrop website through this command we can installl on amazon linux (sudo yum install -y yum-utils shadow-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum -y install terraform) after installing check version if we need with (terraform --version) command.

#### Step 2 : Installing necessary Plugins

We have to ensure the necessary Terraform plugins installations. You have to create a new file with .tf extension Then run the below command for plugins installation
```
terraform init
```

#### Step 3 : Creating a Separate VPC Infrastructure

We have to define and provision a Virtual Private Cloud (VPC) infrastructure. The Terraform configuration files for this step can be found as [vpc.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/vpc.tf) , [subnets.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/subnet.tf) , [internet-gateway.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/internet-gateway.tf) , [route-table.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/route-table.tf) in my repository , alal thr above mentioned files have requried configuration to create a virtual network in my infrastructure.

#### Step 4 : Creating Security Group

We have to Set up a security group for Auto Scaling group and Load Balancer to control inbound and outbound traffic for our instances. Configuration files for this step can be found in [alb-security.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/alb-security.tf)  and [asg-security.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/asg-security.tf)file in this repository that are included with necessary security groups that we needed to create security .

#### Step 5 : Creating Target Group

We have to create an Elastic Load Balancer target group to route traffic to instances within our Auto Scaling Group. Configuration files  for this step can be found in [target-group.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/target-group.tf) file in this repo and also add the user data script file form [user-data.sh](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/user-data.sh) .

#### Step 6 : Creating Load Balancer

Next we have to set up an Elastic Load Balancer (ELB) to distribute incoming traffic across our instances. The ELB configuration can be found in the [application-load-balancer.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/application-load-balancer.tf) file .

#### Step 7 : Defining Launch Template

We have to define a launch template specifying instance configuration details for your Auto Scaling Group. Configuration files for this step are located in the [launch-template.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/launch-template.tf) file.

#### Step 8 : Creating Auto Scaling Group

Finally we have to create an Auto Scaling Group (ASG) to automatically adjust the number of instances based on traffic or resource utilization. ASG configuration files for are located in the [asg.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/asg.tf) file this repo.

#### Step 9 : Providing values for Variables

Till now, we have only assign variables without hardcoding values to them . Create two files with name variables.tf for variable declaration and terraform.tfvars for assign values to variables declared , Copy the [variables.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/variables.tf)  and [terraform.tfvars](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/terraform.tfvars) files from my repo.

#### Step 10 : Getting DNS as Output

We don't have to necessarily need to go to console for fetch the DNS name We can get it in terminal using output concept . Configuration files for this step are located in the [output.tf](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/blob/main/output.tf) file in this repository.


**As we mentioned in the output.tf file we will get loadbalancer DNS then we can paste that DNS in browser we will get our output after we apply below commands**


#### Step 11 : Application

Once the above-mentioned steps are completed, apply the following commands to create the resources:
```
terraform plan
```
The above command will provide you with a preview of the resources that are going to be created.
```
terraform apply -auto-approve
```


The above command will create the resources defined in our configuration. Shortly after, the Auto Scaling Group (ASG) will launch instances and deploy our application on those instances , You can see final output like below picture :

![aws-project1 1](https://github.com/Nikhil1422003/High-availblle-deployment-AWS-TERRAFORM/assets/155822950/2514ac71-fca9-4ebe-8971-382cbfef9b66)

