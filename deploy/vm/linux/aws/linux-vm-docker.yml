```bash
---
- name: Deploy Linux VM on AWS and deploy Docker containers
  hosts: localhost
  connection: local
  gather_facts: no
  vars:
    image: ami-0ff8a91507f77f867
    instance_type: t2.micro
    keypair: my_aws_key
    security_group: my_security_group
    region: ca-central-1
    script: deploy-docker.sh
    config_script: config-settings.sh
    ssh_port: 2222
    ssh_key: /path/to/mykey.pem
    ssh_user: mike

  tasks:
  - name: Create an EC2 instance
    ec2:
      key_name: "{{ keypair }}"
      group: "{{ security_group }}"
      instance_type: "{{ instance_type }}"
      image: "{{ image }}"
      region: "{{ region }}"
      wait: true
      vpc_subnet_id: subnet-0e1f5e677c8f3f3c3
      assign_public_ip: yes
    register: ec2
    failed_when: ec2.failed or (ec2.instances|length == 0)

  - name: Add new instance to host group
    add_host:
      hostname: "{{ ec2.instances[0].public_ip }}"
      groupname: ec2_instances

- name: Change hostname
  hostname:
    name: "{{ new_hostname }}"

- name: reboot the system
  reboot:
    async: 300
    poll: 30

  - name: Update the system
    apt:
      update_cache: yes
    when: ansible_os_family == "Debian"

  - name: Install python3, python3-dev, python3-pip
    apt:
      name: ["python3", "python3-dev", "python3-pip"]
      state: present
    when: ansible_os_family == "Debian"

- name: Add the Telegraf repository
  apt_repository:
    repo: 'deb https://packages.influxdata.com/telegraf/repos/apt buster stable'
    state: present
    key_url: 'https://packages.influxdata.com/influxdb.key'
    update_cache: yes
    when: ansible_os_family == "Debian"

- name: Install Telegraf
  apt:
    name: telegraf
    state: present
    update_cache: yes
    when: ansible_os_family == "Debian"

- name: Configure Telegraf
  template:
    src: telegraf.conf.j2
    dest: /etc/telegraf/telegraf.conf
  vars:
    influxdb_server: "{{ influxdb_server }}"
    influxdb_org: "{{ influxdb_org }}"
    influxdb_bucket: "{{ influxdb_bucket }}"

- name: Allow only specific ports
  ec2_group:
    name: "{{ security_group }}"
    region: "{{ region }}"
    rules:
      - proto: tcp
        from_port: 2222
        to_port: 2222
        cidr_ip: 0.0.0.0/0

  - name: Install Docker
    apt:
      name: docker.io
      state: present
    when: ansible_os_family == "Debian"

  - name: Install Docker Compose
    shell: pip3 install docker-compose
    when: ansible_os_family == "Debian"

  - name: Create new user "mike"
    user:
      name: "{{ ssh_user }}"
      state: present
      groups: sudo
      shell: /bin/bash
    delegate_to: "{{ ec2.instances[0].public_ip }}"

  - name: Add ssh key for new user
    authorized_key:
      user: "{{ ssh_user }}"
      state: present
      key: "{{ lookup('file', ssh_key) }}"
    delegate_to: "{{ ec2.instances[0].public_ip }}"
    when: ssh_key is defined

  - name: copy script to remote server
    copy:
      src: "{{ script }}"
      dest: /tmp/deploy-docker.sh
      remote_src: yes

  - name: run script to deploy Docker containers
    shell: chmod +x /tmp/deploy-docker.sh; /tmp/deploy-docker.sh
    delegate_to: "{{ ec2.instances[0].public_ip }}"
    failed_when: "'command not found' in ansible_job_result.stderr"

  - name: copy config script to remote server
    copy:
      src: "{{ config_script }}"
      dest: /tmp/config-settings.sh
      remote_src: yes

  - name: run config script
    shell: chmod +x /tmp/config-settings.sh; /tmp/config-settings.sh
    delegate_to: "{{ ec2.instances[0].public_ip }}"
    failed_when: "'command not found' in ansible_job_result.stderr"

  - name: Disable root login
    lineinfile:
      path: /etc/ssh/sshd_config
      regexp: '^PermitRootLogin'
      line: 'PermitRootLogin no'
    delegate_to: "{{ ec2.instances[0].public_ip }}"

  - name: Change SSH port
    lineinfile:
      path: /etc/ssh/sshd_config
      regexp: '^#?Port'
      line: 'Port {{ ssh_port }}'
    delegate_to: "{{ ec2.instances[0].public_ip }}"

  - name: Reload SSH
    service:
      name: ssh
      state: restarted
    delegate_to: "{{ ec2.instances[0].public_ip }}"

  - name: Disable port 22
    ec2_group:
      name: "{{ security_group }}"
      region: "{{ region }}"
      rules:
        - proto: tcp
          from_port: 22
          to_port: 22
          cidr_ip: 0.0.0.0/0
          rule_action: remove



This playbook will create an EC2 instance on AWS, it will add the new instance to a host group, update the system, install Python3, python3-dev, python3-pip and Telegraf and then install Docker and Docker Compose. Then it will create the new user "mike" and add his ssh key to the server at the same time. Then it will copy the script to the remote server and run it to deploy the Docker containers. Once the script is done, it will copy the config script to the remote server, and run the config script to configure user and system settings.
It will also Disable root login, change the ssh port and disable port 22.
```
