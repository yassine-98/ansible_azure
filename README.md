# Ansible_Azure

## Project Overview:

The goal of this project is to perform the provisioning of an Azure virtual machine using Ansible.

## 1. Prerequisites:

- Ensure Ansible is installed on your control machine.
- Make sure to have created a Service Principal to facilitate authentication between your control machine and the Azure API.

### Steps:

1. Install the Azure CLI.
2. Run 'az login'.
3. Create a service principal with a contributor role:
    ```bash
    az ad sp create-for-rbac --name <service_principal_name> --role Contributor --scopes /subscriptions/<subscription_id>
    ```
4. Store the result in ~/.azure/credentials.
5. Install the azure_rm collection to use the modules:
    ```bash
    ansible-galaxy collection install azure.azcollection
    ```
6. Install dependencies required by the collection:
    ```bash
    pip3 install -r ~/.ansible/collections/ansible_collections/azure/azcollection/requirements-azure.txt
    ```

## 2. Run Ansible:

- To execute the playbook: 
  ```bash
  ansible-playbook playbooks/create_azure_vm.yml
  ```
- To check the created VM: 
  ```bash
  ansible-inventory -i myazure_rm.yml
  ```
- To Clean up resources: 
  ```bash
  az group delete --name <resource_group>
  ```
  or run 
  ```bash
  ansible-playbook playbooks/delete-rg.yml -e name=myResourceGroup
  ```

Feel free to customize the sections or add more details as needed.