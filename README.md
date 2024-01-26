## Overview

This repository contains Ansible playbook, which might be used for building Ember-optimized Amazon machine images (AMI). For more information about Ember see the [official documentation](https://ember.deltixlab.com/).

Supported target OS are:
 - Amazon Linux 2
 - Amazon Linux 2023
 - Rocky Linux 9

## Usage 

The playbook might be used for manual local execution, as well as for automated image building with the tools like AWS Image Builder or Hashicorp Packer. Target host should have Ansible 2.9+ installed. 

To run the playbook use the following command:
```bash
ansbile-playbook main.yml
```

**Note:** the playbook configures CPU cores isolation. The default values are optimized for c6i.12xlarge instance type and might be not suitable for your setup. This might be overridden by passing your own values via ```kernel_boot_params``` variable:

```bash
ansible-playbook main.yml -e kernel_boot_params=YOUR_BOOT_PARAMETERS_HERE
```