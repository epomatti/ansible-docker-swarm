# Docker Swarm with Ansible

Code to provision and configure a Docker Swarm cluster on Azure Cloud using Ansible playbooks.

## Swarm

![Swarm Cluster](cluster.png)


## Running it

```sh
ansible-playbook release.yml --extra-vars "@some_file.json"
```

## Sources

[Ansible Azure Guide](https://docs.ansible.com/ansible/latest/scenario_guides/guide_azure.html)

[Ansible Azure modules](https://docs.ansible.com/ansible/2.9/modules/list_of_cloud_modules.html#azure)

[Azure Ansible Quickstart](https://docs.microsoft.com/en-us/azure/developer/ansible/vm-configure?tabs=ansible#complete-sample-ansible-playbook)
