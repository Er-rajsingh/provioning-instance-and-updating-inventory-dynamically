# provioning-instance-and-updating-inventory-dynamically
This is useful when we need to provision ec2-instance and configure any thing into it without updating IP in inventory file.

Pre - instruction for this tasks --->
============================
1) Install the ansible using pip module<br/>
	#pip3 install ansible<br/>
2) Install sshpass software using epel release repo<br/>
	#yum install sshpass<br/>
3) Install boto3 library for using aws API<br/>
	#pip3 install boto3 --> for using aws_automate1.yml<br/>
	#pip3 install boto   --> for using aws_automate.yml<br/>
4) Create directory using command - #mkdir /etc/ansible<br/>
5) Put the file "ansible.cfg" into /etc/ansible folder<br/>
	#mv ansible.cfg  /etc/ansible  -->  clone the repo in root folder<br/>
6) Change directory by #cd /aws<br/>
        i) Edit only "aws_var.yml"  and put all informations there<br/>
       ii) After modifying the "aws_var.yml" file run any of the playbook i.e., aws_automate.yml or aws_automate1.yml<br/><br/>

Now let start --><br/><br/>

Provisioning EC2-instance and configuring Web Server into it
===================================================

Step 1 - Provisioning EC2-Instance on the aws<br/>
 - m ec2_instance:<br/>
  &nbsp;&nbsp;&nbsp;-a  "	Key_name: key_pair name<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;instance_type: t2.micro<br/>
&nbsp;&nbsp;&nbsp;&nbsp;image_id: image id which you want to launch as OS[ ami-xxxxx]<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;name: "Your OS name"<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;vpc_subnet_id: subnet-xxxxxx  #your subnet id<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;network:<br/>
	        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;assign_public_ip: yes<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;region: region name<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;state: present<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;security_group: sg-xxxxxxxxxxxx  #your precreated security group<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;aws_access_key: Your_access_keys #created from using IAM servive of aws<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;aws_secret_key: your_secret_keys  #created from using IAM servive of aws<br/><br/><br/>

Step 2 - Retrieving the IP and copying into the inventory file<br/><br/>
&nbsp;&nbsp;&nbsp;-m copy<br/>

Step 3 - Installing Webserver into this instance<br/><br/>
&nbsp;&nbsp;&nbsp;-m package<br/>

Step 4 - creating the webpage <br/>
&nbsp;&nbsp;&nbsp;-m copy<br/>

Step 5 - Starting the httpd services<br/>
&nbsp;&nbsp;&nbsp;-m service<br/>

	
