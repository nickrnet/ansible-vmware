# ESXi Inventory

This inventory is managed by groups. The tasks are called in the playbooks by group.

## 'local' Group

This group is for the local machine. The Ansible `vmware_guest` module is typically set to 
`delegate_to: localhost`, so the local machine must be in the inventory.

## 'dest_template' Group

This is a host in the VMware environment that will be turned on from the src_template defined
in the `all.yml` file of the `group_vars` in the `esxi` inventory.

## 'vms' Group

This is a test VM in the VMware environment that can be turned on from template.
