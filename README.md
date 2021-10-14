# IaC For Config Management - AWS SSM Session Manager

AWS Systems Manager allows for Config Management of your EC2 Instances. AWS Systems Manager allows you to connect to EC2 instanes to perform Run Commands (similar to Ansible) only with accessing via SSH. The benefit of using AWS SSM Session Manager is to give you access to EC2 instances in private subnets without having to use a Bastion Host. Session Manager allows you to access your EC2s within private subnet directly from the AWS console or the AWS CLI. Using a Bastion Host, leaves your EC2 machines vulnerable to attack on port 22. Money is another factor to consider. Having an EC2 running as a Bastion Host can be costly. Reduce costs and tighening security are great reasons to consider using Session Manager.

### Accessing EC2 in private subnets via a Bastion Host in a public subnet
The traditional way to access machines with private IPs is to first connect to a Bastion Host with a public IP and then forward into the machines with private IPs only. In this initial setup we will connect to the private subnet using a Bastion Host.

### What will be created with initial environment

The initial environment will have the following:
* A VPC with IGW
* 3 public subnets
* EC2 Bastion Host in public subnet
* Security Group for Bastion Host allowing port 22 inbound
* public route
* 3 NAT Gateways for High Availability
* 3 private subnets
* 3 EC2 Instances - 1 in each private subnet
* Security Group for EC2 instances allowing port 22 inbound from Bastion Host
* 3 Routes for private subnets/NAT Gateways


## Setting up the environment

Use the cloudformation template below to set up the initial environment with an EC2 Bastion Host in a public subnet<br />
* SSM-Bastion.yml *- for the initial setup environment*
<br />

![SSM_Bastion](https://user-images.githubusercontent.com/90650872/137347028-8a968a1f-acd2-4f6f-adbc-fbb686e80990.png)

As usual wait out the setup...


### Accessing Bastion Host => Private EC2



### What will be created with Session Manager environment

The updated environment will have the following:
* A VPC with IGW
* 3 public subnets
* <strike>EC2 Bastion Host in public subnet</strike>
* <strike>Security Group for Bastion Host allowing port 22 inbound</strike>
* public route 
* 3 NAT Gateways for High Availability
* 3 private subnets
* 3 EC2 Instances - 1 in each private subnet
Security Group for EC2 instances <strike>allowing port 22 inbound from Bastion Host</strike> outbound port 443 only
* 3 Routes for private subnets/NAT Gateways
* 3 SSM Endpoints - 1 in each private subnet
* 3 SSM Messages Endpoints - 1 in each private subnet
* 3 SSM EC2 Messages Endpoints - 1 in each private subnet
* Security group for VPCE with inbound port 443 allowing the EC2 SG an outbound port 443 for the VPC.

### Requirements for using SSM Session Manager
* A role with attached to the EC2 in private subnet to access Session Manager.
* OS that supports SSM agent (using Linux in demo)
* SSM agent installed/started in instance (Amazon Linux 2 has by default)
* 3 VPCE endpoints for linux EC2 (Windows EC2 requires 4)
* Security Group for VPC endpoints allowing EC2 to communicate with System Manager (port 443)

## Setting up the environment for Session Manager

Use the cloudformation template below to set up the environment removing the EC2 Bastion Host and creating SSM endpoints<br />
* SSM-Without-Bastion.yml *- for accessing EC2 via Session Manager*
<br />

![SSM Without Bastion](https://user-images.githubusercontent.com/90650872/137347013-349e1139-a523-4fdf-a4c3-1b4d78e8041d.png)


As usual wait out the setup...


# Finished!

And it's as easy as that! In a few steps you've created a dynamic VPN connection between your on-premises and AWS environments. Enjoy your connectivity.

Check out the official documentation for an alternative way of learning https://docs.aws.amazon.com/vpn/latest/s2svpn/SetUpVPNConnections.html



