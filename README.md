# openstack-toolkit
The Openstack Toolkit has all of the packages necessary to manage an Openstack cloud. The container includes a SSHD server for connecting to the toolkit remotely with a SSH key pair. 

## Tools included

- python-openstackclient
- mariadb-client
- python-glanceclient
- python-ironicclient
- python-manilaclient
- python-novaclient
- python-neutronclient
- python-swiftclient
- python-barbicanclient
- python-cinderclient
- python-ceilometerclient
- python-heatclient
- python-troveclient

## Running the Toolkit on Docker

```
$ sudo docker run -d -e PUBLIC_KEY={{public-key}} -e OS_AUTH_URL={{os-auth-url}} -e OS_REGION_NAME={{region-name}} \
-e OS_PROJECT_DOMAIN_NAME={{project-domain-name}} -e OS_PROJECT_NAME={{project-name}} -e OS_USER_DOMAIN_NAME={{user-domain-name}} \
-e OS_USERNAME={{username}} -e OS_PASSWORD={{password}} -e OS_IDENTITY_API_VERSION=3 -e OS_IMAGE_API_VERSION=2 \
-p 2022:22 slarimore02/openstack-toolkit:latest

$ ssh {{HOST_IP}} -p 2022

```
## Running the Toolkit on Kubernetes

Complete the following to run the toolkit on an existing Kubernetes cluster.

```
$ git clone -b master https://github.com/slarimore02/openstack-toolkit.git

$ kubectl create secret generic ssh-key-secret --from-file=ssh-publickey=/path/to/.ssh/id_rsa.pub

$ kubectl apply -f openstack-toolkit/deployment.yaml

$ kubectl apply -f openstack-toolkit/service.yaml 

$ ssh {{HOST_IP}} -p 30015

```

## Running the Toolkit with Openstack-Helm

Complete the following to deploy the Toolkit using Helm. A working Openstack-Helm deployment is a prerequisite for this chart. 

Clone the openstack-helm-addons repo and checkout the openstack-toolkit branch:

```
$ git clone https://github.com/slarimore02/openstack-helm-addons.git
$ cd openstack-helm-addons
$ git checkout openstack-toolkit
```
Install the openstack-toolkit chart

```
$ helm install --name=openstack-toolkit local/openstack-toolkit --namespace openstack --set=secrets.authorizedkeys={{public-key}}
$ ssh {{HOST_IP}} -p 31022
$ source openrc/openrc
```
