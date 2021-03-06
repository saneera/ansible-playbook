# Strimzi Ansible Playbook

## About
This [Ansible Playbook](http://docs.ansible.com/ansible/playbooks.html) includes
a set of different roles:

* **strimzi-openshift**: Deploy or undeploy cluster components of Strimzi.
* **strimzi-operator**: Deploy or undeploy namespace componentes of Strimzi.
* **ocp-get-token**: To get an OCP User Auth token.

**NOTE:** This playbooks must be executed with **cluster-admin** users.

## Ansible Requirements

This playbook has tested with the next Ansible versions:

	ansible 2.7.9

## Ansible Roles

### Global Variables
Each playbook will use a set of Global Variables with values that it will be the same for all of them.

These variables will be defined in YAML files in [vars](./vars) folder.

**namespaces.yml** file defines the list of different namespaces to manage. This file is similar to:

    namespaces:
    - { namespace: strimzi, user: developer, state: "{{ state }}" }

* **namespace**: Namespace to (un)deploy Strimzi
* **user**: User to manage Strimzi. This user is a non cluster-admin user.
* **state**: Defined to deploy (*present*) or undeploy (*absent*) objects

### strimzi-openshift role

Deploy all cluster objects needed into a OpenShift cluster.

* Cluster Roles
* Strimzi CRDs: Kafka, KafkaTopic, KafkaUser, ...

##### Example playbook

To deploy this playbook:

    ansible-playbook -c local strimzi-deploy-openshift.yml

[01.strimzi-deploy-openshift.yml](01.strimzi-deploy-openshift.yml) is a full playbook.

To undeploy this playbook:

    ansible-playbook -c local strimzi-undeploy-openshift.yml

[strimzi-undeploy-openshift.yml](strimzi-undeploy-openshift.yml) is a full playbook.

### strimzi-operator role

Deploy all namespaced objects needed into an OpenShift namespace.

* Service Accounts
* Cluster Role Bindings and Role Bindings
* Cluster Operator deployment

##### Example playbook

To deploy this playbook:

    $ ansible-playbook -c local strimzi-deploy-operator.yml

[02.strimzi-deploy-operator.yml](02.strimzi-deploy-operator.yml) is a full playbook.

To undeploy this playbook:

    $ ansible-playbook -c local strimzi-undeploy-operator.yml

[strimzi-undeploy-operator.yml](strimzi-undeploy-operator.yml) is a full playbook.

### strimzi-kafka role

Deploy a Kafka Cluster

##### Example playbook

To deploy this playbook:

    $ ansible-playbook -c local strimzi-deploy-kafka.yml

[03.strimzi-deploy-kafka.yml](03.strimzi-deploy-kafka.yml) is a full playbook.

To undeploy this playbook:

    $ ansible-playbook -c local strimzi-undeploy-kafka.yml

[strimzi-undeploy-kafka.yml](strimzi-undeploy-kafka.yml) is a full playbook.
