# Introduction

- Puppet is an open-source,automation admin engine used to perform admin tasks
- Server management remotely. This tool is available on Linux, Unix, and Windows.

**- we will install the Puppet on Ubuntu 20.04 on master and client nodes.**

## Prerequisites

- Minimum two system running Ubuntu 20.04
- Access to an account with sudo privileges

### Step 1:-update Package list

Before you start the installation process, update the list of available packages:

```bash
sudo apt-get update -y
```

#### Step 2:-Hostname Resolution

With Puppet, master and client nodes communicate using hostnames.
Before installing Puppet, you need to set up a unique hostname on each node.

## Use set-hostname to Change the Hostname on each node

```bash
hostnamectl set-hostname new-hostname
```

1. Open the **hosts** file on each node by using:

```bash
sudo vi /etc/hosts
```

**Note :-** you can use any editor.

1.1 Paste the following lines at the end of each **hosts** file:

```bash
[puppet master ip] puppetmaster puppet
[puppet client ip] puppetclient
```

where:

- **[puppet master ip]** is the IP address of the master node,
- **[puppet client ip]** is the IP address of the client node.
  
1.2 Press **Esc**, and then **:wq!** to save and close the file.

## Step 3:-Install Puppet Server on Master Node

1. Download the latest Puppet version on the master node:

```bash
wget https://apt.puppetlabs.com/puppet6-release-focal.deb
```
  
1.2 Once the download is complete, install the package by using:

```bash
sudo dpkg -i puppet6-release-focal.deb
```

1.3 Update the package repository:

```bash
sudo apt-get update -y
```
  
1.4 Install the Puppet server with the following command:

```bash
sudo apt-get install puppetserver -y
```
  
1.5 Open the **puppetserver** file by using :

```bash
sudo vi /etc/default/puppetserver
```
  
1.6 In the server file, modify the below line to change the memory size to 1GB:

```bash
# change this line no.9 as below:
JAVA_ARGS="-Xms1g -Xmx1g -Djruby.logger.class=com.puppetlabs.jruby_utils.jruby.Slf4jLogger"
```
  
1.7 Press **Esc**, and then **:wq!** to save and close the file.
  
1.8. Start the Puppet service and set it to launch on system boot by using:

```bash
sudo systemctl start puppetserver
sudo systemctl enable puppetserver
```
  
1.9 Check if the Puppet service is running with:

```bash
sudo systemctl status puppetserver
```

## Step 4: Install Puppet Agent on Client Node

1. Download the latest version of Puppet on a client node:

```bash
wget https://apt.puppetlabs.com/puppet6-release-focal.deb
```
  
1.2 Once the download is complete, install the package by using:

```bash
sudo dpkg -i puppet6-release-focal.deb
```

1.3 Update the package repository one more time:

```bash
sudo apt-get update -y
```

 1.4 Install the Puppet agent by using:

```bash
sudo apt-get install puppet-agent -y
```
  
1.5 pen the Puppet configuration file:

```bash
sudo vi /etc/puppetlabs/puppet/puppet.conf
```
  
1.6 Add the following lines to the end of the Puppet configuration file
    define the Puppet master information:

```bash
[main]
certname = puppetclient
server = puppetmaster
```

1.7 Start the Puppet service and set it to launch on system boot by using:

```bash
sudo systemctl start puppet
sudo systemctl enable puppet
```

1.8 Check if the Puppet service is running with:

```bash
sudo systemctl status puppet
```

## Step 5:-Sign Puppet Agent Certificate

1. Using the Puppet master node, list all the available certificates:

```bash
sudo /opt/puppetlabs/bin/puppetserver ca list --all
```

1.2 Sign the certificates with:

```bash
sudo /opt/puppetlabs/bin/puppetserver ca sign --all
```

1.3 we will test the communication between the master and agent from agent node:

```bash
puppet agent -t
```
