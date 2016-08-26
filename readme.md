# Datasploit Ansible Playbook

---

This is a simple ansible playbook with vagrant which helps you to quickly setup the working datasploit.

###About Datasploit

A tool to perform various OSINT techniques, aggregate all the raw data, visualise it on a dashboard, and facilitate alerting and monitoring on the data.

- Here is the project details [Datasploit](https://github.com/upgoingstar/datasploit)

- The tool documentation [Datasploit-Docs](http://datasploit.readthedocs.io/en/latest/)

###Prerequisites

- Vagrant
- Ansible


### How to setup this playbook?

- Use the below commands to clone and start the playbook

```
git clone https://github.com/appsecco/datasploit-ansible.git
cd datasploit-ansible
```

#### Playbook Overview

- This playbook is structured in the below format. If you have any `API_KEYS`, please add in the `playbook/roles/common/defaults/main.yml`

```
├── playbook
│   ├── group_vars
│   │   └── all
│   ├── main.yml
│   └── roles
│       ├── common
│       │   ├── defaults
│       │   │   └── main.yml
│       │   ├── handlers
│       │   │   └── main.yml
│       │   ├── tasks
│       │   │   ├── dependencies.yml
│       │   │   ├── main.yml
│       │   │   ├── mongo.yml
│       │   │   └── rabbitmq.yml
│       │   └── templates
│       └── datasploit
│           ├── defaults
│           │   └── main.yml
│           ├── handlers
│           ├── tasks
│           │   └── main.yml
│           └── templates
│               └── config.py.j2
├── readme.md
└── Vagrantfile
```


- Then start the datasploit machine by running `vagrant up`

- Then do `vagrant ssh` and get the `IP` address of the machine.

- For web interface browse to the [http://Vagrant-Machine-IP:8000](http://Vagrant-Machine-IP:8000) to access datasploit

- If you want to use individual modules and code, navigate to the `/opt/datasploit/`

```
python domainOsint.py -d <domain_name>
```

- From next time when you are starting virtual machine start the processes using below commands

```
cd /opt/datasploit/
mongod --fork --logpath datasploitDb/mongodb.log --dbpath datasploitDb
cd /opt/datasploit/core
nohup C_FORCE_ROOT=root celery -A core worker -l info --concurrency 20 & 
nohup python manage.py runserver 0.0.0.0:8000 &
```

- Read more about tool in documentation [http://www.datasploit.info/en/latest](http://www.datasploit.info/en/latest)
