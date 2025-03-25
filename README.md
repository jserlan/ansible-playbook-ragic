# ansible-playbook-ragic

## Description

This project contains a playbook to help you to deploy a Ragic installation on your own servers. It will install all the dependencies and run Ragic as a service in Systemd.

### Requirements :

To use this project, you need :
- A server running on Linux (for now, only on Ubuntu-like)
- An access to the root user or at least a user with administrative privileges with `sudo`.
- A SSH server installed to access on the remote machine.

### Files and folders description :

This project contains the following files and folders :
- deploy-ragic.yml : list of roles to deploy and the common variables. For instance, here you can edit you timezone or remove a role from deployment.
- ansible.cfg : that contains my custom parameters for ansible.
- roles/ : that contains the roles used by the playbook deploy-ragic.yml
- hosts/ : that contains the hosts file used by the playbook. Here you can define the IP addresses that you wan to deploy.
- vars/ : that contains the projects variables used by the playbook. Here are the Ragic archive files.

## Usage

### Clone the repository :

    git clone https://github.com/jserlan/ansible-playbook-ragic.git

### Run the playbook :

    ansible-playbook -k -b -K -u <Your Username> -i hosts/default deploy-ragic.yml

You will need to define a new entry for ragic in your hosts file (or edit the file hosts/default to update the IP or the hostname to fit with your server).

Playbook arguments :

    -k (or --ask-pass) : used if you didn't store your ssh key on the remote machine (optional)

    -b (or --become) : used if your user need sudo to be granted privileges (optional)

    -K (or --ask-become-pass) : used if your user need to set the password for each sudo command (optional)

    -i (or --inventory) : set the host file that contains the seedbox group with the IP address(es) to deploy (mandatory)

    -u (or --user) : set the remote user (mandatory)

## Configuration

At the end of the deployement using the playbook, the service will be available on the URL `http://<Your IP address>:80/` and you will be able to proceed you custom configurations.

If you want to deploy you license file using this playbook, you can replace the license.xml and sig files by your own files under the folder roles/ragic/files.

## To do

To improve thive project, the following tasks is on the todo list :
- [ ] Provide the SSL configuration with certbot and nginx (or apache)
- [ ] Add the UFW and fail2ban roles
- [ ] Use a different user that the root user to run ragic

And more...
