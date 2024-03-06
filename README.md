## Overview

This repository contains Ansible playbook, which might be used for building Ember-optimized Amazon machine images (AMI). For more information about Ember see the [official documentation](https://ember.deltixlab.com/).

Supported target OS are:
 - Amazon Linux 2
 - Amazon Linux 2023
 - Rocky Linux 9
 - RHEL 8

What will the playbook do:
 - Rebuild and install current kernel with CONFIG_NO_HZ_FULL parameter (Amazon Linux only);
 - Set boot parameters to disable certain C-states, isolate particular CPU cores from the scheduler and disable particular security features which may bring additional latency (like auditing, selinux and mitigations);
 - Disable unused system services;
 - Set proper tuned profile. 

## Usage 

The playbook might be used for manual local execution, as well as for automated image building with the tools like AWS Image Builder or Hashicorp Packer. Target host should have Ansible 2.9+ installed. 

To run the playbook use the following command:
```bash
ansible-playbook main.yml
```

### Important notes

1. The playbook configures CPU cores isolation. The default values are optimized for c6i.12xlarge instance type and might be not suitable for your setup. This might be overridden by passing your own values via ```kernel_boot_params``` variable:

```bash
ansible-playbook main.yml -e kernel_boot_params=YOUR_BOOT_PARAMETERS_HERE
```

2. If you're running RHEL, make sure that you have *ansible* packages installed (if available) or install *ansible.posix* collection manually:
```bash
ansible-galaxy collection install ansible.posix
```

3. The playbook disables unused services. The definition of *unused* may vary for different deployments. Please make sure, that any important services are not being disabled. 