aws_ec2
=========

Description
-----------
Launch security group and provision three ec2-instance (t2.micro). All the instances are launched parallelly i.e ๐๐ฌ๐๐ ๐๐ฌ๐ฒ๐ง๐๐ก๐ซ๐จ๐ง๐จ๐ฎ๐ฌ ๐๐ฉ๐ฉ๐ซ๐จ๐๐๐ก, ๐จ๐ฉ๐ญ๐ข๐ฆ๐ข๐ณ๐๐ ๐๐จ๐ซ ๐๐๐๐๐๐ญ๐ข๐ฏ๐ ๐๐ฎ๐ญ๐จ๐ฆ๐๐ญ๐ข๐จ๐ง.


NOTEย : You can provision more ec2 instance by copy/paste the same code of worker or master in the aws_ec2/tasks/main.yml file.


Requirements
------------

`boto` `boto3` `botocore` packages are required.

Role is only tested on `ansible 2.10.3` version.

Role Variables
--------------

Variables required in aws_ec2  roleย :
* default VPC-id
*Subnet-id
*region
*Access Key
*Secret Key

```
---
# vars file for aws_ec2
K8S_key_name: "aws_key"
subnet_id: "subnet-ID"
region: "ap-south-1"
vpc_id: "vpc-ID"
sg_id: "{{ security_group_k8s['group_id'] }}"
access_key: "XXXXXXXXXXXXXXXXXX"
secret_key: "XXXXXXXXXXXXXXXXXX"
```


Example Playbook
----------------
master node
```
- name: Launcing Master instances.
  ec2_instance:
    region: "{{ region }}"
    aws_access_key: "{{ access_key }}"
    aws_secret_key: "{{ secret_key }}"
    name: "K8S_Master"
    key_name: "{{ K8S_key_name }}"
    instance_type: "{{ inst_type }}"
    image_id: "{{ img_id }}"
    security_group: "{{ sg_id }}"
    vpc_subnet_id: "{{ subnet_id }}"
    network:
        assign_public_ip: true
    state: present
    tags:
        K8S : master
        Kube : cluster
    wait: yes
  async: 180
  poll: 0
```


Author Information
------------------
### Connect me
* [Linkedin](https://linkedin.com/in/rahulkumar-choudhary-b662761a2 "Rahulkumar Choudhary")
* [Twitter](https://twitter.com/Rahulkumar29420 "Rahulkumar29420")
* [Medium](https://rahulchoudhary5768.medium.com/ "Rahulkumar Choudhary")
