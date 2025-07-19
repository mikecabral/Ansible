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
  - name: Change Sudoers File (Oracle 9)
    lineinfile:
      path: /etc/sudoers
      state: present
      regexp: '^%wheel'
      line: '%eugene ALL=(ALL) NOPASSWD: ALL'
      validate: /usr/sbin/visudo -cf %s

- hosts: crashoverride
  become: yes
  become_method: sudo
  tasks:
  - name: Install Public Keys (CRASHOVERRIDE)
    ansible.posix.authorized_key:
      user: zerocool
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
  - name: Change Sudoers File (Rocky Linux 9)
    lineinfile:
      path: /etc/sudoers
      state: present
      regexp: '^%wheel'
      line: '%zerocool ALL=(ALL) NOPASSWD: ALL'
      validate: /usr/sbin/visudo -cf %s

- hosts: acidburn
  become: yes
  tasks:
  - name: Install Public Keys (ACIDBURN)
    ansible.posix.authorized_key:
      user: kate
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
  - name: Change Sudoers File (Debian 11)
    lineinfile:
      path: /etc/sudoers
      state: present
      regexp: '^%sudo'
      line: '%kate ALL=(ALL) NOPASSWD: ALL'
      validate: /usr/sbin/visudo -cf %s


- hosts: cerealkiller
  become: yes
  tasks:
  - name: Install Public Keys (CEREALKILLER)
    ansible.posix.authorized_key:
      user: emmanuel
      state: present
      key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
  - name: Change Sudoers File (Debian 11)
    lineinfile:
      path: /etc/sudoers
      state: present
      regexp: '^%sudo'
      line: '%emmanuel ALL=(ALL) NOPASSWD: ALL'
      validate: /usr/sbin/visudo -cf %s
```