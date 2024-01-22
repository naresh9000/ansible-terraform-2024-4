Ansible_tower
***************************
For dynamic inventory plugin
**ref**::https://docs.ansible.com/ansible/latest/collections/amazon/aws/docsite/aws_ec2_guide.html

Inventory Plugins
aws_ec2 inventory – EC2 inventory source

aws_rds inventory – RDS instance inventory source

In oder to deal with changing public ip addresses in aws,static inventory pose the concern for ansbile controled machines,so for ansible to deal with dynamic inventories when it changes during the auto scaling and auto healiing,terraform tainting ,we have the ec2 dynamic inventory plugin which handles without the downtime..

**Minimal Example**
Fetch all hosts in us-east-1, the hostname is the public DNS if it exists, otherwise the private IP address.

# demo.aws_ec2.yml
plugin: amazon.aws.aws_ec2

# This sets the region. If empty (the default) default this will include all regions, except possibly
# restricted ones like us-gov-west-1 and cn-north-1.
regions:
- us-east-1
After providing any required options, you can view the populated inventory with ansible-inventory -i demo.aws_ec2.yml --graph:

@all:
 |--@aws_ec2:
 |  |--ip-10-210-0-189.ec2.internal
 |  |--ip-10-210-0-195.ec2.internal
 |--@ungrouped: