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

$ ssh {{HOST_IP}}:2022

```
## Running the Toolkit on Kubernetes

```
$ git clone -b master https://github.com/slarimore02/openstack-toolkit.git

$ kubectl create secret generic ssh-key-secret --from-file=ssh-publickey=/path/to/.ssh/id_rsa.pub

$ kubectl apply -f openstack-toolkit/deployment.yaml

$ kubectl apply -f openstack-toolkit/service.yaml 

$ ssh {{HOST_IP}}:30015

```
