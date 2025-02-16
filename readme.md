# Proxmox VE Cloud-init VM Template

## summary

Ansible playbook for creating a Cloud-init enabled VM Template for ProxmoxVE.  
Currently supports Ubuntu 22.04 cloud-img, but plans to expand to other supported OSes in the future.  

## Setup Method

### Set up a machine to run Ansible

```bash
sudo apt install sshpass ansible -y
```

### Create a configuration file

Create a configuration file referring to `example.hosts.yaml`

### Deploy VM Template for Ubuntu 22.04

```bash
ansible-playbook -i example.hosts.yaml templates/ubuntu22.04-template-v1.0.0/main.yaml
```

---

## Reference

- https://homelabing.fr/how-to-automate-proxmox-ve-using-ansible/
