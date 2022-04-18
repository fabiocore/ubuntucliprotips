# Ubuntu Server CLI pro tips

---
---

# BASIC

### Networking

Get the IP address of all interfaces `networkctl status`

Display all IP addresses of the host `hostname -I`

Enable/disable interface

```
ip link set <interface>  up

ip link set <interface> down
```

Manage firewall rules:

```
enable firewall: sudo ufw enable

list rules: sudo ufw status

allow port: sudo ufw allow <port>

deny port: sudo ufw deny <port>
```

Connect remotely through SSH `ssh <user>@<host IP>`

### Security

Show which users are logged in

`w`

Get password expiration data for <user>

`chage -l <user>`

Set password expiration date for <user>

`sudo chage <user>`

Lock a user account

`sudo passwd -l <user>`

Unlock a user account

`sudo passwd -u <user>`

List open ports and associated processes

`sudo netstat -tulpn`

Automatically detect and ban abusive IP addresses

`sudo apt install fail2ban`

Show banned IP addresses

`sudo fail2ban-client status`

`sudo fail2ban-client status <jail>`

Get the support status for installed packages

`ubuntu-support-status`

Enable kernel live patching

`sudo snap install canonical-livepatch`

`sudo canonical-livepatch enable <token>`

Visit [ubuntu.com/livepatch](ubuntu.com/livepatch) to get a free token for up to 3 machines.

### Packages

Search for packages

`apt search <string>`

`snap find <string>`

List available updates

`apt list --upgradable`

Apply all available updates

`sudo apt update && sudo apt upgrade`

Install from the Ubuntu archive

`sudo apt install <package>`

Install from the snap store

`sudo snap install <package>`

Which package provides this file?

`sudo apt install apt-file`

`sudo apt-file update`

`apt-file <filename or command>`

### Files

List files

`ls`

List files with permissions and dates

`ls -al`

Common file operations

`create empty: touch <filename>`

`create with content: echo "<content>" > <filename>`

`append content: echo "<content>" >> <filename>`

`display a text file: cat <file>`

**Tip:** Use [bat](https://github.com/sharkdp/bat) instead of cat to get a pretty view of files like json, yaml, others.

`copy: cp <file> <target filename>`

`move/rename: mv <file> <target directory/filename>`

`delete: rm <file>`

Create a directory

`mkdir <directory>`

Create directories recursively

`mkdir -p <directory1>/<directory2>`

Delete a directory recursively

`rm -r <directory>`

Quick file search

`locate <q>`

Search string in file

`grep <string> <filename>`

Search string recursively in directory

`grep -Iris <string> <directory>`


# ADVANCED

### Files

Find files modified in the last n minutes

`find <directory> -mmin -<n> -type f`

eg. find . -mmin -5 -type f

Show only the nth column

`col<n> "<separator>" <filename>`

eg. col2 "," foo.csv

Display file paginated

`less <filename>`

Display first n lines

`head -n <n> <filename>`

Display last n lines

`tail -n <n> <filename>`

Follow file content as it increases

`tail -f <filename>`

Pack a directory into an archive

`zip: zip -r <target> <source dir>`

`tar.gz: tar cvzf <target>.tar.gz <source dir>`

Unpack an archive

`zip: unzip <zip file>`

`tar.gz: tar xvf <tar.gz file>`

Copy file to remote Server

`scp <filename> <user@server>:<destination>`

eg. scp config.yaml admin@192.0.0.0:/config

Copy directory recursively from remote Server

`scp -r <user@server>:<source> <destination>`

eg. scp -r admin@192.0.0.0:/config /tmp


### System

Display kernel version

`uname -r`

Get disk usage

`df -h`

Get memory usage

`cat /proc/meminfo`

Get system time

`timedatectl status`

Set system timezone

`timedatectl list-timezones`

`sudo timedatectl set-timezone <zone>`

Get all running services

`systemctl --state running`

Start or stop a services

`service <service> start/stop`

Monitor new logs for a services

`journalctl -u <service> --since now -f`

Get the list of recent logins

`last`

Display running processes

`htop`

Kill process by id

`kill <process id>`

Kill process by uname

`kill <process name>`

Run command in the background

`<command> &`

Display background commands

`jobs`

Bring command <n> to the foreground

`fg <n>`

### Kubernetes and containers

Install MicroK8S and list available add-ons

`sudo snap install microk8s --classic`

`microk8s.status --wait-ready`

Enable a MicroK8S add-on

`microk8s.enable <service>`

Enable MicroK8S nodes and running services

`microk8s.kubectl get nodes`

`microk8s.kubectl get services`

[MicroK8S documentation](https://microk8s.io/docs)

Launch a LXD container

`lxd init`

`lxc launch ubuntu:18.04 <container name>`

Or another distro

`lxc launch images:centos/8/amd64 <container name>`

Get a shell inside a LXD container

`lxc exec <name> -- /bin/bash`

Push a file to a LXD container

`lxc file push <filename>`

`<container name>/<path>`

Pull a file from a LXD container

`lxc file pull <destination>`

`<container name>/<file path>`

[LXD documentation](https://linuxcontainers.org/lxd/docs/master/)


### Virtualisation

Install Multipass and launch an Ubuntu VM

`sudo snap install multipass --classic multipass launch <image> --name <VM name>`

Omitting <image> will launch a VM with the latest Ubuntu LTS.

List existing VMs

`multipass list`

Get a shell inside a VM

`multipass shell <VM name>`

[Multipass home and docs](https://multipass.run/)

### OpenStack

Install OpenStack and launch an instance

`sudo snap install microstack --classic`

`sudo microstack.init`

`microstack.launch`

The Horizon dashbaord is available at 10.20.20.1
Default credentials: admin / keystone

[Microstack docs](https://microstack.run/docs)

---

This document was copied from [Ubuntu Server CLI pro tips](https://assets.ubuntu.com/v1/f401c3f4-Ubuntu_Server_CLI_pro_tips_2020-04.pdf?_ga=2.108098050.1677985905.1650293425-402451695.1650293425) in PDF.
