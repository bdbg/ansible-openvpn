# ansible-openvpn

OpenVPN setup with Ansible. Based on

https://www.digitalocean.com/community/tutorials/how-to-set-up-and-configure-a-certificate-authority-on-ubuntu-22-04

https://www.digitalocean.com/community/tutorials/how-to-set-up-and-configure-an-openvpn-server-on-ubuntu-22-04

## Prerequisites

This playbook assumes that CA server and OpenVPN server are different remote machines, which involves file transfers between them. In order for this to work both CA and OpenVPN servers should have SSH keys generated (without passphrase) with the public keys added to each other's `authorized_keys` file.

Having CA and OpenVPN servers hosted on the same machine is also supported via specifying the same host for both in the `hosts.yml`. But in order for this to this to work a SSH key should be generated (without passphrase) on this machine with the public key added to it's own `authorized_keys` file.
```
ssh-keygen -C "$(whoami)@$(hostname)"
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

## Dependencies

Tested with the following versions:
- ansible 2.16.7
- ubuntu 22.04
- openvpn 2.5.9
- openssl 3.0.2
- easyrsa 3.0.8

## Usage

1. `cp hosts.example.yml hosts.yml` and configure it by specifying actual data for hosts and clients
2. run `ansible-playbook playbook.yml`
3. `*.ovpn` files for each specified client will be downloaded into the current directory
4. import `.ovpn` file into a OpenVPN client
