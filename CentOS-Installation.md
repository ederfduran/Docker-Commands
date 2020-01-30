# CentOS Commands

### Prerequisites
* Unistall old versions:
```sh
sudo yum remove -y docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

### Install Docker CE
* Add the Utilities needed for Docker:
```sh
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

* Set up the stable repository:
```sh
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

* Install Docker CE:
```sh
    sudo yum -y install docker-ce
```

* Enable and start Docker:
```sh
    sudo systemctl start docker && sudo systemctl enable docker
```

* Add user to the docker group:
```sh
    sudo usermod -aG docker cloud_user
```

