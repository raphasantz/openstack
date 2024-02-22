Installation of OpenStack
In order to install the DevStack in a system, first, you have to create a Linux VM on your computer (such as using VirtualBox or VMware) or remotely in the cloud (such as using AWS).

The VM must have at least 4GB of memory, and the proper internet connection is also important. Here, we are going to use one version of the debian 12, i.e., 18.04.

Follow the following steps to install the OpenStack in your ubuntu virtual machine :

Step 1: Update debian System

Open the terminal and run the following command to ensure that the system is up to date :
```bash
$ sudo apt update  
$ sudo apt -y upgrade  
$ sudo apt -y dist-upgrade  
$ sudo reboot  
```
Step 2: Create Stack User

It is important that the devstack must run as a regular user (non-root user) with the sudo enabled.

To keep this note in mind, let's create a new user with the name "stack" and assign the sudo permissions or privileges. To create a stack user, run the following command in your terminal:
```Bash
$ sudo useradd -s /bin/bash -d /opt/stack -m stack 
```
Now, to assign the sudo privileges to the stack user, run the following command :

$ echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack  

You can switch to the 'stack' user by running the following command:

$ sudo su - stack  

In Most of the debian systems, git comes by default. But if git is missing on your system, then install it by running the following command:

$ sudo apt install git -y  

Step 4: Download OpenStack

Once you install the git, use the git command to download the DevStack from Github.

$ git clone https://git.openstack.org/openstack-dev/devstack  

Step 5: Create a DevStack Configuration File

First of all, go to the devstack directory by running the following command :

$ cd devstack  

Now, create a local.conf file in which you have to enter the four passwords and the host IP address :

Copy the following line of content in the file :

[[local|localrc]]  
  
# Password for KeyStone, Database, RabbitMQ and Service  
ADMIN_PASSWORD=StrongAdminSecret  
DATABASE_PASSWORD=$ADMIN_PASSWORD  
RABBIT_PASSWORD=$ADMIN_PASSWORD  
SERVICE_PASSWORD=$ADMIN_PASSWORD  
  
# Host IP - To get your Server or VM IP, run the 'ip addr' or 'ifconfig' command  
HOST_IP=xxx.xxx.xxx.xxx

Press the ESC, then wq to save and then exit from the local.conf file.

Here, ADMIN_PASSWORD is the password that we will use to log into the OpenStack login page. The default username for an OpenStack is 'admin'.

And HOST_IP is the IP address of your system. To get your Server or VM IP, run the 'ifconfig' or 'ip addr' command.

Step 6 : Install OpenStack with DevStack

To install and run the openstack, execute the following command :

$ ./stack.sh  

DevStack will install the following components:

Compute Service (Nova)
Image Service- Glance
Identity Service-Keystone,
Block Storage Service - Cinder
OpenStack Dashboard - Horizon
Network Service - Neutron
Placement API - Placement
Object Storage - Swift
The installation will take about 10-20 minutes, mostly depends on your internet speed.

At the very end of the installation, you will get the host's IP address, URL for managing it and the username and password to handle the administrative task.

Step 7: Accessing OpenStack on a browser

Copy the horizon URL given in the installation output and paste it into your browser :

http://<IP Address>/dashboard  
To login to OpenStack with the default username - admin or demo and configured password - secret.

Once you login into the OpenStack, you will be redirected to the Dashboard of OpenStack. This dashboard screen is called the Openstack management web console.
