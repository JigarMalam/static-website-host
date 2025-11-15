# Launching a Hello World Website on AWS EC2

_This guide outlines the steps to launch a basic "Hello World" website using an AWS EC2 instance with an Amazon Linux AMI (Amazon Machine Image), install the Apache HTTP Server (httpd), and configure it to be accessible via HTTP (Port 80) and HTTPS (Port 443), all within the AWS Free Tier limits._

## Prerequisites
*An active AWS Account (signed up for the Free Tier).*

### Basic knowledge of AWS console navigation.
*SSH Client (like PuTTY or the built-in Terminal/PowerShell) for connecting to the EC2 instance.*
*A Key Pair generated during the EC2 launch process (e.g., my-key.pem).*

#  Step-by-Step Guide
A. Launch the EC2 Instance
- This step provisions the virtual server that will host the website.
- Navigate to the EC2 Dashboard in the AWS Management Console.
- Click "Launch instances".
- Name and Tags: Give your instance a name, e.g., HelloWorldServer.
- Application and OS Images (AMI):
  - Search for or select Amazon Linux.
  - Choose the Amazon Linux 2023 AMI (or similar Free Tier eligible version).

2. Instance Type:
- Select t2.micro or t3.micro (ensure it's marked as Free tier eligible).

3. Key pair (login):
- Choose an existing key pair or Create a new key pair. You will need the private key file (.pem or .ppk) to connect later.

4. Network settings:

- Click "Edit" if needed.
  -   Create security group (or select an existing one).
  -   Crucially, add inbound rules for:
  -   Type: SSH, Source type: My IP or Anywhere
  -   Type: HTTP, Source type: Anywhere (0.0.0.0/0)
  -   Type: HTTPS, Source type: Anywhere (0.0.0.0/0)

5. Configure storage: Leave the default settings (usually 8 GiB General Purpose SSD, which is free-tier eligible).

6. Review and click "Launch instance".
   -Wait until the instance state changes from pending to running.

----
B. Connect to the EC2 Instance (SSH)
You will connect to the server using the public IP address and the key pair you created.

Select your running instance in the EC2 Dashboard.

Copy the Public IPv4 address or Public IPv4 DNS.

Open your SSH client (Terminal, PowerShell, PuTTY).

Use the SSH command (replace placeholders):

Bash

ssh -i /path/to/your/keyfile.pem ec2-user@<Your-Public-IP-Address>
Note: The default username for Amazon Linux is ec2-user.

Confirm the connection by typing yes if prompted about the host's authenticity. You should now be at the Linux command prompt.

----
C. Install and Configure the Web Server (httpd)
This section installs the web server and ensures it starts automatically.

Update the package list:

```

sudo su
yum  update -y
yum install httpd -y
cd /var/www/html
nano indext.html

```

*In index.html* --> <index.html>
_Save the file_
```
sevice httpd start
```


#### Clean Up (Avoid Charges)
-----
_To ensure you don't incur unexpected AWS charges, terminate the EC2 instance once you are finished testing.
Navigate back to the EC2 Dashboard in the AWS Console.
Select the HelloWorldServer instance._

Click "Instance state" -> "Terminate instance".

Confirm the termination.
