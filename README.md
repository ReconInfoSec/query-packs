query-packs
=========

Ansible role for importing query packs into Kolide (https://kolide.com)

Requirements
------------

Must have Ansible installed.

If you want to download the query packs from an S3 bucket, you will need to pip install boto, and you will need the AWS CLI installed with your AWS credentials configured (`pip install awscli` or `brew install awscli`, or similar).

Otherwise, you should only need to pip install requests.

Query packs are from: https://github.com/palantir/osquery-configuration/tree/master/Classic/Endpoints/packs

How To
--------------

1. Clone the repo
2.
```
cd query-packs
ansible-playbook main.yml
```

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
