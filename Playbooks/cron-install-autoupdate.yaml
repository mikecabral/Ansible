### This is for Ubuntu 22.04 LTS ONLY!!
```bash
---
- name: Set up cron job for the script
  hosts:
    - rancher
  become: true

  vars:
    username: mike
    script_name: debian-security-only.sh
    cron_job_name: security_only_updates
    cron_schedule: "30 23 * * *"

  tasks:
    - name: Install cron package
      apt:
        name: cron
        state: present

    - name: Add cron job
      cron:
        name: "{{ cron_job_name }}"
        user: "{{ username }}"
        job: "/home/{{ username }}/{{ script_name }}"
        state: present
        cron_file: "{{ username }}"
        special_time: daily
```
