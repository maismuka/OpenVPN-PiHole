# OpenVPN-PiHole

This step by step is to create a PiHole VPS Server which is will be bypassed by OpenVPN.

USER - OpenVPN - PiHole - Internet

## Introduction

What is PiHole : A black hole for Internet advertisements. The Pi-hole acts as a Domain Name System (DNS) server, something that sits in-between you and the internet. This allows the Pi-hole to intercept any outgoing or incoming DNS requests and can block or pass certain domains from accessing your device, keeping your computer and other devices safe from ads

What is OpenVPN : OpenVPN is an open-source commercial software that implements virtual private network (VPN) techniques to create secure point-to-point or site-to-site connections in routed or bridged configurations and remote access facilities. It uses a custom security protocol that utilizes SSL/TLS for key exchange.

## Requirements

Since I am goinng to do this all virtually, you must acquire;

1. 2 VPS Server
2. MobaXterm

The VPS server will have different function;

1. VPN Server

2. PiHole Server

The concept here is to create a VPN server which is the domain is intercepted by PiHole.
Then the simple method is to first create a PiHole server and acquire the IP address.
After that, create a VPN server, but the DNS address will be the PiHole IP address.

As simple as that

Lets start!

## VPN Server

Download this OpenVPN Script

`https://github.com/maismuka/OpenVPN-PiHole/blob/master/openvpn-install.sh`

`chmod 777 openvpn-install.sh`

Then run it

`./openvpn-install.sh`

Then continue to set the setting default installation.

In the end, the script will ask for the `client`. This indicate you have successfully install OpenVPN on your server

## PiHole Server

Based on `https://github.com/pi-hole/pi-hole`, I just simply download the script provided and run it

```
wget -O basic-install.sh https://install.pi-hole.net
sudo bash basic-install.sh
```

There's also nothing much, set all to default, but when prompted with `select DNS server`, you must select `custom`

Then proceed to put into your PiHole server IP, left next optional DNS as empty

After prompted the DNS like this;

```
167.71.208.111, 
```

The simple configuration is set all as default!

After all done, there will be prompted to Admin web for PiHole and your password. Save it for later.

Now you have PiHole on your VPS Server.

Simply type `ip a s` to get your server IP

```
root@maismukapi:~# ip a s
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 46:3d:8b:4b:cb:cb brd ff:ff:ff:ff:ff:ff
    inet 167.71.208.111/20 brd 167.71.223.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet 10.15.0.6/16 brd 10.15.255.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::443d:8bff:fe4b:cbcb/64 scope link
       valid_lft forever preferred_lft forever

```

My PiHole server IP is `167.71.208.111`

## Creating VPN Client

After a success install OpenVPN, lastly the script will prompt to create a `Client Name`

Put any name without space, eg `maismuka`

After that choose between `[1] Passwordless` or `[2] With password`

After that, a new file name `maismuka.ovpn` has created.

To check, use command `ls`

This is the 'key' that you or anybody will need to connect to your VPN

Export, download or copy the key to your user/client.


## Client Connecting VPN

Download and install from OpenVPN website that suits your needs

`https://openvpn.net/community-downloads/`

After complete your installation, open the application and proceed to `Import File`

Import your file by browse to your key provided earlier.

Please be aware that only one key can be used per device.

If you need to create another key for another client or devices, simply run `./openvpn-install.sh` on your VPN Server.


## Managing PiHole Web 

Go to the web address that provided earlier by your PiHole installation.

If you missed it, your PiHole web server is at `http://<PiHole Vps Ip>/admin` 

For me its, `http://167.71.208.111/admin`

Login and proceed to Blacklist.

Here is the PiHole DNS blocking catchphrase works. All you need to obtain is some ads domain address link, paste here, and add to `Regex`



# Thats All Folks



