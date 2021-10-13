# Demonstration script to deploy Citrix ADC VPX via Ansible
This Ansible playbook is a proof of concept how to deploy and integrate a [Citrix ADC](https://www.citrix.com/products/citrix-adc/) into an existing environment.

# Flow
The Flow looks like this
1. deployment of VPX out of an existing VM Template
2. initial password change
3. configuring some basic stuff
4. adding ADC instance to [ADM Service](adm.cloud.com)
5. allocate bandwidth license to instance by using pooled licensing
6. copy Files to instance (e.g. SSL certificates) 

# Prerequisites
1. [install Citrix ADC and ADM ansible modules](https://netscaler-ansible.readthedocs.io/en/latest/usage/getting_started.html)
2. replace `citrix_adm.py` in your installation (mostly `/home/<user>/.ansible/collections/ansible_collections/citrix/adm/plugins/module_utils/citrix_adm.py`) with the [modified one of this repo](deps/citrix_adm.py). This is necessary because of a bug in Cloud connect with the original one, Citrix engineering is already aware of that and it will be fixed in future release.
3. change the [variable files](vars)
4. start playbook with `ansible-playbook -e "@vars/<your-vpx-variables>"`
5. Have Fun.

# Variables files
- xen.yml: credentials needed to access the Hypervisor for deploying VPX from template. 
- CitrixCloud.yml: Use [example file](vars/CitrixCloudExample.yml) for building. You need to create API credentials in your Citrix Cloud Account. [Howto](https://developer.cloud.com/app-delivery-and-security/citrix-application-delivery-management-service/login/docs/getting-started)
- vpx_*.yml: in this files you can specify the ADC template (to deploy from), IPs, credentials. The file has to be specified in the `ansible-playbook` command

# Links
Links for references:
- [Citrix ADC Ansible Module Documentation](https://developer-docs.citrix.com/projects/netscaler-ansible-modules/en/latest/)
- [Citrix Application Delivery Management Service API reference](https://developer.cloud.com/app-delivery-and-security/citrix-application-delivery-management-service)
- [Citrix Cloud API Introduction](https://developer.cloud.com/citrix-cloud/citrix-cloud-api-overview/docs/get-started-with-citrix-cloud-apis)
