# build_iso
This section covers how to build a customized RHEL system image to be used for provisioning RHEL clusters. We are going to use image builder to build custom ISO for provisioning RHEL nodes.

First thing we will do is to provision an host machine that will act as imagebuilder server. For this POC we will use AWS. Host is already provisioned and up and running with RHEL 9.6 and is also registered with Red Hat.

## Pre-flight steps
Install [this](https://github.com/rprakashg/vpac) ansible collection by running command below

Create an ansible inventory file and add snippet below

```yaml
---
all:
  hosts:
    imagebuilder:
      ansible_host: "<replace>"
      ansible_port: 22
      ansible_user: "<replace>"
      ansible_ssh_private_key_file: "<replace>"
```

Create ansible vault by running command below:

```sh
ansible-vault create vars/secrets.yml
```

The above command will require you to enter a secret for vault and once in editor paste yaml snippet below and replace with values specific to your environment.

```yaml
root_password: '<redacted>'
rh_user: <replace>
rh_user_password: '<redacted>'
admin_user: '<replace>'
admin_user_password: '<redacted>'
admin_user_ssh_key: '<redacted>'
```

Set the vault secret in an environment variable like below

```sh
export VAULT_SECRET=<redacted>
```

```sh
ansible-galaxy collection install git+https://github.com/rprakashg/vpac.git,main
```

Steps to configure host as image builder server is automated in [playbook](../playbooks/setup_imagebuilder.yml). Before we can go ahead and run this playbook as shown in command below

```sh
ansible-playbook -i inventory setup-imagebuilder.yml
```

Once the image builder host is configured we can now run an ansible playbook to build a customized ISO

```sh
ansible-playbook -i inventory --vault-password-file <(echo "$VAULT_SECRET") build_iso.yml -e @vars/vpac-system.yml
```

If everything goes well the playbook will print the path for downloading the ISO from the imagebuilder server. We can now SSH into the image builder server and copy it to a location from where it can be downloaded to provision host systems.





