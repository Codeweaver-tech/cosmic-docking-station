# Repository configuration

In order to setup the nvidia-docker repository for your distribution, follow the instructions below.

If you feel something is missing or requires additional information, please let us know by [filing a new issue](https://github.com/NVIDIA/nvidia-docker/issues/new).

List of supported distributions:

|  OS Name / Version   |  Identifier | amd64 / x86_64 | ppc64le | arm64 / aarch64 |
| -------------------- | :---------: | :------------: | :-----: | :-------------: |
| Amazon Linux 1       | amzn1       | :heavy_check_mark: |         |                 |
| Amazon Linux 2       | amzn2       | :heavy_check_mark: |         |                 |
| Amazon Linux 2017.09 | amzn2017.09 | :heavy_check_mark: |         |                 |
| Amazon Linux 2018.03 | amzn2018.03 | :heavy_check_mark: |         |                 |
| Open Suse Leap 15.0  | sles15.0    | :heavy_check_mark: |         |                 |
| Open Suse Leap 15.1  | sles15.1    | :heavy_check_mark: |         |                 |
| Debian Linux 9       | debian9     | :heavy_check_mark: |         |                 |
| Debian Linux 10      | debian10    | :heavy_check_mark: |         |                 |
| Centos 7             | centos7     | :heavy_check_mark: | :heavy_check_mark: |                 |
| Centos 8             | centos8     | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| RHEL 7.4             | rhel7.4     | :heavy_check_mark: | :heavy_check_mark: |                 |
| RHEL 7.5             | rhel7.5     | :heavy_check_mark: | :heavy_check_mark: |                 |
| RHEL 7.6             | rhel7.6     | :heavy_check_mark: | :heavy_check_mark: |                 |
| RHEL 7.7             | rhel7.7     | :heavy_check_mark: | :heavy_check_mark: |                 |
| RHEL 8.0             | rhel8.0     | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| RHEL 8.1             | rhel8.1     | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| RHEL 8.2             | rhel8.2     | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Ubuntu 16.04         | ubuntu16.04 | :heavy_check_mark: | :heavy_check_mark: |                 |
| Ubuntu 18.04         | ubuntu18.04 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Ubuntu 19.04         | ubuntu19.04 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Ubuntu 19.10         | ubuntu19.10 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Ubuntu 20.04         | ubuntu20.04 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |

## Debian-based distributions

```bash
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update
```

## RHEL-based distributions

```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.repo | \
  sudo tee /etc/yum.repos.d/nvidia-docker.repo
```

# Updating repository keys

In order to update the nvidia-docker repository key for your distribution, follow the instructions below.

## RHEL-based distributions 

```bash
$ DIST=$(sed -n 's/releasever=//p' /etc/yum.conf)
$ DIST=${DIST:-$(. /etc/os-release; echo $VERSION_ID)}
$ sudo rpm -e gpg-pubkey-f796ecb0
$ sudo gpg --homedir /var/lib/yum/repos/$(uname -m)/$DIST/*/gpgdir --delete-key f796ecb0
$ sudo gpg --homedir /var/lib/yum/repos/$(uname -m)/latest/nvidia-docker/gpgdir --delete-key f796ecb0
$ sudo gpg --homedir /var/lib/yum/repos/$(uname -m)/latest/nvidia-container-runtime/gpgdir --delete-key f796ecb0
$ sudo gpg --homedir /var/lib/yum/repos/$(uname -m)/latest/libnvidia-container/gpgdir --delete-key f796ecb0
$ sudo yum update
```

# Amazon Linux (1 and 2)

Be careful to run each instruction one by one!

```bash
$ sudo gpg --homedir /var/lib/yum/repos/$(uname -m)/*/nvidia-docker/gpgdir --delete-key f796ecb0
$ sudo gpg --homedir /var/lib/yum/repos/$(uname -m)/*/nvidia-container-runtime/gpgdir --delete-key f796ecb0
$ sudo gpg --homedir /var/lib/yum/repos/$(uname -m)/*/libnvidia-container/gpgdir --delete-key f796ecb0
$ sudo yum update
```

## Debian-based distributions
```bash
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
```
