# ansible

Inventory and playbooks for the installation and configuration of servers using [Ansible](https://docs.ansible.com/)

## Repository

Clone the repository into the local folder from here:
https://gitlab.infoware.de/server/ansible.git

*Prerequisite: The "ansible" package must be installed*
```bash
sudo apt install ansible
```

## Usage on Linux

For installation, see Tutorial

Access to the servers should be done via SSH keys. The public key should be stored at Hetzner and used directly when setting up cloud servers. On the control node, the corresponding private key must be located at `~/.ssh/id_rsa` or passed with the `--key-file` parameter when calling.

## Semaphore

API setup:

### Get Cookie
```bash
curl -v -c /tmp/semaphore-cookie -XPOST -H 'Content-Type: application/json' -H 'Accept: application/json' -d '{"auth": "admin", "password": "2lAw6DKg90luHgQVEpNa"}' http://localhost:3001/api/auth/login
```

### Query Token
```bash
curl -v -b /tmp/semaphore-cookie -H 'Content-Type: application/json' -H 'Accept: application/json' http://localhost:3001/api/user/tokens
```
mxxh5txmgpe3geaxiwym1rsl63aafpdu8qp54iwlbem=

### Use Token
```bash
curl -v -XPOST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: Bearer mxxh5txmgpe3geaxiwym1rsl63aafpdu8qp54iwlbem=' -d '{"template_id": 1}'
```
### http://localhost:3001/api/project/1/tasks

## Usage on Windows
Ansible can be used under Windows with the Windows Subsystem for Linux (WSL). After setting up a distribution (Ubuntu 22.04 LTS was tested), the installation is carried out as described in the tutorial above (see also the points under Miscellaneous).

The WSL can access the Windows paths directly: If this repository has been checked out under C:\infoware\git\ansible, it is used via these commands, for example:
`ansible-inventory -i /mnt/c/infoware/git/ansible/inventory/hosts.yml --list -y`
`ansible-playbook -i /mnt/c/infoware/git/ansible/inventory/hosts.yml /mnt/c/infoware/git/ansible/playbooks/haproxy.yml -l load_balancers`

### Preparing the Windows computer
The minimum requirement is that you have [[OpenSSH]] installed.

If this is not the case, you can upgrade the package with the following steps:
```
- install choco: (instructions from https://chocolatey.org/install#individual)
      - powershell.exe as administrator
         Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
    - install openssh: (instructions from https://docs.ansible.com/ansible/latest/os_guide/windows_setup.html#id1)
       choco install --package-parameters=/SSHServerFeature openssh
```
	

## Hetzner Server (windows)
You can recreate a Windows server as follows:
- Via the Hetzner console, create a new computer based on a snapshot. (e.g. Win10-BasisImage3 and CX31 Server)
- Rename the computer and enter the name and IP in hosts.yml
  The ansible password can be chosen freely.
  Example:
    - `ih-detour-test:`
              `ansible_host:: 49.13.58.82`
			  `ansible_password: ZA6oDtBt3opzayZqgu`
              `dbpass: 1x0AG39KBZXFYbhYrgbl0dR1N`

Then, execute the installation with 
- `ansible-playbook -i inventory/hosts.yml playbooks/install_windows.yml -l ih-detour-test`

The following call is then used to perform a complete installation of a 
Detour server with the following call:

- `ansible-playbook -i inventory/hosts.yml playbooks/windows_olrserver.yml -l ih-detour-test`

- PostgreSQL 15 on port 5432 (the password “dbpass” is required for this, see above)
- NaviServer on port 6600
- OLR-Server on port 5500
- Routing server on port 5007

## Playbooks
In order to be able to access the computer via ssh, you have to “identify” yourself with
with the keyfile id_rsa_ansible

For ssh this can be done with:
ssh -i id_rsa_ansible root@<IP-ADRESS>

For ansible, for example, it works like this:
ansible-playbook --private-key id_rsa_ansible playbooks/ubuntu.yml -l ih-maptrip-manager-02

### ubuntu.yml

Basic installation and configuration for servers based on Ubuntu, e.g. servers for Load Balancer, MapTrip Manager or the editors. This includes

- Creating and configuring users
- Authentication exclusively via SSH key
- Set host name and time zone
- Installation of various packages (“basic equipment”)
- Installing and configuring SNMP for monitoring
- Installing and configuring the Shorewall firewall

*Shorewall only allows SSH access to the server from the infoware network. If the installation and configuration should also be possible from the home office, access must be via the VPN. To do this, it is entered in WireGuard under AllowedIPs.

Installation on all servers in the load_balancers group with the **install** tag:

`ansible-playbook -i inventory/hosts.yml playbooks/ubuntu.yml -l load_balancers --tags “install”`

Install the update on a server and, if necessary, restart the server with the **update** tag:

`ansible-playbook -i inventory/hosts.yml playbooks/ubuntu.yml -l ih-lb-03 --tags “update”`


Transfer private keys (iwServer) to Linux server (id_rsa and id_rsa.pub):
ansible-playbook -i inventory/hosts.yml playbooks/ubuntu.yml -l ih-nextcloud -t keypair

### windows_server.yml
Private Keys (iwServer) auf Windows-Server übertragen (id_rsa und id_rsa.pub):
ansible-playbook -i inventory/hosts.yml playbooks/windows_server.yml -l ih-detour-staging -t keypair

### haproxy.yml
Installs the load balancer haproxy on a number of servers. These are configured for access via floating IPs, then haproxy is installed and configured. The configuration of the shorewall firewall is also adjusted.

*Prerequisite: Installation of the servers via ubuntu.yml*

Installation (configuration of floating IPs, installation and configuration of haproxy and shorewall) only on a load balancer with the tag **install**:

`ansible-playbook -i inventory/hosts.yml playbooks/haproxy.yml -l ih-lb-03 --tags “install”`

The same installation on all load balancers:

`ansible-playbook -i inventory/hosts.yml playbooks/haproxy.yml -l load_balancers --tags “install”`

Update the configuration and certificates for haproxy on all load balancers with the tag **haproxy**:

`ansible-playbook -i inventory/hosts.yml playbooks/haproxy.yml -l load_balancers --tags “haproxy”`

Update the configuration of the shorewall on all load balancers with the tag **shorewall**:

`ansible-playbook -i inventory/hosts.yml playbooks/haproxy.yml -l load_balancers --tags “shorewall”`

### editors.yml
Sets up servers for the operation of the editors (Detour, FollowMe, MapTrip Remote). These are operated in different branches (prod, staging, each with and without MapTrip Manager, ...) on the servers ih-editors-01 and 02, each in a Docker container with nginx.

*Precondition: Installation of the servers via ubuntu.yml*

Installation on one server:

`ansible-playbook -i inventory/hosts.yml playbooks/editors.yml -l ih-editors-01`

Installation on all editor servers:

`ansible-playbook -i inventory/hosts.yml playbooks/editors.yml -l editors`

### sonarqube.yml
Installs Sonarqube, a static code analysis tool, on a server. The playbook sets some environment variables for the operation of Sonarqube, installs Docker, sets up Sonarqube and the required database via Docker and configures the firewall for access to Sonarqube.

*Prerequisite: Installation of the server via ubuntu.yml*

`ansible-playbook -i inventory/hosts.yml playbooks/sonarqube.yml -l ih-sonar`

### windows_server.yml
Sets up a Windows server.

`ansible-playbook -i inventory/hosts.yml playbooks/windows_server.yml -l ih-navi02`.

Transfer public keys to Windows server (authorized keys):
ansible-playbook -i inventory/hosts.yml playbooks/windows_server.yml -l ih-traffic-01 -t pubkeys

### control_node.yml
Sets up a control node for ansible. Currently mainly for the
distribution of map data
ansible-playbook --private-key id_rsa_ansible playbooks/control_node.yml -l ih-control

### windows_olrserver.yml
Used to install and deploy a fully equipped Detour server.
Includes:
* RoutingServer
* NaviServer
* OLRServer

*Prerequisite: Installation of the server via windows_server.yml*


Installation on a server:
`ansible-playbook -i inventory/hosts.yml playbooks/windows_olrserver.yml -l ih-detour-staging`


Deployment only - update the server executables:
`ansible-playbook -i inventory/hosts.yml playbooks/windows_olrserver.yml -l ih-detour-staging -t deploy_exe`


Deployment only - update the server executables:
`ansible-playbook -i inventory/hosts.yml playbooks/windows_olrserver.yml -l ih-detour-staging -t deploy_exe`

ansible-playbook -i inventory/hosts.yml playbooks/windows_olrserver.yml -l
ih-routing01 -t deploy_exe

ansible-playbook -i inventory/hosts.yml playbooks/windows_olrserver.yml -l
ih-navi02 -t deploy_exe

### windows_firewall_mar.yml

Configures the firewall of the map and route servers appropriately. All ports are opened for access from the other servers, SSH and RDP are only permitted by infoware and monitoring via PRTG is permitted.

This call adjusts the rules for all Windows servers in the `mar.yml` inventory:

`ansible-playbook -i inventory/mar.yml playbooks/windows_firewall_mar.yml -l windows_servers`

SSH must first be activated on the servers and the fingerprint saved (via `ssh user@<ip>`, a login is not required).

### Roles
The following roles are also included, which can be used in playbooks:

- docker
- postgres
- tomcat

Function and use are described in the respective directory in README.md.

## Etc
### Put Host on known_hosts
If you have locked yourself out with a faulty firewall configuration or similar or want to test an installation
completely, the easiest way is to reset the server using the *Rebuild* function of the Hetzner Cloud Console
function.

Ansible then cancels the installation (“WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!”), as the server's
entry of the server in the list of known hosts has changed. The old server can be deleted as follows
as follows:

`ssh-keygen -f ~/.ssh/known_hosts -R 91.107.192.235`

### Private keys under WSL
SSH only accepts a private key if the access rights have been restricted to the user:

`chmod 0600 ~/.ssh/id_rsa`

However, setting the rights only works if the file is located in the Linux file system. For a path
such as `/mnt/c/id_rsa` in the Windows file system, setting with chmod does not work!

### "Ansible is being run in a world writable directory" unter WSL
If the Ansible directory is located in the Windows file system, you will receive the error message *Ansible is being run in a world writable directory* when using an ansible.cfg in this
directory, you will receive the error message *Ansible is being run in a world writable directory*. In order to adjust the authorization for
this directory, as described in [this comment](https://github.com/trailofbits/algo/issues/1637#issuecomment-1329187046)
the Windows file system with metadata must be used:

```
sudo umount /mnt/c
sudo mount -t drvfs C: /mnt/c -o metadata
```

This only works if you are not in /mnt/c. Now switch to the Ansible directory and adjust the authorization:

`sudo chmod o-w .``