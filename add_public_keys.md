```yaml
---
- hosts: master
  become: yes
  tasks:
  - name: Install Public Keys (MASTER)
    ansible.posix.authorized_key:
      user: eugene
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"


- hosts: crashoverride
  become: yes
  tasks:
  - name: Install Public Keys (CRASHOVERRIDE)
    ansible.posix.authorized_key:
      user: zerocool
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"

- hosts: acidburn
  become: yes
  tasks:
  - name: Install Public Keys (ACIDBURN)
    ansible.posix.authorized_key:
      user: kate
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"

- hosts: cerealkiller
  become: yes
  tasks:
  - name: Install Public Keys (CEREALKILLER)
    ansible.posix.authorized_key:
      user: emmanuel
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
```
