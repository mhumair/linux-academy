# Managing Users & Remote Desktops Connections

## Topics :
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

  

## Creating Users 

```console
humair@ems:~$ sudo useradd -m -d /opt/joe joe
```

```console
humair@ems:~$ sudo useradd -m -d /opt/alice -s /bin/sh joe
```

-m : The -m tag specifies the creation of a home directory if it dosen't exist.
-d : Specifies the login directory by appending the Base directory with the user's name 
-s : Can be used to change the default login shell.

![users created](https://i.ibb.co/qCrb5Pk/Screenshot-from-2020-02-12-05-20-44.png)
![check users](https://i.ibb.co/qCrb5Pk/Screenshot-from-2020-02-12-05-20-44.png)

## Managing Users in Groups

### Creating a Secondary Group
```console
humair@ems:~$ sudo groupadd friends; sudo gpasswd -M alice, jhon friends
```
-M : Specifes that a list of users are to be added to the group.

### Creating a File

```console
humair@ems:~$ touch some_file
```
### Changing Group OwnerShip
```console
humair@ems:~$ chgrp some_file friends
```
### Changing Accessiblity 
```console
humair@ems:~$ setfacl -m u:alice:r-- ./some_file
```
For some reason the bits were'nt working here.
### /bin/false vs /usr/bin/false

The main diffrence that i found was that `bin/false` is just a binary that dosen't return anything & restricts login while `/nologin` exits gracefully with a message.

### Changing The Shell 

Since I had already used to the `-s` flag while creating the user. I edited the etc/passwd file directly.


### Restricting Sudo Access
Edited the sudoers file 
```console
alice ALL=(root) /sbin/reboot
```
### Deleting a User

```console
humair@ems:~$ deluser alice
```

![group created](https://i.ibb.co/qCrb5Pk/Screenshot-from-2020-02-12-05-20-44.png)
![change group ownership](https://i.ibb.co/qCrb5Pk/Screenshot-from-2020-02-12-05-20-44.png)

### Generating public/private keys using gpg.

```console
humair@ems:~$ gpg --full-gen-key
```
### Encrypting files using gpg
```console
humair@ems:~$ gpg -c ./mangpg
```
### Generating public/private ssh key pairs.
```console
humair@ems:~$ gpg -c ./mangpg
```
### Configuring SSH Server For Remote Access.
```console
humair@ems:~$ ssh localhost
```
The command for connecting to the remote & this server was also fairly the same. However do we need to portforward in order for it to work on different network machines?
### Configuring telnet for Remote Access.

```console
humair@ems:~$ telnet
```

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
