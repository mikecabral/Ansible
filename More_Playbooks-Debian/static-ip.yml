```yaml
---
- name: Set static IP address for a specific NIC Debian 11 (ACIDBURN)
  hosts: linux_host
  become: yes

  vars:
    interface_name: ens192
    ip_address: 172.16.16.x
    subnet_mask: 255.255.255.0
    gateway_address: 172.16.x.x

  tasks:
    - name: Check current IP address configuration
      command: /sbin/ip -o -4 addr show {{ interface_name }}
      register: ip_output
      changed_when: false
      check_mode: no

    - name: Configure static IP address
      lineinfile:
        dest: /etc/network/interfaces
        regexp: "^\\s*iface\\s+{{ interface_name }}"
        line: |
          auto {{ interface_name }}
          iface {{ interface_name }} inet static
          address {{ ip_address }}
          netmask {{ subnet_mask }}
          gateway {{ gateway_address }}
        backrefs: yes
      when: ip_address not in ip_output.stdout_lines[0]

      notify:
        - Restart network

  handlers:
    - name: Restart network
      service:
        name: networking
        state: restarted
```
