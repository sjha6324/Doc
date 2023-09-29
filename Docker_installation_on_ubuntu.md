# Docker installation on ubuntu

- First, update existing packages:

```bash
sudo apt update
```

- install a few prerequisite packages which let apt use packages over HTTPS:


```bash 
sudo apt install apt-transport-https ca-certificates curl software-properties-common
bash 

- Then add the GPG key for the official Docker repository to your system:

```bash 
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

- **Add the Docker repository to APT sources:**
```bash 
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

- Update existing list of package again 

```bash 
$ sudo apt update
```

- **Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:**

```bash 
$ apt-cache policy docker-ce
```

- **Install Docker:**

```bash 
$ sudo apt install docker-ce
```

> Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:

```bash 
$ sudo systemctl status docker
```

