# single machine
* read README.md first, because some of the html guide might be out of sync with the code.
* https://docs.openstack.org/developer/devstack/guides/single-machine.html
  ```
  # useradd -s /bin/bash -d /opt/stack -m stack
  # apt-get install sudo -y || yum install -y sudo
  # echo "stack ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
  # su stack
  $ cd
  $ git clone https://git.openstack.org/openstack-dev/devstack
  $ cd devstack
  $ create local.conf (e.g. from samples/local.conf, or devstack.git/opt/stack/devstack/local.conf)
  $ ./stack.sh
  ```
* fixes
  * can also use this to create use: devstack/tools/create-stack-user.sh (maybe used as a after-art check)
  * mkdir ~/.cache, or have to sudo chmod -R +rwx .cache, otherwise it has permission issues.
  * static ip address - after changing /etc/network/interfaces (e.g. devstack.git/etc/network/interfaces), need to run these
    ```
    ifdown enp0s3
    ip addr flush dev enp0s3
    ifup enp0s3
    ```
* problems and solutions
  * can not install
    * sudo apt install xxx
  * manage.py not found in lib/horizon: 
     * export PYTHON=/usr/bin/python  # add this line before the following line
     * (cd $HORIZON_DIR; $PYTHON manage.py compilemessages)  # e.g. line 84
  * init_placement
    * skip it
* other docs:
  * http://www.techrepublic.com/article/how-to-install-openstack-on-a-single-ubuntu-server-virtual-machine/
  
# behind a proxy
* inc/python
  * function pip_install
    * sudo_pip http_proxy=  # e.g. line 337, need to setup the proxy again. (or setup root proxy)
* potential certificate problem with the proxy:
  * lib/etcd3: wget --no-check-certificate 
