Ansible-Roles
******************************
Roles are a way to group multiple tasks together into one container to do the automation in very effective manner with clean directory structures.

**Roles**: Roles are reusable units of automation that encapsulate tasks, variables, and handlers. They provide a way to organize and share Ansible content. Roles can be used to structure and modularize playbooks.
**Collections**: Collections are a more recent addition to Ansible Galaxy. They encompass roles, modules, and other content. Collections allow for better organization and distribution of Ansible content.

**ansible-galaxy** CLI is used to interact with Ansible Galaxy server. 
ansible-glaxy is the command to create the roles using the templates.

**default directory** /etc/ansible/roles  => roles path can be found in ansible/cfg file
=>anisble-galaxy init  /etc/ansible/roles/apache/<custom-role-name> --offline
=>ansible-galaxy install <author_name>.<role_name>  => installs the roles from anisble server/github depends on store..





complex project structure using the anisble,ci/cd,kubernetes
```
ansible_project/
├── ansible/
│   ├── inventory/
│   │   ├── production/
│   │   │   └── hosts
│   │   └── staging/
│   │       └── hosts
│   ├── group_vars/
│   │   ├── all.yml
│   │   ├── production/
│   │   │   ├── web_servers.yml
│   │   │   └── database_servers.yml
│   │   └── staging/
│   │       ├── web_servers.yml
│   │       └── database_servers.yml
│   ├── roles/
│   │   ├── nginx/
│   │   │   ├── defaults/
│   │   │   ├── tasks/
│   │   │   ├── templates/
│   │   │   └── meta/
│   │   ├── mysql/
│   │   │   ├── defaults/
│   │   │   ├── tasks/
│   │   │   └── meta/
│   │   └── common/
│   │       ├── tasks/
│   │       └── handlers/
├── kubernetes/
│   ├── microservices/
│   │   ├── service1/
│   │   │   ├── deployment.yaml
│   │   │   ├── service.yaml
│   │   │   ├── ingress.yaml
│   │   │   ├── secrets.yaml
│   │   │   └── other_k8s_files...
│   │   ├── service2/
│   │   │   ├── deployment.yaml
│   │   │   ├── service.yaml
│   │   │   ├── configmap.yaml
│   │   │   ├── hpa.yaml
│   │   │   └── other_k8s_files...
│   │   └── ...
│   └── k8s_manifests/
│       ├── namespace.yaml
│       ├── common_resources.yaml
│       ├── network_policy.yaml
│       └── other_k8s_files...
├── jenkins/
│   ├── Jenkinsfile
│   ├── build_scripts/
│   │   ├── build_script_1.sh
│   │   ├── build_script_2.sh
│   │   └── other_build_scripts...
│   ├── pipeline_scripts/
│   │   ├── deploy_microservice1.groovy
│   │   ├── deploy_microservice2.groovy
│   │   └── other_pipeline_scripts...
│   └── other_jenkins_files...

```

updating an installed role to the latest version...
    ansible-galaxy install --force <author_name>.<role_name>
If you have roles defined in a requirements.yml file, you can use the ansible-galaxy install -r requirements.yml --force command to update all roles listed in the file.

Here is an example of a requirements.yml file:
```
- name: geerlingguy.nginx
  version: v2.10.0

```
=>ansible-galaxy install -r requirements.yml --force

AWS project staructure
@@@@@@@@@@@@@@@@@@@@@@

```
my-eks-app/
├── roles/
│   ├── eks-cluster-role/
│   │   ├── defaults/
│   │   │   └── main.yml
│   │   ├── tasks/
│   │   │   ├── create_cluster.yml
│   │   │   └── delete_cluster.yml
│   │   └── handlers/
│   │       └── main.yml
│   ├── eks-nodegroup-role/
│   │   ├── defaults/
│   │   │   └── main.yml
│   │   ├── tasks/
│   │   │   ├── create_nodegroup.yml
│   │   │   └── delete_nodegroup.yml
│   │   └── handlers/
│   │       └── main.yml
│   ├── s3-bucket-role/
│   │   ├── defaults/
│   │   │   └── main.yml
│   │   ├── tasks/
│   │   │   ├── create_bucket.yml
│   │   │   └── delete_bucket.yml
│   │   └── handlers/
│   │       └── main.yml
│   ├── ec2-instance-role/
│   │   ├── defaults/
│   │   │   └── main.yml
│   │   ├── tasks/
│   │   │   ├── create_instance.yml
│   │   │   └── delete_instance.yml
│   │   └── handlers/
│   │       └── main.yml
│   ├── rds-instance-role/
│   │   ├── defaults/
│   │   │   └── main.yml
│   │   ├── tasks/
│   │   │   ├── create_instance.yml
│   │   │   └── delete_instance.yml
│   │   └── handlers/
│   │       └── main.yml
│   ├── iam-user-role/
│   │   ├── defaults/
│   │   │   └── main.yml
│   │   ├── tasks/
│   │   │   ├── create_user.yml
│   │   │   └── delete_user.yml
│   │   └── handlers/
│   │       └── main.yml
│   ├── k8s-deploy-role/
│   │   ├── defaults/
│   │   │   └── main.yml
│   │   ├── tasks/
│   │   │   ├── deploy_app.yml
│   │   │   └── undeploy_app.yml
│   │   └── handlers/
│   │       └── main.yml
│   └── k8s-namespace-role/
│       ├── defaults/
│       │   └── main.yml
│       ├── tasks/
│       │   ├── create_namespace.yml
│       │   └── delete_namespace.yml
│       └── handlers/
│           └── main.yml
├── inventories/
│   ├── development/
│   │   └── hosts
│   ├── staging/
│   │   └── hosts
│   └── production/
│       └── hosts
├── group_vars/
│   ├── all.yml
│   ├── development/
│   │   └── aws.yml
│   ├── staging/
│   │   └── aws.yml
│   └── production/
│       └── aws.yml
├── playbooks/
│   ├── deploy-eks-app.yml
│   └── deploy-app.yml

```
configure the role paths by setting the roles_path variable. By default, Ansible looks for roles in the roles/ directory within the playbook directory.

1. Specify Role Path in Command Line:
ansible-playbook -i inventory.ini my_playbook.yml --roles-path=/path/to/your/roles

2. Set roles_path in ansible.cfg:
```
[defaults]
roles_path = /path/to/your/roles
```
3. Set roles_path in Playbook:
```
---
- name: My Playbook
  hosts: all
  vars:
    roles_path: /path/to/your/roles
  roles:
    - my_role
    - another_role

```
