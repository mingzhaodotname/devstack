# single machine
* read README.md first, because some of the html guide might be out of sync with the code.
* https://docs.openstack.org/developer/devstack/guides/single-machine.html
* http://www.techrepublic.com/article/how-to-install-openstack-on-a-single-ubuntu-server-virtual-machine/
* fixes
  * can also use this to create use: devstack/tools/create-stack-user.sh (maybe used as a after-art check)
  * have to sudo chmod -R +rwx .cache, otherwise it has permission issues.
  * static ip address - after changing /etc/network/interfaces, need to run these
    ```
    ifdown enp0s3
    ip addr flush dev enp0s3
    ifup enp0s3
    ```
