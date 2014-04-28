# Full Continuous Integration Setup

This is a simple setup which provides functionality for most tasks.
- **Subversion:** software versioning and revision control system
- **Trac**: wiki and issue tracking system
- **Jenkins**: continuous integration services

SVN is setup with two hooks:
- Poll a new building process with Jenkins with latest commit
- Adds a message to a Trac ticket with commit messages starting with "Trac<Ticket Number> ..."


## How to start
This setup is fully tested on **Ubuntu 12.04 LTS Server edition**

### Setup of virtual machine
Prepare two network interfaces:
  * First one is default NAT for internet connection and can be switched of after setup or update process.
  * Second one should be a host-only adapter for communication towards your local internal network and SSH connection. 

### Run setup
Create a folder (for additional files) and download setup script: 
```
wget https://raw.githubusercontent.com/draftchallenge/continuous-integration-setup/master/setup
```
Run via `sudo bash ./setup`.
OpenSSH is installed by default to use server inside a virtual machine in connection with a SSHClient like Putty on your host system.

After setup execution further instructions can be seen at your local server's welcome page, by default http://192.168.56.101/.

## Problems
### Network connection
**Network connection from VM to internet does not work.**
Mostly happens after host computer/laptop is used in another environment and with different (wifi-)internet connection.
enter this code inside the VM, respectively eth0 is your network device for your internet connection. 
Maybe check with `sudo ifconfig` first.
```
sudo ifdown eth0 && sudo ifup eth0
```
### Rerun setup and rollback
**If not sure whether setup was executed already you can execute it again any time.**
Each step of the setup - represented by a single function - should be able to be invoked again without harm to the system. 
Simply comment out steps and at the bottom of the setup script if you want to skip some certain steps. 

A rollback script comes by default with files downloaded by setup script. It makes it possible to completely remove all modifications from the system.

### Problems occured within setup
Usually steps are providing as less as possible of output. In case of error it is providing more information. 
Please be sure execution was correct before hitting enter for next step. 

Common errors:
  * Step 1: "gpg: no valid OpenPGP data found": Jenkins does not provide a pgp public key right now. Maybe server is down, try again later.