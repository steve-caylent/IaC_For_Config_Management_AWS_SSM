# IaC For Config Management - AWS State Manager and Run Command

AWS Systems Manager has two other important features when it comes to config management; State Manager and Run Command. These two features allows you to automate management tasks in a secure and easy to use way. Better security is provided over traditional SSH and incoming port 22 doesn't need to be open. All connections are audited by CloudTrail and permissions can be controlled using IAM. Ansible can now be used to deploy runbooks in a more secure fashion.
<br />
<br />
[Back to README](../README.md)


## Setting up the environment

Use the same cloudformation template (below) that is used in the Session Manager demo. This will create EC2's to connect to using Ansible <br />
* SSM-Without-Bastion.yml *- for accessing EC2 via Session Manager*
<br />

![SSM Without Bastion](https://user-images.githubusercontent.com/90650872/137347013-349e1139-a523-4fdf-a4c3-1b4d78e8041d.png)

**State Manager and Run Command can deploy Ansible to EC2 and Remote VM's with Systems Manager Agent installed**
![AWS SSM High Level](https://user-images.githubusercontent.com/90650872/137359824-852ab878-5015-4b8f-81f0-a84851e7b818.png)



### Installing Ansible on target instances
Ansible must be installed on the EC2 instances you intend to use. That can be done during the bootstrap process but in this example you can install it manually or with `Run Command`. See below for installing

`sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm`<br />
`sudo yum -y install ansible`

![UsingRunCommand](./images/run.png)

![ShellCommand](./images/shell.png)

![AnsiblePlaybook](./images/commandparameters.png)

![RunAnsible](./images/runansible.png)

![InstallAnsible](./images/install.png)

![CheckEc2](./images/check.png)








## Finished!

And it's as easy as that! In a few steps you've created SSM Session Manager endpoints for access to EC2 in private subnets AND with no open ports!
The benefit of having the SSM VPCE's is that you can now use Systems Manager to Run Commands, install updates and scan using Inspector.<br />
Check here for more info on Systems Manager [AWS SSM](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)

## Author
Caylent Inc.






