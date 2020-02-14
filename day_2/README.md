# Managing Users & Remote Desktops Connections

## Topics :
* Overview of Groups & File Permissions
* Creating Users
* Managing Users in Groups
* Restricting File Access
* /bin/false vs /usr/bin/false
* Restricting sudo access
* Deleting a User
* Exploring GnuPg
* Generating public/private ssh key pairs.
* Configuring SSH Server For Remote Access.
* Configuring telnet for Remote Access.

  

## Overview of Groups & File Permissions 

```console
humair@ems:~$ sudo useradd -m -d /opt/alice -s /bin/sh joe
```
-m : The -m tag specifies the creation of a home directory if it dosen't exist.
-d : Specifies the login directory by appending the Base directory with the user's name 
-s : Can be used to change the default login shell.


![Compute Options](https://docs.microsoft.com/en-us/learn/modules/principles-cloud-computing/media/2-vm-vs-container-vs-serverless.png)

## Cloud Vs Shared Hosting
![Cloud vs Shared Hosting](https://www.hostingadvice.com/wp-content/uploads/2017/11/server-comparison.jpg)

Factors  | Cloud Hosting | Managed Hosting
-------- | --------------| ----------------|
Server Resources, Configuration, and Management|Shared | Dedicated
Scalability | Easily Scale Up or Down | Scaling Requires more time
Performance | Customized Configurations Leads To Better Performance | Slows down once server is maxed out.
Security | Managed Partially By Provider | Managed By Client At the Application level
Cost | Starts from $15 to $20 | Starts from only a few Dolllars

## Cloudways Managed Services
A Managed Cloud Hosting Platform Where Teams Can Build, Deploy, Scale & Manage Small to Medium Sized Web Applications. 
Out of the box it provides Application as well as Server-side configuration stacks :

| Cloud Providers |
--- | --- | --- | --- | --- |
 Managed Amazon Cloud | Managed Google Cloud | Managed DigitalOcean | Managed Linode | Managed Vultr |

| Applications |
--- | --- | --- | --- | --- |
WordPress Hosting | WooCommerce Hosting | Enterprise WordPress Hosting | Magento Hosting | PHP Hosting
Laravel Hosting | Drupal Hosting | Joomla Hosting | PrestaShop Hosting | Ecommerce Hosting

### SSH

Secure Shell is a cryptographic network protocol for operating network services securely over an unsecured network. Typical applications include remote command-line, login, and remote command execution, but any network service can be secured with SSH. 
You can login to any shell using ssh on linux in the following way :

```console
humair@ems:~$ sudo ssh yourusername@yourip
```
![ssh](https://i.ibb.co/qCrb5Pk/Screenshot-from-2020-02-12-05-20-44.png)
### DDOS
In computing, a denial-of-service attack is a cyber-attack in which the penetrator seeks to make a machine or network resource unavailable to its intended users by temporarily or indefinitely disrupting services of a host connected to the Internet.
Six steps to prevent DDoS attacks :
* Buy more bandwidth. ...
* Build redundancy into your infrastructure. ...
* Configure your network hardware against DDoS attacks. ...
* Deploy anti-DDoS hardware and software modules. ...
* Deploy a DDoS protection appliance. ...
* Protect your DNS servers.
#### Resources :
* https://docs.microsoft.com/en-us/learn/modules/principles-cloud-computing/2-what-is-cloud-computing
* https://www.hostingadvice.com/how-to/cloud-hosting-vs-shared-hosting/
* http://cloudways.com/
