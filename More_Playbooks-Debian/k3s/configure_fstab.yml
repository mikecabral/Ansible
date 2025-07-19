```yaml
---
- name: Configure fstab and mount shares
  hosts: k3s_master
  become: true
  tasks:
    - name: Create mount directories
      file:
        path: "{{ item }}"
        state: directory
      loop:
        - /media/Jellyfin
        - /media/Jellyfin2
        - /media/Music

    - name: Create .vault directory
      become_user: youruser
      file:
        path: "/home/youruser/.vault"
        state: directory
        mode: "0700"

    - name: Copy .smbcred file
      copy:
        src: group_vars/.smbcred
        dest: /home/youruser/.vault/.smbcred
        mode: "0600"

    - name: Add entries to fstab
      blockinfile:
        dest: /etc/fstab
        block: |
          //192.168.x.x/Jellyfin /media/Jellyfin cifs credentials=/home/youruser/.vault/.smbcred,uid=1000,gid=1000,vers=3.0 0 0
          //192.168.x.x/Jellyfin2 /media/Jellyfin2 cifs credentials=/home/youruser/.vault/.smbcred,uid=1000,gid=1000,vers=3.0 0 0
          //192.168.x.x/Jellyfin2/Music /media/Music cifs credentials=/home/youruser/.vault/.smbcred,uid=1000,gid=1000,vers=3.0 0 0

    - name: Mount shares
      mount:
        name: "{{ item.name }}"
        src: "{{ item.src }}"
        fstype: cifs
        opts: credentials=/home/youruser/.vault/.smbcred,uid=1000,gid=1000,vers=3.0
        state: mounted
      loop:
        - { name: "/media/Jellyfin", src: "//192.168.x.x/Jellyfin" }
        - { name: "/media/Jellyfin2", src: "//192.168.x.x/Jellyfin2" }
        - { name: "/media/Music", src: "//192.168.x.x/Jellyfin2/Music" }


- name: Configure fstab and mount shares
  hosts: k3s_nodes
  become: true
  tasks:
    - name: Create mount directories
      file:
        path: "{{ item }}"
        state: directory
      loop:
        - /media/Jellyfin
        - /media/Jellyfin2
        - /media/Music

    - name: Create .vault directory
      become_user: youruser
      file:
        path: "/home/youruser/.vault"
        state: directory
        mode: "0700"

    - name: Copy .smbcred file
      copy:
        src: group_vars/.smbcred
        dest: /home/youruser/.vault/.smbcred
        mode: "0600"

    - name: Add entries to fstab
      blockinfile:
        dest: /etc/fstab
        block: |
          //192.168.x.x/Jellyfin /media/Jellyfin cifs credentials=/home/youruser/.vault/.smbcred,uid=1000,gid=1000,vers=3.0 0 0
          //192.168.x.x/Jellyfin2 /media/Jellyfin2 cifs credentials=/home/youruser/.vault/.smbcred,uid=1000,gid=1000,vers=3.0 0 0
          //192.168.x.x/Jellyfin2/Music /media/Music cifs credentials=/home/youruser/.vault/.smbcred,uid=1000,gid=1000,vers=3.0 0 0

    - name: Mount shares
      mount:
        name: "{{ item.name }}"
        src: "{{ item.src }}"
        fstype: cifs
        opts: credentials=/home/youruser/.vault/.smbcred,uid=1000,gid=1000,vers=3.0
        state: mounted
      loop:
        - { name: "/media/Jellyfin", src: "//192.168.x.x/Jellyfin" }
        - { name: "/media/Jellyfin2", src: "//192.168.x.x/Jellyfin2" }
        - { name: "/media/Music", src: "//192.168.x.x/Jellyfin2/Music" }
```
