# ansible-vmware

Working with Ansible and VMware ESXi/vCenter

## Prerequisites

- VMware ESXi
- vCenter
- Ansible 2.4.4 or greater
- one VM template in VMware ESXi/vCenter with an OS installed to use as a source

That last one for me is basically the following:
1. Create a VM in ESXi
2. Install an OS on it
3. Convert it to a template

## Caveats

My current VMware ESXi environment is statically managed - No DHCP, no LDAP, not much use
of DNS - so that means that dynamic inventory doesn't apply and things are managed by a `hosts`
file for the most part.

I also primarily only use Linux, and RedHat at that. This project doesn't have much
Windows+Ansible at the moment, though it's on the list to get in at some point. 

## Usage

Use `pip` and `pipenv`.

    sudo easy_install pip
    pip install pipenv
    pipenv install
    pipenv shell
    
    ansible all -i inventory --list-hosts
    ansible-playbook -i inventory/esxi playbooks/esxi/update_template.yml
    ansible-playbook -i inventory/prod_db playbooks/esxi/refresh_vm.yml
    ansible-playbook -i inventory/prod_db playbooks/esxi/create_snapshot.yml
    ansible-playbook -i inventory/prod_db playbooks/prod_db/clean.yml
    ansible-playbook -i inventory/prod_db playbooks/prod_db/snapshot.yml
    
If you don't want to use `pipenv`, you need to have

- ansible
- passlib
- pyvmomi

in your `PYTHONPATH`.

Set the variable values in [roles/esxi/vars/main.yml](./roles/esxi/vars/main.yml)
for your VMware ESXi/vCenter environment.

Set the variable values in [inventory/esxi/group_vars/all.yml](./inventory/esxi/group_vars/all.yml)
for your VMware ESXi/vCenter environment.

Set the variable values for each host in the [esxi inventory](./inventory/esxi/host_vars).

Set the variable values for each host in the [prod_db inventory](./inventory/prod_db/host_vars).

Set the proper configurations in [roles/common/files](./roles/common/files).

## Notes

The `vmware_guest` module in Ansible has more functionality than what is demonstrated here.

There are potential opportunities for naming convention collisions: My VMware environment is tiny,
so I don't use the approach of dynamic inventory at all, though it should be investigated. That
means you should **pay attention to naming conventions,** or change the plays/tasks to use the
returned ids from the vmware_guest module.

Performance could probably be improved with more `register` and `when` combinations in the roles.
That is an exercise for the user.
