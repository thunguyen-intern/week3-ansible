# Setup Ansible for deploying Applications
## Ansible
### The Structure of Roles
We need to setup 3 Applications to host 2 servers Odoo.
``` bash
roles
├── nfs
│   ├── README.md
│   ├── defaults
│   │   └── main.yml
│   ├── files
│   ├── handlers
│   │   └── main.yml
│   ├── meta
│   │   └── main.yml
│   ├── tasks
│   │   ├── firewall.yml
│   │   ├── install.yml
│   │   └── main.yml
│   ├── templates
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   └── vars
│       └── main.yml
├── nginx
│   ├── README.md
│   ├── defaults
│   │   └── main.yml
│   ├── files
│   ├── handlers
│   │   └── main.yml
│   ├── meta
│   │   └── main.yml
│   ├── tasks
│   │   ├── main.yml
│   │   └── setup.yml
│   ├── templates
│   │   └── default.conf
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   └── vars
│       └── main.yml
├── odoo15
│   ├── README.md
│   ├── defaults
│   │   └── main.yml
│   ├── files
│   ├── handlers
│   │   └── main.yml
│   ├── meta
│   │   └── main.yml
│   ├── tasks
│   │   ├── create-user.yml
│   │   ├── install.yml
│   │   ├── main.yml
│   │   ├── nfs-setup.yml
│   │   ├── odoo.yml
│   │   └── pyenv.yml
│   ├── templates
│   │   ├── odoo.conf
│   │   └── odoo.service
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   └── vars
│       └── main.yml
└── postgres
    ├── README.md
    ├── defaults
    │   └── main.yml
    ├── files
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── tasks
    │   ├── main.yml
    │   └── postgres.yml
    ├── templates
    ├── tests
    │   ├── inventory
    │   └── test.yml
    └── vars
        └── main.yml

37 directories, 44 files
```
### How to run
In this project, I'm using Vagrant VM to setup 5 servers (1 postgres, 2 odoos, 1 nginx). Locate to the directory ansible (/etc/ansible) and run this command:
``` bash
ansible-galaxy -i hosts playbook.yml
```
## NFS
Sync Odoo data (filestore, sessions) between multiple Odoo servers using NFS.
**How to setup NFS?** There are 2 main jobs: Install and configure NFS server on server and clients.
### Server
Install nfs-kernel-server:
``` bash
apt install nfs-kernel-server
```
Make share NFS directory (/mnt/odoo/):
``` bash
mkdir -p /mnt/odoo
chown -R nobody:nogroup /mnt/odoo/
chmod 777 /mnt/odoo/
```
Grant NFS access (/etc/exports):
``` bash
echo "/mnt/odoo 192.168.56.0/24(rw,sync,no_subtree_check)" >> /etc/exports
exportfs -ra
```
Restart NFS server:
``` bash
systemctl restart nfs-kernel-server
```
_Optional: Grant Firewall access_
``` bash
ufw allow from 192.168.56.0/24 to any port nfs
ufw enable
ufw status
```
### Clients
Install nfs-common:
``` bash
apt install nfs-common
```
Create a mount point on the NFS client system (my NFS ip address is 192.168.56.14):
``` bash
mount 192.168.56.14:/mnt/odoo /opt/odoo/.local/share/odoo
```

I have provisioned it using Ansible (roles/nfs/).
