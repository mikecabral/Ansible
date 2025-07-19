```yaml
---
- name: Upload script to user's home directory
  hosts: 
    - gibson
    - k3s_master
    - k3s_nodes
  become: true

  vars:
    username: user # username /home/user <---
    script_path: /home/user/scripts/debian-security-only.sh

  tasks:
    - name: Create scripts directory if it doesn't exist
      file:
        path: "/home/{{ username }}/scripts"
        state: directory
        mode: '0755'

    - name: Copy script to user's home/scripts directory
      ansible.builtin.copy:
        src: "{{ script_path }}"
        dest: "/home/{{ username }}/scripts"
        mode: '0755'

```

