# QEMU-KVM role

This role install virtualization tools **qemu-kvm** with additional tools (libvirtd, libvirt-client, etc)

## Variables

### General
* `qemu_kvm_packages`: [optional]: list of packages to be installed (see defaults/main.yml for detail)
* `qemu_kvm_use_rhev_version`: [optional, default `true`]: set use or not **virt7-kvm-common-candidate** repo (el7 only)
* `qemu_kvm_remove_default_network`: [optional, default `true`]: delete default qemu-kvm network

### Configure
* `qemu_kvm_libvirtguests_onshutdown`: [optional, default `suspend`, ]: set **ON_SHUTDOWN=** variable (in /etc/sysconfig/libvirt-guests). Possible values: `shutdown` or `suspend`

### Examples
1\. Playbook qemu-kvm.yml`
```yml
- hosts:
    - hostname
  roles:
    - qemu-kvm
```
2\. Install

	ansible-playbook --user=username --become qemu-kvm.yml

3\. Configure (set the variable ON_SHUTDOWN=shutdown)

	ansible-playbook --user=username --become --extra-vars="qemu_kvm_libvirtguests_onshutdown=shutdown" qemu-kvm.yml --tags=libvirt-guests-configure
	
or you can define the variable `qemu_kvm_libvirtguests_onshutdown: "shutdown"` in `host_vars\hostname`

### NOTE
After changing the value **ON_SHUTDOWN** in /etc/sysconfig/libvirt-guests, the **libvirt-guests service** is **NOT** restarted automatically (otherwise all VM will be shutdown or suspended).

#### License

GPLv3 license

#### Author Information

Vitaly Yakovenko
