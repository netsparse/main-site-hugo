---
layout: post
author: Angel
date: 2023-03-10
title: Setup WireGuard VPN Server with Ubiquiti Edgerouter X (EdgeOS)
description:
tag: ["vpn, wireguard", "networking", "routers", "linux"] 
category: blog
excerpt_separator: <!--more-->
## end of jekyll ##

showToc: true
TocOpen: false
hidemeta: false
comments: true
#canonicalURL: "https://canonical.url/to/page"
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: false
---

[WireGuard](https://www.wireguard.com/) is a fast and secure VPN protocol that uses state-of-the-art cryptography. It is designed to be easy to implement and manage, and has a minimal attack surface. Its simplicity and efficiency make it well-suited for use in mobile devices and large-scale deployments.

**Note: Before making any major changes on your EdgeOS router, always make a backup.**
Refer to the [official documentation](https://help.ui.com/hc/en-us/articles/360002535514-EdgeRouter-Backup-and-Restore-Configuration) on how to perform one.

# Breakdown

## Step 1. Installation
**Note: The following installation guide was verified working on EdgeOS v2.0.9-hotfix.4 as of Feb 2023.**

### Verify your EdgeOS version
```bash
show version
```

### Download Wireguard
Head over to [WireGuard's EdgeOS releases](https://github.com/WireGuard/wireguard-vyatta-ubnt/releases/) and look for the `release` that matches your platform/version.

**On the ER-X, use `curl` to download the `.deb` file**
```bash
curl -OL https://github.com/WireGuard/wireguard-vyatta-ubnt/releases/download/1.0.20220627-1/e50-v2-v1.0.20220627-v1.0.20210914.deb
```

### Install with dpkg
```bash
sudo dpkg -i e50-v2-v1.0.20220627-v1.0.20210914.deb
```

Output Log
```bash
user@ER-X:~$ sudo dpkg -i e50-v2-v1.0.20220627-v1.0.20210914.deb
Selecting previously unselected package wireguard.
(Reading database ... 37091 files and directories currently installed.)
Preparing to unpack e50-v2-v1.0.20220627-v1.0.20210914.deb ...
Adding 'diversion of /opt/vyatta/share/perl5/Vyatta/Interface.pm to /opt/vyatta/share/perl5/Vyatta/Interface.pm.vyatta by wireguard'
Adding 'diversion of /opt/vyatta/share/vyatta-cfg/templates/firewall/options/mss-clamp/interface-type/node.def to /opt/vyatta/share/vyatta-cfg/templates/firewall/options/mss-clamp/interface-type/node.def.vyatta by wireguard'
Adding 'diversion of /opt/vyatta/share/vyatta-cfg/templates/firewall/options/mss-clamp6/interface-type/node.def to /opt/vyatta/share/vyatta-cfg/templates/firewall/options/mss-clamp6/interface-type/node.def.vyatta by wireguard'
Unpacking wireguard (1.0.20220627-1) ...
Setting up wireguard (1.0.20220627-1) ...
```

### If there is no space available
If additional storage space is needed, you can safely delete the **backup** system image (not the currently running firmware).
```bash
delete system image
```

You can check if wireguard is installed by running: 
```bash
wg version
```

Output log:
```bash
user@ER-X:~$ wg version
wireguard-tools v1.0.20210914 - https://git.zx2c4.com/wireguard-tools/
```

## Step 2. Key Creation

**Confirm working directory**
```
pwd
```

### Generate Server Keys

**Create folder for your server keys**
You can create it in the `/config` directory to preserve your files during upgrades, and to make it easier during backups.
```
cd /config
```

**Create a folder `wireguard`, then create another folder for `server_keys`**
```
mkdir wireguard; cd wireguard
mkdir server_keys; cd server_keys
```

**Generate a key pair for the Wireguard server**
```
wg genkey | tee privatekey | wg pubkey > publickey
```

**Note your public and private key for the next configuration steps.**
```
cat publickey privatekey
```

### Generate Client Keys

**Move to `wireguard` directory.**

```
cd /config/wireguard
```

**Create folder `wg_clients`**
```
mkdir wg_clients ; cd wg_clients
```

**Create folder for `client01`**
```
mkdir client01 ; cd client01
```

**Generate client keys.**
```
wg genkey | tee privatekey | wg pubkey > publickey
```

**Note your public and private key for the next configuration steps.**
```
cat publickey privatekey
```
Example output:
```
user@ER-X:~$ cat privatekey publickey 
sAoqK3dXpc2UbOn2LWb/MMcHTKtU0nqHjDQiXqNcyHs=
Bf6LBfuoRDRbO4EJ+tawJXu6qu5BOWaXGK0V+uVRC3Q=
```

## Step 3. wg0 Interface Configuration

**Enter `configure` mode**
```
configure
```

**Set the location of the server's `private-key`, previously generated**
```
set interfaces wireguard wg0 private-key <server-private-key-here>
```

**Create the Gateway IP for the VPN and the subnet**
This subnet can be any private IP range, though make sure to check for conflicts 
```
set interfaces wireguard wg0 address 10.0.0.1/32
```

**Create entries in the route table for the VPN subnet**
```
set interfaces wireguard wg0 route-allowed-ips true
```

**Set the UDP port for WG (that peers will use)**
WireGuard default port is `51820`, but can be changed to any port
```
set interfaces wireguard wg0 listen-port 51820
```

Save
```
commit ; save
```

## Step 4. Adding peers to the wg0 Interface

### Adding Client 01
Note: make sure you are in `configure` mode.
```
set interfaces wireguard wg0 peer <public-key-here>
```

```
set interfaces wireguard wg0 peer <public-key-here> allowed-ips 10.0.0.5/32
```

```
set interfaces wireguard wg0 peer <public-key-here> description client01
```

### Adding Additional Clients
When adding additional peers, repeat the steps above, make sure to update `allowed-ips` and `description` for the new clients.

```
set interfaces wireguard wg0 peer <public-key-here>
```

```
set interfaces wireguard wg0 peer <public-key-here> allowed-ips 10.0.0.6/32
```

```
set interfaces wireguard wg0 peer <public-key-here> description client02
```

Save
```
commit ; save
```

## Step 5. Create firewall rules for WireGuard
Create an accept rule in `WAN_LOCAL` to accept all incoming UDP connections from port `51820` (or any port of your choice).
```
set firewall name WAN_LOCAL rule 50 action accept
set firewall name WAN_LOCAL rule 50 protocol udp
set firewall name WAN_LOCAL rule 50 destination port 51820
set firewall name WAN_LOCAL rule 50 description 'WireGuard'
```

Save
```
commit ; save
```

Once this is done, your `wg0` interface and firewall configuration should look something like this.

```bash
user@ER-X$ show configuration

  wireguard wg0 {
        address 10.0.0.1/32
        listen-port 51820
        peer Bf6LBfuoRDRbO4EJ+tawJXu6qu5BOWaXGK0V+uVRC3Q= {
            allowed-ips 10.0.0.6/32
            description client02
        }
        peer Kf6LBfuoRDRbO4EJ+tawJXu6qu5BOWaXGK0V+uVRC3Q= {
            allowed-ips 10.0.0.5/32
            description client01
        }
        }
        private-key ****************
        route-allowed-ips true
    }



        }
        rule 50 {
            action accept
            description WireGuard
            destination {
                port 51820
            }
            log enable
            protocol udp
            source {
            }
        }
    }
}
```
## Step 6. Constructing the Config on the peer side
### Config File (.conf)
Create a file on the peer, with the file extension as `.conf`

The peer side needs a few pieces of information to create the tunnel:

- The server’s public key
- The server’s endpoint (public IP address, or DNS record)
- The peer’s `private key`
- The peer’s IP address in the VPN subnet (the allowed IPs value set on the server)

Therefore, the previously generated `client01 private-key` and the `server-public-key`, should be copied to the peer device.

The configuration should look something like the one below:

### Example Client 01
```conf
[Interface]
PrivateKey = <private-key-here>
ListenPort = 51820
Address = 10.0.0.5/32
DNS = <any dns>, 9.9.9.9

[Peer]
PublicKey = <public-key-here>
AllowedIPs = 0.0.0.0/0
Endpoint = <your-public-ip-or-dynamic-dns-hostname>:51820
```

### Example Client 02
```conf
[Interface]
PrivateKey = <private-key-here>
ListenPort = 51820
Address = 10.0.0.6/32
DNS = <any dns>, 9.9.9.9

[Peer]
PublicKey = <public-key-here>
AllowedIPs = 0.0.0.0/0
Endpoint = <your-public-ip-or-dynamic-dns-hostname>:51820
```
Once the `.conf` file is created, you can import that into the peer/device of your choice.

To bring up your tunnel, you can use the `wg-quick` command.

```
wg-quick up client01.conf
```

Run `wg show` on your peer to verify you are connected to the endpoint.

```bash
user@PC$ wg show

interface: client01
  public key: <private-key>
  private key: (hidden)
  listening port: 51820
  fwmark: 0xca6c

peer: <peer-key>
  endpoint: xx.xx.xx.xx:51820
  allowed ips: 0.0.0.0/0
  latest handshake: 11 seconds ago
  transfer: 3.11 MiB received, 6.92 MiB sent
```

## Step  7. Save WireGuard Keys and Configuration Files
Once the above configuration is made, you can easily save the config by [running a backup](https://help.ui.com/hc/en-us/articles/360002535514-EdgeRouter-Backup-and-Restore-Configuration#2) from the Edgerouter's GUI.


1. Navigate to the **System** tab in the bottom-left of the GUI to download the backup configuration archive.

**System > Configuration Management & Device Maintenance > Back Up Config**


2. Download the backup config file by clicking on the **Download** button.

3. The EdgeRouter will prompt you to save the archive on your computer.

You can then extract this file on your local machine, and in the `/config` directory, you'll find the wireguard public and private keys you generated earlier.


# Quick Script
**Warning, the following script is not guaranteed to work, you may need to modify it according to your specific platform/version. Use at your own risk.**

Determine shell with `echo $SHELL`

```
user@ER-X:~$ echo $SHELL
/bin/vbash
```

EdgeOS comes with `vi`, you can use that to create the script.

```
user@ER-X:~$ touch wg-setup.sh
user@ER-X:~$ vi wg-setup.sh
```

NOTE: Make sure to modify your `$SHELL` in case it differs, for EdgeOS, it will usually be  `#!/bin/vbash`

Paste the following:

```bash
#!/bin/vbash

/bin/ip link add dev wg0 type wireguard
/bin/ip addr add 10.0.0.1/32 dev wg0
/usr/bin/sudo /usr/bin/wg setconf wg0 /home/$USER/wg0.conf
/bin/ip link set up dev wg0
/bin/ip route add 10.0.0.1/32 dev wg0
/usr/bin/sudo /sbin/ifconfig wg0 mtu 1300
```

Make executable

```
chmod +x wg-setup.sh
```

Run

```
./wg-setup.sh
```

Sources:
- [https://github.com/WireGuard/wireguard-vyatta-ubnt/wiki/EdgeOS-and-Unifi-Gateway](https://github.com/WireGuard/wireguard-vyatta-ubnt/wiki/EdgeOS-and-Unifi-Gateway)
- [https://www.wireguard.com/quickstart/](https://www.wireguard.com/quickstart/)
- [https://blog.usman.network/posts/wireguard-vpn-on-a-ubiquiti-edgerouter/](https://blog.usman.network/posts/wireguard-vpn-on-a-ubiquiti-edgerouter/)

