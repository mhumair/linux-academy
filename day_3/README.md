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

* -m : The -m tag specifies the creation of a home directory if it dosen't exist.
* -d : Specifies the login directory by appending the Base directory with the user's name 
* -s : Can be used to change the default login shell.

![users created](https://i.ibb.co/gVYq3TB/1.png)
![check users](https://i.ibb.co/R93nVpv/check-users.png)

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
![group created](https://i.ibb.co/9r8jXJg/create-Grou.png)
![change group ownership](https://i.ibb.co/Yyrw7kh/2.png)
![change accessibility](https://i.ibb.co/8mcBzpc/acl.png)



### /bin/false vs /usr/bin/false

The main diffrence that i found was that `bin/false` is just a binary that dosen't return anything & restricts login while `/nologin` exits gracefully with a message.

### Changing The Shell 

Since I had already used to the `-s` flag while creating the user. I edited the etc/passwd file directly.

![no login shells](https://i.ibb.co/Nx6MgKr/nolgin.png)

### Restricting Sudo Access
Edited the sudoers file 
```console
alice ALL=(root) /sbin/reboot
```
### Deleting a User

```console
humair@ems:~$ deluser alice
```

### Generating public/private keys using gpg.

```console
humair@ems:~$ gpg --full-gen-key
```
![generate key gpg](https://i.ibb.co/84hQ4Wr/gpg-key-gen.png)

### Encrypting files using gpg
```console
humair@ems:~$ gpg -c ./mangpg
```
![generate key gpg](https://i.ibb.co/84hQ4Wr/gpg-key-gen.png)
### Generating public/private ssh key pairs.
```console
humair@ems:~$ gpg -c ./mangpg
```
### Configuring SSH Server For Remote Access.
```console
humair@ems:~$ ssh localhost
```

The command for connecting to the remote & this server was also fairly the same. However do we need to portforward in order for it to work on different network machines?

![localhost ssh](https://i.ibb.co/L1TVxnS/localhost-ssh.png)

### Configuring telnet for Remote Access.

```console
humair@ems:~$ telnet
```
![localhost telnet](https://i.ibb.co/9GzWvVz/telnet.png)
