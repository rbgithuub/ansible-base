Role Name
=========

Common base role for all hosts. Should be ran after mrlesmithjr.bootstrap role.
(Configure apt-cacher,update dhcp client,update dns servers,configure lvm)

Requirements
------------

If creating, resizing or creating LVM volumes/volume groups ensure that you define the correct current disk and the new disk(s) added. If you choose to use apt-cacher ensure that you already have a server built and configured correctly for apt-caching.

Role Variables
--------------

````
config_lvm: false  #defines if lvm should be configured when adding additional disks...should be defined in host_vars/host
create_lvm: false  #defines if lvm should be created when adding additional disks...should be defined in host_vars/host (do not set extend or resize to true)
create_lvname: test-lv  #define lvm name when adding additional disks...should be defined in host_vars/host
create_lvsize: 100%FREE  #defines the lvm lv size --- (10G) - would create new lvm with 10Gigabytes -- (512) - would create new lvm with 512m
create_vgname: test-vg  #defines the lvm vg name to create...
current_disk: /dev/sda5  #defines the disk currently configured for lvm...should be defined in host_vars/host
extend: false  #defines if lvm vg should be extended (do not set create to true)...should be defined in host_vars/host
extend_disks: '{{ current_disk }},{{ new_disk }}'  #defines the disks to extend in lvm group...should be defined in host_vars/host
extend_lvname: test-lv  #defines the lvm lv name to extend...should be defined in host_vars/host
extend_vgname: test-vg  #defines the lvm vg name to extend...should be defined in host_vars/host
filesystem: ext4  #defines the filesystem type to create when configuring lvm ( ext3, ext4, xfs, etc. )...should be defined in host_vars/host
lvextend_options: '-L+10G'  #defines the options to pass to lvextend --- ('-L+10G') - would increase by 10GB whereas ('-l +100%FREE') would increase to full capacity
new_disk: /dev/sdb  #defines the new disk being added to volume group...should be defined in host_vars/host
new_mntp: /mnt/test  #defines the desired mount point to be created and new logical volume to be mounted to...should be defined in host_vars/host
resize: false  #set to true if resizing the logical volume (do not set create to true)...should be defined in host_vars/host
resize_lvname: test-lv  #defines the logical volume name to resize...should be defined in host_vars/host
resize_vgname: test-vg  #defines the volume group name to resize...should be defined in host_vars/host
update_dhcpclient_conf: false  #defines if dhcp client config should be updated...define here or globally in group_vars/all/configs
update_dns_nameservers: false  #defines if dns servers should be updated...define here or globally in group_vars/all/configs
update_dns_search: false  #defines if dns search domain should be updated...define here or globally in group_vars/all/configs
update_etc_hosts: false  #defines if /etc/hosts should be updated...define here or globally in group_vars/all/configs
````

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: mrlesmithjr.base }

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
