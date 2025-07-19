##### Set static IP address for Oracle Linux 9
```yaml
---
- name: Set static IP address using nmcli for a specific NIC (MASTER)
  hosts: master
  become: yes

  tasks:
    - name: Set static IP address for Oracle Linux 9
      block:
        - command: nmcli connection modify ens33 ipv4.method manual ipv4.addresses 172.16.16.x/24 ipv4.gateway 172.16.16.1 connection.interface-name ens33
          notify:
            - Restart network
  handlers:
    - name: Restart network
      service:
        name: NetworkManager
        state: restarted
```

##### Set static IP address for Rocky Linux 9
```yaml
---
- name: Set static IP address using nmcli for a specific NIC (CRASHOVERRIDE)
  hosts: crashoverride
  become: yes

  tasks:
    - name: Set static IP address for Rocky Linux 9
      block:
        - command: nmcli connection modify ens33 ipv4.method manual ipv4.addresses 172.16.16.x/24 ipv4.gateway 172.16.16.1 connection.interface-name ens33
          notify:
            - Restart network
  handlers:
    - name: Restart network
      service:
        name: NetworkManager
        state: restarted
```

##### Set static IP address for Debian 11 without nmcli (/etc/network/interfaces)
#### CerealKiller
```yaml
---
- name: Set static IP address for a specific NIC Debian 11 (CEREALKILLER)
  hosts: cerealkiller
  become: yes

  vars:
    interface_name: ens192
    ip_address: 172.16.16.x
    subnet_mask: 255.255.255.0
    gateway_address: 172.16.16.1

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

##### Set static IP address for Debian 11 without nmcli (/etc/network/interfaces)
#### AcidBurn
```yaml
---
- name: Set static IP address for a specific NIC Debian 11 (ACIDBURN)
  hosts: acidburn
  become: yes

  vars:
    interface_name: ens192
    ip_address: 172.16.16.x
    subnet_mask: 255.255.255.0
    gateway_address: 172.16.16.1

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
