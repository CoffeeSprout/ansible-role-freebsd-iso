coffeesprout.freebsd-iso
=========

This role creates an installable iso file that includes a custom /etc/installerconfig for automated install.
You can also define your own installerconfig
Combine this whatever process you have to start VM's, for example on Proxmox


Requirements
------------

This role supports two methods for creating the ISO
1. Installing growisofs and adding a session containing the installerconfig
2. Mounting the ISO, syncing the folders and adding the installerconfig

Personally I prefer 1 as it requires less temporary storage, doesn't require me to think about mounting and umounting files etc.
Method 2 is currently untested.

This whole thing is a work in progres. Here be dragons.

Role Variables
--------------

See the defaults/main.yml but here is a small selection of things that make sense to change

    freebsd_iso_name: "custom"

If you need to create multiple iso's it makes sense to give them unique names. Example use the VM name of the resulting machine.

    iso_workdir: "{{ playbook_dir }}/files/isos"

By default store the results on the controller; But if you are running remotely say against a proxmox machine it might make sense to use the path where the ISO's end up being stored, for example /var/lib/vz/template/iso/ or a shared version of that

There is also a more advanced installerconfig that has it's own veriables, too many to list here.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: proxmox-machine
      roles:
      - role: coffeesprout.freebsd-iso
        iso_workdir: "/var/lib/vz/template/iso/"
        freebsd_iso_installerconfig: "installerconfig.vagrant.j2"

License
-------

BSD

Author Information
------------------

Just reach out via Github
