##### Check version of Debian
```
ansible acidburn -m shell -a "lsb_release -a"
```

##### Check version of Rocky or Red Hat
```bash
ansible crashoverride -m shell -a "cat /etc/redhat-release"
```

##### Check version of Oracle Linux
```bash
ansible master -m shell -a "cat /etc/oracle-release"
```

