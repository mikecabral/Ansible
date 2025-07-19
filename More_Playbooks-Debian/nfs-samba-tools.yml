```yaml
---
- nfs-utils
- hosts: master
  become: yes
  tasks:
  - name: Install Samba and NFS Tools / multiple packages using dnf (MASTER/ORACLE9)
    dnf:
      name:
        - samba
        - samba-client
        - samba-common-tools
        - cifs-utils
        - nfs-utils
      state: present

- hosts: node1
  become: yes
  tasks:
  - name: Install Samba and NFS Tools / multiple packages using dnf (ROCKY9)
    dnf:
      name:
        - samba
        - samba-client
        - samba-common-tools
        - cifs-utils
        - nfs-utils
      state: present

- hosts: node2
  become: yes
  tasks:
  - name: Install Samba and NFS Tools / multiple packages using apt (DEBIAN11)
    apt:
      name:
        - samba
        - smbclient
        - samba-common
        - cifs-utils
        - nfs-common
        - nfs-kernel-server
      state: present

- hosts: node3
  become: yes
  tasks:
  - name: Install Samba and NFS Tools / multiple packages using apt (DEBIAN11)
    apt:
      name:
        - samba
        - smbclient
        - samba-common
        - cifs-utils
        - nfs-common
        - nfs-kernel-server
      state: present
```
