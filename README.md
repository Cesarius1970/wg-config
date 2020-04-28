This is a simple wireguard VPN user management script using on VPN server.
Client config file and qrcode are generated.

### dependency

* wireguard
* qrencode

### config
The wireguard default config directory is /etc/wireguard.

The script config file is "wg-config.def", create and edit it according to "wg-config.def.sample". 
Copy client.conf.tpl.sample to client.conf.tpl and copy server.conf.tpl.sample to server.conf.tpl. Edit "tpl"files if you want to change some config.

You can generate the public key and private key with command `wg genkey | tee prikey | wg pubkey > pubkey`.

### usage

Running as root. (mandatory)
This script creates the "users" directory where youd cloned this repo.

#### init wireguard server

```bash
./wg-config.sh -i
```
This will init the server configuration (from server.conf.tpl) and support files. Creates wg0.conf file under /etc/wireguard

#### add a user

```bash
./wg-config.sh -a alice
```
This will generate a client conf and qrcode in users directory which name is alice
and add alice to the wg server config.

This will disable default route change. Route traffic Manually.

```bash
./wg-config.sh -a alice -r
```
client will route all traffic to server.

#### delete a user

```bash
./wg-config.sh -d alice
```
This will delete the alice directory and delete alice from the wg server config.

#### clear all

```bash
./wg-config.sh -c
```
Delete all users before clear.
