```yaml
- name: Remove fstab entries and unmount shares
  hosts: k3s_master
  become: true
  tasks:
    - name: Unmount shares
      mount:
        name: "{{ item.name }}"
        src: "{{ item.src }}"
        fstype: cifs
        state: unmounted
      loop:
        - { name: "/media/Jellyfin", src: "//192.168.x.x/Jellyfin" }
        - { name: "/media/Jellyfin2", src: "//192.168.x.x/Jellyfin2" }
        - { name: "/media/Music", src: "//192.168.x.x/Jellyfin2/Music" }

    - name: Remove entries from fstab
      replace:
        path: /etc/fstab
        regexp: "{{ item.regexp }}"
        replace: ""
      loop:
        - { regexp: '^//192\.168\.x\.x/Jellyfin /media/Jellyfin.*' }
        - { regexp: '^//192\.168\.x\.x/Jellyfin2 /media/Jellyfin2.*' }
        - { regexp: '^//192\.168\.x\.x/Jellyfin2/Music /media/Music.*' }

- name: Remove fstab entries and unmount shares
  hosts: k3s_nodes
  become: true
  tasks:
    - name: Unmount shares
      mount:
        name: "{{ item.name }}"
        src: "{{ item.src }}"
        fstype: cifs
        state: unmounted
      loop:
        - { name: "/media/Jellyfin", src: "//192.168.x.x/Jellyfin" }
        - { name: "/media/Jellyfin2", src: "//192.168.x.x/Jellyfin2" }
        - { name: "/media/Music", src: "//192.168.x.x/Jellyfin2/Music" }

    - name: Remove entries from fstab
      replace:
        path: /etc/fstab
        regexp: "{{ item.regexp }}"
        replace: ""
      loop:
        - { regexp: '^//192\.168\.x\.x/Jellyfin /media/Jellyfin.*' }
        - { regexp: '^//192\.168\.x\.x/Jellyfin2 /media/Jellyfin2.*' }
        - { regexp: '^//192\.168\.x\.x/Jellyfin2/Music /media/Music.*' }
```
