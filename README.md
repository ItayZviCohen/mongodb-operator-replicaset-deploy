# mongodb-operator-replicaset-deploy

An Ansible playbook for deploying and patching a MongoDB replicaset via the MongoDB kubernetes operator.

## Getting Started

```
git clone git@github.com:ItayZviCohen/mongodb-operator-replicaset-deploy.git

cd mongodb-operator-replicaset-deploy

pip install requirements.txt

ansible-playbook deploy.yml -e "k8s_source_ip_cidr='<cidr of the cluster source ip>' ops_manager_url='<Ops Manager/Cloud manager URL>' k8s_api_url='<kuberneets api server URL>' k8s_namespace='<kubernetes namespace>' mongodb_replicaset_name='<replcaset's name>' ops_manager_admin_public_key='<Ops manager/Cloud manager global public api key>' ops_manager_admin_private_key='<Ops manager/ Cloud Manager global private api key' k8s_api_key='<kubernetes api bearer token>' [mongodb_replicaset_members='3' mongodb_replicaset_version='4.2.2-ent']"
```

### Prerequisites

Kubernetes:
  - A kubernetes cluster.
  - A [MongoDB kubernetes operator](https://docs.mongodb.com/kubernetes-operator/stable) installed with [cluster-wide topology](https://docs.mongodb.com/kubernetes-operator/stable/tutorial/plan-k8s-operator-install/#cluster-wide-scope).
  - A MongoDB [Ops Manager](https://www.mongodb.com/products/ops-manager) or a [Cloud Manager](https://www.mongodb.com/cloud/cloud-manager) instance.

On the Ansible Runner:

 Packages:
  - ansible >= 2.9

 Python:
  See [requirements.txt](https://github.com/ItayZviCohen/mongodb-operator-replicaset-deploy/blob/master/requirements.txt) for exact dependencies.

## AWX Support

Create a container group with this pod configuration:
```
apiVersion: v1
kind: Pod
metadata:
  namespace: default
spec:
  containers:
    - image: itayzvicohen/awx-container-group:latest
      tty: true
      stdin: true
      args:
        - sleep
        - infinity
```

## Hashicorp Vault support
This playbook support Hashicorp Vault's kv2 secret engine.
All the secret variables need to be stored in one secret like so:

```
<Kv2 secret engine>
└── <secret name>
    ├── k8s_api_key
    ├── ops_manager_admin_public_key
    └── ops_manager_admin_private_key
```

**Note:** All the keys inside your secret need to be identical to the ones in this diagram.

Now, when calling the playbook, do not pass the above variables as extra-vars. Instead, supply the following parameters:
|Name|Type|Description |
|----|----|------------|
| hashi_vault_secret_engine|string|The name of your secret engine|
| hashi_vault_secret_name|string|  The name/path of your secret (Example: mongodb-vars or databases/mongodb)|
| hashi_vault_secret_token|string|A token for Vault authentication|
| hashi_vault_secret_url|string|The full url of your Vault (Example: https://vault.example.com:8200)|

## Built With

* [Ansible](https://docs.ansible.com/) - Configuration management tool

## Authors

* **Itay Zvi Cohen** - *Initial work* - [ItayZviCohen](https://github.com/ItayZviCohen)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
