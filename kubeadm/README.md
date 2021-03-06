# Heat template for Kubeadm v1.13.5
A Heat template to deploy a Kubernetes cluster on the OpenStack cloud.

## Quick Start
First, you must be installed OpenStack CLI tool on your machine, you can execute the following command to install:
```sh
$ virutalenv .env
$ source .env/bin/activate
$ pip install -r requirements.txt
```

Create client environment scripts for the projects and users:
```sh
$ cat <<EOF > openrc
export OS_PROJECT_DOMAIN_NAME=default
export OS_PROJECT_DOMAIN_ID=default
export OS_USER_DOMAIN_NAME=default
export OS_REGION_NAME=RegionOne
export OS_PROJECT_NAME=admin
export OS_TENANT_NAME=admin
export OS_USERNAME=admin
export OS_PASSWORD=password
export OS_AUTH_URL=http://YOUR_OPENSTACK_HOST/identity
export OS_IDENTITY_API_VERSION=3
export OS_IMAGE_API_VERSION=2
EOF

$ source openrc
```

Set the variables in `env.yml` to reflect you need options:
```yaml
parameters:
  key_name: test
  master_image: ubuntu-k8s-v1.13
  node_image: ubuntu-k8s-v1.13
  master_flavor: m1.medium
  node_flavor: m1.medium
  private_net: private
  public_net: public

```

Now, just execute the following command to create the stack:
```sh
$ openstack stack create k8s -t stack.yml -e env.yml
```
