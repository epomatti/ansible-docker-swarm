# Docker Swarm with Ansible

Code to provision and configure a Docker Swarm cluster on Azure Cloud using Ansible playbooks.

## Swarm

![Swarm Cluster](docs/cluster.png)


## Running it

Log in to Azure Cloud Shell and run the playbooks:

```sh
ansible-playbook src/provision.yml \
    --extra-vars '{"instance":"development","ssh_key_file_path":"~/.ssh/id_rsa.pub"}'
```

Create the inventory file ([example](https://github.com/ansible/ansible/blob/devel/examples/hosts.yaml)):

```yml
all:
  vars:
    ansible_ssh_private_key_file: <KEY>
    ansible_user: <USER>
  children:
    managers:
      hosts:
        manager001:
          ansible_ssh_host: <IP_ADDRESS>
          private_ip_address: <IP_ADDRESS>
    workers:
      hosts:
        worked001:
          ansible_ssh_host: <IP_ADDRESS>
          private_ip_address: <IP_ADDRESS>
      vars:
        join_manager_node_public: <IP_ADDRESS>
        join_manager_node_private: <IP_ADDRESS>
```

Install and config Docker:

```sh
ansible-playbook src/install-docker-playbook.yml -i inventory.yml -l all

ansible-playbook src/config-docker-playbook.yml -i inventory.yml -l all
```

For Swarm the [docker](https://pypi.org/project/docker/) python dependency is required in your local machine.

```
pip install docker
```

Config Swarm cluster:

```sh
ansible-playbook src/install-swarm-playbook.yml -i inventory.yml
```

### Local Ansible

Optionally, you may want to run Ansible locally.

```sh
sudo apt-get install python3-venv
python3 -m venv env
. env/bin/activate
pip install --upgrade pip
pip install -r https://raw.githubusercontent.com/ansible-collections/azure/dev/requirements-azure.txt
pip install 'ansible'
```

## Sources

[Ansible Azure Guide](https://docs.ansible.com/ansible/latest/scenario_guides/guide_azure.html) | [Ansible Azure collections](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) | [Azure Ansible Quickstart](https://docs.microsoft.com/en-us/azure/developer/ansible/vm-configure?tabs=ansible#complete-sample-ansible-playbook) | [Reuse playbooks](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse.html) | [Run Ansible in Parallel](https://toptechtips.github.io/2019-07-09-ansible_run_playbooks_tasks_in_parallel/) | [Install docker remotely with Ansible](https://www.rechberger.io/tutorial-install-docker-using-ansible-on-a-remote-server/) | [Sample repo for swarm automation](https://github.com/ruanbekker/ansible-docker-swarm) | [Docker Swarm Orchestration](https://upcloud.com/community/tutorials/docker-swarm-orchestration/) | [How to build your inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
