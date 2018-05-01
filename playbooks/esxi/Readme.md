# ESXi Playbooks

## update_template.yml

This playbook requires the use of the `inventory/esxi` inventory.

This playbook is written to be self explanatory. The goal is to create a VM template the other inventories use
that is semi-up-to-date with OS level patches for integration testing. It performs the following steps:

- Detects if a template exists; deletes it if so
- Creates a new VM based on the base OS template
- Deploys yum repositories, and host definitions
- Updates the OS packages
- Shuts down the VM and converts it to a template used by the other relevant inventories

The template that is produced has a date stamp in its notes to reflect the last time it was run.

This playbook can be executed with:

    ansible-playbook -i inventory/esxi playbooks/esxi/update_template.yml
    
from the root of the project.

This playbook could be periodically executed by a scheduled job configured on a build server.
