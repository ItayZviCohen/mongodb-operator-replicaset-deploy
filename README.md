# mongodb-operator-replicaset-deploy

An Ansible playbook for deploying and patching a MongoDB replicaset via the MongoDB kubernetes operator.

## Getting Started

```
git clone git@github.com:ItayZviCohen/mongodb-operator-replicaset-deploy.git

cd mongodb-operator-replicaset-deploy

ansible-playbook deploy.yml -e "ops_manager_url='https://<Ops manager/Cloud manager url>:<port>' k8s_api_url='https://<k8s api server address>' k8s_namespace='tit' mongodb_replicaset_name='<replica set name>' ops_manager_admin_public_key='<global public api key>' ops_manager_admin_private_key='<global private api key>'"
```

### Prerequisites

Kubernetes:
  - A kubernetes cluster
  - A [MongoDB kubernetes operator](https://docs.mongodb.com/kubernetes-operator/stable) insatlled with [cluster-wide topology](https://docs.mongodb.com/kubernetes-operator/stable/tutorial/plan-k8s-operator-install/#cluster-wide-scope)
  - A MongoDB [Ops Manager](https://www.mongodb.com/products/ops-manager) or a [Cloud Manager](https://www.mongodb.com/cloud/cloud-manager)

On the Ansible Runner:

 Packages:
  - ansible >= 2.9

 Python:
  - ansible >= 2.9
  - python >= 2.7
  - openshift >= 0.6
  - PyYAML >= 3.11
  - See [requirements.txt](https://github.com/ItayZviCohen/mongodb-operator-replicaset-deploy/blob/master/requirements.txt) for exact dependencies.

## Built With

* [Ansible](https://docs.ansible.com/) - Configuration management tool

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Authors

* **Itay Zvi Cohen** - *Initial work* - [ItayZviCohen](https://github.com/ItayZviCohen)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
