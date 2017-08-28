# Introduction
This set of Ansible playbooks can be used to automatically configure Debian servers (currently based on 'stretch').

# Playbooks
A main playbook called "**main.yml**" will all the other playbooks in the list below.


- "**VPS.yml**" will:

  - Install 'sudo'
  - Create custom username and import its SSH key
  - Modify the '$PATH' variable to include custom folder


- "**basic_setup.yml**" will:
  - Lock out the *root* account
  - Copy a custom *sources.list*
  - Update the *APT* cache and upgrade all packages (safe)
  - Enable and configure unattented-upgrades (security updates will be installed automatically). This setup provides email notification.
  - Setup the proper timezone
  - Install several essential packages
  - Configure *NTP* to sync time
  - Copy custom scripts and executables to the system
  - Configure *logrotate* to take care of log files in */var/log/cron*
  - Create and configure local backups (full system and separate MySQL databases)
  - Restrict SSH authentication with key
  - Install and configure local firewall (**both incoming and outgoing connections are filtered**)
  - Install *Postfix* and imports custom configuration (through a relay)
  - Install *OSSEC* in local mode and enable mail notifications and all active responses


- "**webserver.yml**" will:

  - Install and configure *MariaDB* server
  - Install *Nginx* (default Website is not enabled)
  - Install *OpenSSL* and *Let's Encrypt* (=*certbot*)
  - Modify the user's skeleton to be ready for Web hosting
  - Install *PHPMyAdmin* and creates a VHost in Nginx


- "**nextcloud.yml**" will:

  - Install *NextCloud* requirements and *Redis server*
  - Create a dedicated user for *NextCloud*
  - Download and install the latest version of *NextCloud* (if it does not exist already)
  - Create a hardended VHost for Nginx and enable it (certificates created with *Let's Encrypt*. If not possible, fallback to default SSL certificates)


# Installation
In order to use Ansible, it is necessary to install Python on the target servers.
Install Python with the following command:

``` $ apt-get install python ```

It is also necessary to access the server via SSH. By default, the *VPS* playbook is configured to use the "root" account for this purpose. Feel free to modify this if the account is different.

Finally, it is recommended to configure in advance your DNS A records for your Websites so Let's Encrypt can create your certificates. Otherwise, non-valid SSL certificates will be used and new ones need to be generated later.


# Usage
In order to use these playbooks, you first need to adjust them with the proper "vars" file (recommended to be encrypted with 'ansible-vault'). When everything is adapted to your needs, use the playbooks with the following command:

``` $ ansible-playbook main.yml --ask-pass ```


This example will launch the *main* playbook and ask you for a SSH password (if required). In this case, the *SUDO* password is read from the variables.

Of course, each playbook can be launched separately and with different options.


# TODO
There are still quite a few enhancements to be done. Here is a list of things required:

  - Make the playbooks compatible with Linux distributions other than Debian family (needs to be adapted for Red Hat family too)
  - Simplify some of the roles to reduce their codes
  - Improve the way SSL certificates are generated with Let's Encrypt (to avoid having fails and ignoring them)
  - (Optional) Divide all these into different GIT repositories?
