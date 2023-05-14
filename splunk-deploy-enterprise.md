# SPLUNK-DEPLOY-ENTERPRISE

Download Ubuntu, or other Linux flavor of your choice with the Container Template Download Utility

### Download linux container

1. click local (pvex) - (where x denotes the node id)
2. click CT Templates in column to the right
3. click Templates at the top
4. search for linux flavor of your choice
5. select LXC container you wish to download
6. click Download

### Create Container

1. right click node, pvex (where x denotes the node id)
2. in the dropdown menu that pops up click Create CT
3. General Tab
   * CT ID = 200
   * hostname = ub-splunk-enterprise
   * Password = \<complex password>
   * Confirm password = \<complex password>
   * Optionally add your public SSH Key File by clicking 'Load SSH Key File', locating it in local directory of the machine you wish to tunnel from to access container
   * Click Next
4. Template
   * Template dropdown -> linux distro
5. Disks
   * Disk size (GiB) = 30
   * NOTE: Depending on available hard drive space you may want to select either less or more
   * Click Next
6. CPU
   * Cores = 1
   * NOTE: Depending on total number of cores on host you may want to select either less or more
   * Click Next
7. Memory
   * Memory = 2048
   * Swap = 2048
   * Click Next
8. Network
   * Name = \<default>
   * Bridge = vmbro (or another port)
   * IPv4 = 192.168.55.200/24
   * Gateway (IPv4) = 192.168.55.1
   * NOTE: I am setting all of my splunk servers on the same subnet for now
   * Click Next
9. DNS
   * DNS domain = use host settings
   * DNS servers = use host settings
   * Click Next
10. Confirm
    * Click Finish
    * Task viewer will pop up, TASK OK at bottom means the container was created successfully&#x20;
    * close Task viewer by clicking x in top right of pop up

### Log in to Console

* On the left under the node, pvex (where x denotes the node id), right click the container you just created and click Start from the drop down
* A green triangle will appear indicating the Container has started
* Click Console in the colum to the right of the Datacenter menu
* You will be prompted to login which is, root.
* Press enter after you enter login, and then type the password you created before.
* Update linux - if you are running ubuntu you can use the following command:

```
/apt update && apt upgrade -y
```

* Wait for update and upgrade to finish, then enter the following command
* NOTE: it is possible that this package will be deprecated, or they move the link elsewhere, in that case you will need to replace the url with a valid one.

### Download, unpack, and start the Splunk Enterprise Server

```
wget -O splunk-9.0.4.1-419ad9369127-Linux-x86_64.tgz "https://download.splunk.com/products/splunk/releases/9.0.4.1/linux/splunk-9.0.4.1-419ad9369127-Linux-x86_64.tgz"
```

Move the tarball to the /opt directory

```
mv splunk-9.0.4.1-419ad9369127-Linux-x86_64.tgz /opt
```

Change Directory

```
cd /opt
```

Unpack the tarball

tar -xzvf splunk-9.0.4.1-419ad9369127-Linux-x86\_64.tgz

Change Directory

```
cd splunk/bin
```

Start the Splunk server and accept the license

```
./splunk start --accept-license
```

You will be asked to enter credential that you will use to login to the server after running the command above. Pick something you like and wait till the server is done loading

### Login to the Web Interface

In a web browser, enter in the IP address of the container. in my case I will type in 192.168.55.200:8000 to the address bar and hit enter

The login page will load.

Now enter the credentials you created

Voila - you should be good to go
