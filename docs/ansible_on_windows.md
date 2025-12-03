# Install Ansible on Windows 
This section walks through how to install Ansible on Windows

## Install WSL
Install Windows Subsytem for Linux

```sh
wsl --install

```

Run `wsl` and create a new user and update installed packages as shown in commands below.

```sh
sudo apt update
sudo apt upgrade -y
```

## Install Ansible
We are now ready to install ansible. Run command below to install Ansible

```sh
sudo apt install -y ansible
```

## Verify ansible is installed
We can now verify that Ansible is installed by running command below

```sh
ansible --version
```