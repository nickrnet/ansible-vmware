# Playbooks

## 'esxi' Playbooks

These playbooks manage a template for OS updates. The
[`esxi/update_template.yml`](./esxi) file is the main play for managing things in
VMware ESXi/vCenter.

## 'prod_db' Playbooks

Creates a VM from the specified template and installs MongoDB. The
[`prod_db/snapshot.yml`](./prod_db) file is the main play for managing things
in VMware ESXi/vCenter.
