# Puppet-agent installation on lxc and agnet configuration

Puppet-agent installed on lxc container

os release :-NAME="Ubuntu"
VERSION="20.04.6 LTS (Focal Fossa)"

First update the apt packages lists :-

```bash
apt-get update 
```

Than eanble the ubuntu repository E.g.:-
```bash
wget https://apt.puppet.com/puppet7-release-focal.deb
sudo dpkg -i puppet7-release-focal.deb
```

Again update the apt packages lists :-

```bash
apt-get update 
```

Now install the puppet agent on lxc container with command as below :

```bash
apt-get install puppet-agent 
```

You can source a script that puppet-agent installs. Run the following command:

```bash
source /etc/profile.d/puppet-agent.sh

export PATH=/opt/puppetlabs/bin:$PATH
```
