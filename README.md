# aws

Infrastructure as a Service (IaaS):<br>
Definition: IaaS provides virtualized computing resources over the internet. Users can rent virtual machines, storage, and networking components on a pay-as-you-go basis.<br>
Examples in AWS:
1. Amazon EC2 (Elastic Compute Cloud): Offers resizable compute capacity in the form of virtual servers.
2. Amazon S3 (Simple Storage Service): Provides scalable object storage in the cloud.
3. Amazon VPC (Virtual Private Cloud): Allows users to provision a logically isolated section of the AWS Cloud where they can launch AWS resources.<br>

Platform as a Service (PaaS):<br>
Definition: PaaS provides a platform that allows customers to develop, run, and manage applications without dealing with the complexities of infrastructure management.<br>
Examples in AWS:
1. AWS Elastic Beanstalk: Enables easy deployment and management of applications, handling infrastructure provisioning and scaling automatically.
2. AWS Lambda: A serverless computing service that runs code in response to events without the need for server provisioning or management.
3. Amazon RDS (Relational Database Service): Manages database operations, including backups, patch management, and scaling.<br>

Software as a Service (SaaS):<br>
Definition: SaaS delivers software applications over the internet, eliminating the need for users to install, maintain, and update the software on their devices.<br>
Examples in AWS:
1. Amazon WorkMail: A secure and managed business email and calendaring service.
2. Amazon Chime: A communication service that includes online meetings, video conferencing, and business chat.
3. Amazon Connect: A cloud-based contact center service that makes it easy to set up and manage a customer contact center.



ports open for working<br>
SSH - 22<br>
HTTP -80<br>
HTTPS - 443<br>


# Setting Up AWS CodeDeploy Agent on Ubuntu EC2
script for code deploy for aws ec2 connetcion between ec2 and code deploy<br>
#!/bin/bash <br>
#This installs the CodeDeploy agent and its prerequisites on Ubuntu 22.04.  <br>
sudo apt-get update <br>
sudo apt-get install ruby-full ruby-webrick wget -y <br>
cd /tmp <br>
wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/releases/codedeploy-agent_1.3.2-1902_all.deb <br>
mkdir codedeploy-agent_1.3.2-1902_ubuntu22 <br>
dpkg-deb -R codedeploy-agent_1.3.2-1902_all.deb codedeploy-agent_1.3.2-1902_ubuntu22 <br>
sed 's/Depends:.*/Depends:ruby3.0/' -i ./codedeploy-agent_1.3.2-1902_ubuntu22/DEBIAN/control <br>
dpkg-deb -b codedeploy-agent_1.3.2-1902_ubuntu22/ <br>
sudo dpkg -i codedeploy-agent_1.3.2-1902_ubuntu22.deb <br>
systemctl list-units --type=service | grep codedeploy <br>
sudo service codedeploy-agent status <br>
