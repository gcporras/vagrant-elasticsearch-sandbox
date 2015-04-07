# vagrant-elasticsearch-sandbox
Installs an elasticsearch server with nginx as the proxy

## Coding Style
The coding style of this project is defined in the .editorconfig file. For more information see
[EditorConfig.org](http://editorconfig.org/)

## Requirements
- Pyton 2.7.5
- virtualenv or virtualenvwrapper (optional)
- [ansible](http://docs.ansible.com/intro_installation.html) > 1.8.1. It can be installed running:
 ```shell
 pip install -r ansible/requirements.txt
 ```
- [vagrant](http://www.vagrantup.com) 1.6.3
- [virtualbox](https://www.virtualbox.org/wiki/Downloads) 4.3.12

## Vagrant configuration file

Here is the list of all variables and their default values. You can override these settings by redefining them on a
file named `vagrantconfig_local.yml`:
```yaml
memory: 2048                      # The amount of memory allocated for the VM
cpus: 2                           # The number of CPUs allocated for the VM
network_ip: "192.168.33.21"       # The ip assigned to the VM
```

## Installation instructions

### 1. Install vagrant [vagrant-hostsupdater](https://github.com/cogitatio/vagrant-hostsupdater) plugin:

```shell
vagrant plugin install vagrant-hostsupdater
```

### 2. Install ansible-galaxy roles:

```shell
ansible-galaxy install -r ansible/requirements.yml
```

### 3. Provision with vagrant

```shell
vagrant up
```
