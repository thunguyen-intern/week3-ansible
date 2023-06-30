# Setup Ansible for deploying Applications
## Ansible
### The Structure of Roles
We need to setup 3 Applications to host 2 servers Odoo.
``` bash
roles
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
```
### How to run
In this project, I'm using Vagrant VM to setup 5 servers (1 postgres, 2 odoos, 1 nginx). Locate to the directory ansible (/etc/ansible) and run this command:
``` bash
ansible-galaxy -i hosts playbook.yml
```
## NFS
