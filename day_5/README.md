# Linux Networking Fundamentals

## Topics :

* Tranferring files : rsync | scp | ftp | sftp
* Using tcp_wrappers
* Download/Upload FTP VS SFTP : 
* Tmux : 
* Strace : 
* Apt-Get Repositories : 

  

## Tranferring Files : 

### Rsync
The `netstat` utility can be used with `-i` flag to display all the network interfaces as follows : 
```console
humair@ems:~$  netstat -i
```
* -i : Displays all the interfaces in a table format.

`ss : `
```console
humair@ems:~$  ss -ltnp
```
where the `ltnp` flag shows all the info except foreign address as compare to `netstat`.

### With Ip & Name
```console
humair@ems:~$  netstat -r |gawk '{print $1 " | " $8}' | column -t'
``````
* -r : Display routing tables.
* gawk : Awk is mostly used for pattern scanning and processing.
* column : Process output into tables.

## Processes

### `ps augx` vs `ps ef -f`
* ps augx : prints all the processes using the BSD format.
* ps -ef -f : prints all the processes using the POSIX standard.

### Process Id's;

Since I had multiple tabs & windows open, there were several process id's for chrome because each tab exists as a seperate process. Parent id for chrome : 2815

```console
humair@ems:~$ pstree -p -T | grep chrome
```
For slack the parent id was : 7167
```console
humair@ems:~$ pstree -p -T | grep slack
```
* -p : prints the process ids along with the tree
* -T : hides threads.

### Using Signals to Kill/Suspend

* `Ctrl + C` is used to kill a process with signal SIGINT , in other words it is a polite kill . 
* `Ctrl + Z` is used to suspend a process by sending it the signal SIGTSTP , which is like a sleep signal, that can be undone and the process can be resumed again.

### Zombie process

Whenever a process(parent) forks itself to create another process(child) : 
* it has to wait for the child to finish inorder to clear up resources like the child's pid upon exit. 

* If the parent exits first the child is left an orphan & no one to clear up it's resources upon exit. 

* This results the child process to become a zombie processe. Zombie processes are those processes who have exited but their temporary resources such as theire pid's have'nt been cleaned up by the OS.

* This results in them being shown in the process table with a defunct tag.

### Killing a zombie process
 Get zombie 
 ```console
humair@ems:~$ ps aux | grep defunct | awk '{print $2}'
```
Kill a zombie 
 ```console
humair@ems:~$ kill -9 <pid>
```
### fg | bg Signals

* `SIGCONT`: Backgrounding a process is accomplished by sending SIGCONT but not waiting for it to finish. In this case, both the shell and the child process can interact with stdout/stderr,

* `SIGTSTP`: Suspending a command (CTRL-Z) works by sending a SIGTSTP to the child process. The shell is then free to interact with the user via stdin/stdout.

### Configuring SSH : 
#### To listen on loopback-interface only : 

Check which interface & port is sshd listening on : 
 ```console
humair@ems:~$ sudo netstat -ltnp | grep sshd
```
then edit the sudo vi /etc/ssh/sshd_config file 
And change`#ListenAddress 0.0.0.0` to `#ListenAddress 127.0.0.1`

To change port, in the same file change `#Port 22` to desired port.

Then restart the service : 
 ```console
humair@ems:~$ sudo service sshd restart
```
### Creating Processes Using Fork

A call to fork does the following things :

* creates a new process by duplicating the process that calls it. 
* the child process & the parent have the same address space untill the child manipulates the address space.
* it is then upto the scheduling policy to schedule the child or parent.
* a parent is responsible to clear resources of a child on exit.
* the first processes that starts is `init`, it is also the father of all processes.
* `init` is responsible for adopting all processes whose parent process has exited process.

### TCP | UDP Services/Applications

### Three Way HandShake

To establish a connection, TCP uses a three-way handshake : 

* `SYN` : Is short for synchronize & is sent by the client to start after the server has passively opened a port for connections.
* `SYN-ACK` : In response the server replies with an acknowledgement.
* `ACK` : Finally, the client also sends an acknowledgement back to the server.

## Transferring Encrypted/Signed Files

### Generating key
 
 ```console
humair@ems:~$ gpg --full-generate-key
```

### Exporting key
 
 ```console
humair@ems:~$ gpg --list-secret-keys --keyid-format LONG
```

 ```console
humair@ems:~$ gpg --armor --export <id>
```
### Encrypting file
 
 ```console
humair@ems:~$ gpg -e -r <public_key> <file>
```

### Decrypting file
 
 ```console
humair@ems:~$ gpg <file>
```
### Signing a file
 
 ```console
humair@ems:~$ gpg --sign <file>
```
### Verifying a signed a file
 
 ```console
humair@ems:~$ gpg --verify <file
```
Output if signing is altered :
```
gpg: [don't know]: invalid packet (ctb=5c)
gpg: no signature found
gpg: the signature could not be verified.
Please remember that the signature file (.sig or .asc)
```


