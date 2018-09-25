# Ansible Role - virsh

VM Deployment using virsh

Available on Ansible Galaxy: [pgkehle.virsh](https://galaxy.ansible.com/pgkehle/virsh)

## Variables
```yaml
deploy_dir:     Required for where the base path lives
```

## Tags

```YAML
tags:
- install
- rename
- create
- storage
```

## Examples

### Example to install the packages 

```YAML
- hosts: all

  vars:
    flags:      ['install']
    
  roles:
    - { role: pgkehle.virsh }
```

### Example to create a vm 

```YAML
- hosts: all

  vars:
    flags:          ['create']
    vm_new:
        name:       'my_vm'
    storage:
      array_num:    0
      size:
        quan:       1
        type:       "T"
      name:         "sdb"
      fs_type:      "xfs"
    variant:        'ubuntu16.04'
    
  roles:
    - { role: pgkehle.virsh }
```

### Example to rename a vm 

```YAML
- hosts: all

  vars:
    flags:          ['rename']
    vm_old:
        name:       'old_vm'
    vm_new:
        name:       'new_vm'
    
  roles:
    - { role: pgkehle.virsh }
```

### Example storage add

```YAML
- hosts: all

  vars:
    flags:          ['storage_add']
    virsh_cfg:
      version:        '16.04.3'
      do_proxy:       true
      img_type:       'img'
      type:           'raw'
      driver:         'qemu'
      format:         'qcow2'
      config:         '--config'

  roles:
    - { role: pgkehle.virsh }
```





## License

MIT

## Author Information

Paul Kehle  
@pgkehle ([twitter](https://twitter.com/pgkehle), [github](https://github.com/pgkehle), [linkedin](https://www.linkedin.com/in/pgkehle))

## For local development testing

```bash
rsync -av --delete ~/code/ansible-virsh/* ~/.ansible/roles/pgkehle.virsh
```

## Reference

* http://xmodulo.com/use-kvm-command-line-debian-ubuntu.html
* http://www.cyberciti.biz/faq/how-to-install-kvm-on-ubuntu-linux-14-04/
* http://serverfault.com/questions/196379/virt-manager-virt-viewer-virtualization-command-line-alternatives
* http://www.tuxradar.com/content/howto-linux-and-windows-virtualization-kvm-and-qemu
* http://manitra.net/how-to-create-a-vm-ubuntu-vmbuilder
* https://blacks3pt3mb3r.wordpress.com/linux-stuffz/264-2/

* KVM/CreateGuests
* https://help.ubuntu.com/community/KVM/CreateGuests

* Default directory: /var/lib/libvirt/
* ISO images for installation: /var/lib/libvirt/boot/
* VM installation directory: /var/lib/libvirt/images/
* Libvirt configuration directory for LVM/LXC/qemu: /etc/libvirt/
*
* virsh for management (debian package libvirt-bin), virt-top for statistics

#### Virsh Commands: 

```bash
# List all servers
virsh list --all
```

```bash
# Edit a server
virsh edit vm_name
```

```bash
# Start a server
virsh start vm_name
```

```bash
# Set server to autostart 
virsh autostart vm_name
```

```bash
# Shutdown a server 
virsh shutdown vm_name
```

```bash
# Reboot a server 
virsh reboot vm_name
```

```bash
# list all domain virtual interfaces 
virsh domiflist 
```

```bash
# Find Name of a server 
virsh dumpxml vm_name | grep '<name>' | cut -d\' -f2
```

```bash
# Find MAC Address of a server 
virsh dumpxml vm_name | grep 'mac address' | cut -d\' -f2
```

```bash
# Find source file for a server 
virsh dumpxml vm_name | grep 'source file' | cut -d\' -f2
```

```bash
# Destroy a server
virsh destroy 1
```

```bash
# create a bridge device and attach an existing network device to it
virsh iface-bridge eno1 br0
```

```bash
# You can also specify --managed-save to delete any managed save images and --snapshots-metadata to remove snapshots for the specified VM.
virsh undefine app-cfg-rs0
virsh dumpxml 1
virsh dumpxml app-worker001
```

```bash
# Virtual Networking
ifconfig virbr0
```

```bash
# Find IP Address of virtual machine
arp -an
ip link show
```

```bash
# Virtual Server DNS Masq
sudo cat /var/lib/libvirt/dnsmasq/default.conf
sudo cat /var/lib/libvirt/dnsmasq/default.leases
```
