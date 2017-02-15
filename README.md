# Ansible: virsh

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
```

## Examples

### Example to rename a vm 

```YAML
- hosts: all

  vars:
    do_rename:      true
    vm_name_old:    'old_vm' 
    vm_name_new:    'new_vm'
    
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
rsync -av ~/code/ansible-virsh/* ~/.ansible/roles/pgkehle.virsh
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
