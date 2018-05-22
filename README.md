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
s3_bucket: "my-bucket-name"

Notes
----------------

Comment out the following in tasks/main.yml if you want to use the local JSON files instead of pulling from S3.
```
---
- name: Get query pack from S3
  aws_s3:
    bucket: "{{ s3_bucket }}"
    object: "{{ item }}.json"
    dest: "roles/query-packs/files/{{ item }}.json"
    mode: get
```

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
