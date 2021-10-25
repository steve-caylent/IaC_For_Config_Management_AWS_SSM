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


### Using AWS Systems Manager Run Command
Navigate over to AWS Systems Manager and select Run Command. This service is able to run commands as part of config management. 
![UsingRunCommand](./images/run.png)

### Selecting appropriate Run Command
There are several commands you can choice from. In order to install ansible using Run Command we will have to use a Shell Command. Select it and in the commands paste in 
`sudo yum -y install ansible`. For instances, select the 3 instances created in private subnets. Ignore output to S3 and run the command! 

![ShellCommand](./images/shell.png)

And just like that ansible has been installed on all of the selected instances!

![InstallAnsible](./images/install.png)

## Deploying to Instances using Ansible Playbook
Systems Manager Run Command has many options for different commands, one of them being Running Ansible Playbooks. That's exaxtly what we need so in this case make the appropriate selection below.

![RunAnsible](./images/runansible.png)

### Running Ansible Playbook
Use the ansible playbook provided in this solution (playbook.yml). Copy and paste the contents in the command parameters and select the 3 instances as you did before. This playbook will install httpd on all 3 instances. 

![AnsiblePlaybook](./images/commandparameters.png)


### Success
Great! Now if you want to make sure that everything was installed correctly, use Session Manager to connect into one of the 3 instances.

![CheckEc2](./images/check.png)


## Finished!

And it's as easy as that! In a few steps you've managed to see the power of using Run Command both with and without Ansible. Enjoy!<br />
Check here for more info on Systems Manager [AWS SSM](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)

## Author
Caylent Inc.






