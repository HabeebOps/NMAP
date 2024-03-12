# Linux Project - Simple Network Scanner Web App (nmap)

Below are prerequisites needed for the project:

## Prerequisites:

- Linux Environment (Ubuntu)
- AWS EC2 instance
- Basic understanding of Cron Jobs for Scheduled Tasks (crontab)
- Basic knowledge of Apache2 webserver installation and management
- Familiarity with PHP and configuring web servers

## Step by Step Implementation:

### Step - 1 : Update the Package manager and install Apache2 webserver

The following step by step guide is used to implement the project

Update package manager

```
sudo apt update
```

Install apache2 webserver

```
sudo apt install apache2
```
![alt_text](Images/Apache.png)

### Step - 2 : PHP Installation

Install php

```
sudo apt install php
```

![alt_text](Images/php%20install.png)

### Step - 3 : Nmap Installation 

_Nmap, short for "Network Mapper," is an open-source network scanning tool used for discovering hosts and services on a computer network. It is widely used by network administrators, security professionals, and penetration testers to assess network security, identify vulnerabilities, and gather information about network devices._

Install nmap

```
sudo apt install nmap
```

### Step - 4 : Configure Ownership and Permission 

It's important to manage permissions and ownership properly to ensure security. Adjusting permissions as described below is a basic setup for demonstration purposes; in real settings, follow security best practices.

Change Ownership of the '/var/www/html' directory to the user 'ubuntu'

```
sudo chown ubuntu /var/www/html
```

Set permissions on the /var/www/html directory for demonstration purposes (not recommended for production)

```
sudo chmod 777 /var/www/html
```
![alt_text](Images/Screenshot%202024-03-09%20at%2020.50.17.png)


### Step - 5 : Create a Cronjob that schedules the execution of the nmap command every 10 minutes

Edit the crontab file
```
sudo crontab -e
```

Add the following line to the crontab file:

```
*/10 * * * * nmap <private Ip Address> -oN /var/www/html/nmap.html
```
![alt_text](Images/cron%20tab.png)

Note: Running nmap frequently on your network may generate a significant amount of network traffic and could potentially be disruptive.

### Step-6 : Create a PHP script to display the generated content from nmap.html

- Create 'network.php' file in '/var/www/html' directory

```
touch /var/www/html/network.php
```

- Populate the file with the following PHP script:

```
<?php

echo "Server Timestamp: ";
echo date("h:i:sa");

echo "<pre>";
include("nmap.html");
echo "</pre>";

?>
```
![alt_text](Images/php%20script.png)

Ensure that the nmap.html file exists in the same directory as this PHP script or provide the correct path if located elsewhere. Also, ensure that the web server has permission to read the nmap.html file and that PHP is properly configured on your server.

### Step-7 : View the output from your browser 

- Access <public_ip_address>/network.php to view the generated output. 

Note that it might take up to 90 seconds for nmap to populate the result after the command has been executed.


![alt text](Images/nmap%20working.png)
