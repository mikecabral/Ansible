```yaml
---
- hosts: master
  become: yes
  tasks:
  - name: Install Public Keys (MASTER)
    ansible.posix.authorized_key:
      user: masteruser
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
  - name: Change Sudoers File (Oracle 9)
    lineinfile:
      path: /etc/sudoers
      state: present
      regexp: '^%wheel'
      line: '%masteruser ALL=(ALL) NOPASSWD: ALL'
      validate: /usr/sbin/visudo -cf %s

- hosts: node1
  become: yes
  become_method: sudo
  tasks:
  - name: Install Public Keys
    ansible.posix.authorized_key:
      user: node1user
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
  - name: Change Sudoers File (Rocky Linux 9)
    lineinfile:
      path: /etc/sudoers
      state: present
      regexp: '^%wheel'
      line: '%node1user ALL=(ALL) NOPASSWD: ALL'
      validate: /usr/sbin/visudo -cf %s

- hosts: node2
  become: yes
  tasks:
  - name: Install Public Keys
    ansible.posix.authorized_key:
      user: node2user
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
  - name: Change Sudoers File (Debian 11)
    lineinfile:
      path: /etc/sudoers
      state: present
      regexp: '^%sudo'
      line: '%node2user ALL=(ALL) NOPASSWD: ALL'
      validate: /usr/sbin/visudo -cf %s


- hosts: node3
  become: yes
  tasks:
  - name: Install Public Keys
    ansible.posix.authorized_key:
      user: node3user
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
  - name: Change Sudoers File (Debian 11)
    lineinfile:
      path: /etc/sudoers
      state: present
      regexp: '^%sudo'
      line: '%node3user ALL=(ALL) NOPASSWD: ALL'
      validate: /usr/sbin/visudo -cf %s
```
