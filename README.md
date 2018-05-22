query-packs
=========

Ansible role for importing query packs into Kolide (https://kolide.com)

Requirements
------------

If you want to download the query packs from an S3 bucket, you will need boto and your AWS credentials configured.

Query packs are from: https://github.com/palantir/osquery-configuration/tree/master/Endpoints/packs

Role Variables
--------------

kolide_url: "https://kolide.yourwebsite.com"   
kolide_user: "admin"  
kolide_pw: "password"  


Example Playbook
----------------
```
---
- hosts: localhost
  vars_files:
    - vars/main.yml
  tasks:
    - name: Import query packs
      include_role:
        name: query-packs
      with_items:
        - 'windows-application-security'
        - 'unwanted-chrome-extensions'
        - 'performance-metrics'
        - 'osx-attacks'
        - 'security-tooling-checks'
        - 'windows-compliance'
        - 'windows-registry-monitoring'
        - 'windows-attacks'
```

Author Information
------------------

@shortxstack
