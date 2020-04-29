## The LAB

The LAB is made of 3 containers to be managed by Ansible:

- Docker Debian
- Docker Ubuntu
- Docker Centos

Plus a Docker Ansible, to have and avoid installing Ansible on your laptop.

## Bootstrap Ansible LAB

To bootstrap this LAB, execute init.sh, it will perform the following tasks:

- Delete previous 3 containers Debian, Ubuntu et Centos
- Create an RSA key allowing Ansible connection through SSH
- Starting 3 instances Docker Debian, Docker Ubuntu, and Docker Centos
- Ssh key injection in each Docker instance using ssh-copy-id (password will be ask: toor)
- Ansible hosts inventory creation

To "ping" our 3 nodes:

```
docker run -it --rm -v `pwd`/hosts:/etc/ansible/hosts -v `pwd`/id_rsa:/root/.ssh/id_rsa itwars/ansible-cli all -m ping
```

```
172.17.0.3 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
172.17.0.4 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
172.17.0.2 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

To setup Nginx on Debian Ansible node:

```
docker run -it --rm -v `pwd`/hosts:/etc/ansible/hosts -v `pwd`/id_rsa:/root/.ssh/id_rsa itwars/ansible-cli debian -m apt -a "name=nginx state=present"
```

To start Nginx on Debian Ansible node:

```
docker run -it --rm -v `pwd`/hosts:/etc/ansible/hosts -v `pwd`/id_rsa:/root/.ssh/id_rsa itwars/ansible-cli debian -m service -a "name=nginx state=started"
```
