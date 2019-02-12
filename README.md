# Linux_Server_Configuration
An Udacity Full Stack Web Developer II Nanodegree Project.

## Breif Intro About The Project:
This  will guide you through the steps to make  a installation of a Linux server and prepare it to host your Web applications. You will be then able to secure your server from a number of attack vectors, install and configure a database server, and deploy one of your existing Flask-based Web applications onto it.

*Finally the project is to  Configuring a Linux server to host a web app securely.*

In this project, I have set up an Ubuntu 18.04 image on a DigitalOcean droplet. The technical details of the server as well as the steps that have been taken to set it up can be found in the succeeding sections.

## Technical Information About the Project

1. **Server IP Address:** 54.159.20.61
2. **SSH server access port:** 2200
3. **SSH login username:** grader
4. **Application URL:** http://54.159.20.61.xip.io
5. **The Private_Key is:** [Click here](https://github.com/saichandadabala/Linux_Server_Configuration/blob/master/private_key).

## Procedural steps forEstablishing a connection with Amazon EC2:

- open your AWS Educate and login to your account.

- After logging in, go to your lab which is activated for you and Click on start lab.
   - Now your lab is running, and it should run till the end of your deployment process.
   
- Click on Open Console and then go to All Services and `Select EC2`.

- Now Change the server to  **_N.Virginia_** for creating an instance.

- Now click on `Launch Instance` and select your preferred instance.
   - In this project, the instance used is `**Ubuntu Server 18.04 LTS.**`
   
- After selecting, Click on Review and Launch and again select Launch.

- Choose `“Create a new Pair”` and edit the key pair name and Download it. The downloaded file is of the format `“.pem”.`

- Now Click on Launch Instance and give it a name. It shows that instance is `running.`

- Click on `**Description**` which is at the end of the page and Copy your Public DNS and Public IP

- Click on `view Launch log` to check whether it is running `successfully`.
  - Now, click on `launch wizard-2` and Click on `Inbound`. In this you must add the rules for incoming connections i.e., add port for SSH (2200), HTTP (80) and NTP (123) and save.
  
## Linux Server _Configuration Steps:
**Step 1:** At first, Create a new folder and place the downloaded `.pem` file in it.

**Step 2:** Open it using Git Bash by the following command:

    ssh -i  filename(linux_server_config.pem) ubuntu@IP address
    
**Step 3:**  You need to `update the packages now`.
```
  sudo apt-get update
  sudo apt-get upgrade
  ```
**Step 4:** After `updating` the packages, open the file using the following command:

  ```sudo vi /etc/ssh/sshd_config```
 
 Do some modifications by Changing the port number from ``22`` to ``2200`` and **save it `(Esc and :wq)`** in the file.
 
 **Step 5:** Restart the service using :
   ```
   sudo service ssh restart
   ```
   
**Step6:** Open the file with `ssh port 2200`. It is to check whether the `port 2200` is working or not.
    
    ssh -i linux_server_config.pem -p 2200 ubuntu@IP address
    
**Step 7:** Now add the following commands to configure the Firewall (UFW):
```
 sudo ufw default deny incoming
 sudo ufw default allow outgoing
 sudo ufw default allow 2200/TCP
 sudo ufw default allow www
 sudo ufw default allow 123/NTP
 sudo ufw default deny 22
 
 sudo ufw default enable
 
 ```
 After Proceed with the Option `(Y/N) - Y`

**To check status:
```
 sudo ufw status
 
 ```
 ```
 To                         Action      From
--                         ------      ----
2200/tcp                   ALLOW       Anywhere                  
80/tcp                     ALLOW       Anywhere                  
123/udp                    ALLOW       Anywhere                  
22                         DENY        Anywhere                  
2200/tcp (v6)              ALLOW       Anywhere (v6)             
80/tcp (v6)                ALLOW       Anywhere (v6)             
123/udp (v6)               ALLOW       Anywhere (v6)             
22 (v6)                    DENY        Anywhere (v6)

```
_After Completing the above steps,  You need to create a User By following the below steps:


