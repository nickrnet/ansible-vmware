# ESXi Playbooks

## clean.yml

This playbook requires the use of the ['inventory/prod_db'](../../inventory/prod_db) inventory.

This playbook is written to be self explanatory. The goal is to create a VM template the other inventories use
that is semi-up-to-date with OS level patches for integration testing. It performs the following steps:

- Detects if a VM exists; deletes it if so
- Creates a new VM based on the updated OS template
- Runs the specified (mongo) role

Execute this playbook by running:

    ansible-playbook -i inventory/prod_db playbooks/prod_db/clean.yml
    
from the root of the project.

## snapshot.yml

This playbook requires the use of the ['inventory/prod_db'](../../inventory/prod_db) inventory.
                                      
This playbook is written to be self explanatory. The goal is to create a VM template the other inventories use
that is semi-up-to-date with OS level patches for integration testing. It performs the following steps:

- Reverts a VM to an initial snapshot that was based on the updated OS template
- Runs the specified (mongo) role

Execute this playbook by running:

    ansible-playbook -i inventory/prod_db playbooks/prod_db/clean.yml
  
from the root of the project.

## Results

The ['snapshot.yml'](./snapshot.yml) playbook is much faster as snapshots are used instead of the full build up of
a VM in the ESXi environment.
