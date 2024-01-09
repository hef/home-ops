
# Initial formate of drives

* Flash drive with Etcher: ubuntu preinstalled server arm64

````bash
mount /dev/disk/by-label/system-boot /mnt/boot
mount /dev/disk/by-label/writable /mnt/writable
sudo curl https://raw.githubusercontent.com/TheRemote/Ubuntu-Server-raspi4-unofficial/master/BootFix.sh | sudo bash
umount /mnt/boot
umount /mnt/writable
echo ", 32G" | sudo sfdisk /dev/sdb -N2
sync
echo ", +" | sudo sfdisk /dev/sdb -N3
sudo e2fsck -f  /dev/sdb2
sudo resize2fs /dev/sdb2
sudo wipefs -a /dev/sdb3
````

todo: add `cgroup_memory=1 cgroup_enable=memory`  to the end of /mnt/boot/firmware/cmdline.txt


# installing cluster

```
task ansible:playbook:ubuntu-prepare
task ansible:playbook:ubuntu-upgrade
task cluster:bootstrap
```

# adding a node
 * install ubuntu server
 * add an entry to provision/ansible/inventory/hosts.yml
 * add some values to provision/ansible/inventory/host_vars/*node-name*.sops.yml.
   * `ansible_user` and `ansible_become_pass`
 * run `task ansible:playbook:ubuntu-prepare`
 * run `task ansible:playbook:k3s-install`

# references

*  https://github.com/onedr0p/flux-cluster-template
