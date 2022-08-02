# Strongswan ike configuration

Written By: Nebi Volkan UNLENEN ( unlenen@gmail.com ) 

Here is an example of how to build a IKE Tunnel using strongswan app

## Example Configuration

- Enodeb 
```
    Public : 192.168.231.84
    Private : 10.13.0.60
    Subnet : 10.13.0.0/16
    Policy : 0.0.0.0 to 10.14.0.4/32
```
- IKE Strongswan router
```
    Public : 192.168.231.150
    Private : 10.14.0.248
    Subnet : 10.14.0.0/24  
```
- Core
```
  Policy : 10.14.0.0/24 to 10.13.0.34/32 (core)
```

## Installation
```
apt-get install strongswan libcharon-extra-plugins strongswan-pki -y
```

## Configuration
```
vi /etc/sysctl.conf
net.ipv4.ip_forward = 1
net.ipv6.conf.all.forwarding = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0

```
## Starting Service
```
    service strongswan restart
    systemctl enable strongswan
    ipsec restart
```

## Check Status
```
ipsec status
```

## Watch From wireshark 
```
plink.exe -no-antispoof -pw "MY_SUPER_PASSWORD" root@192.168.x.y /usr/sbin/tcpdump -i any -w- 'port!22' | wireshark -k -i -
```
