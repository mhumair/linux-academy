# Linux Networking Fundamentals

## Topics :
* Network Interfaces
* Processes
* Signals
* Configuring ssh
* TCP vs UDP
* Transferring Encrypted/Signed Files

  

### Network Interfaces 

#### Display List Of Networking Interfaces
The `netstat` utility can be used with `-i` flag to display all the network interfaces as follows : 
```console
humair@ems:~$  netstat -i
```
* -i : Displays all the interfaces in a table format.

### With Ip & Name
```console
humair@ems:~$  netstat -r |gawk '{print $1 " | " $8}' | column -t'
``````
* -r : Display routing tables.
* gawk : Awk is mostly used for pattern scanning and processing.
* column : Process output into tables.

![users created](https://i.ibb.co/gVYq3TB/1.png)
![check users](https://i.ibb.co/R93nVpv/check-users.png)


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
