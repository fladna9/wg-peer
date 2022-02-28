# wg-peer
Managing peers was a bit hard. Not anymore.

## Notice
This script is not fool proof, and many security considerations are at best ***meh***, but for my usecase, it is fitting my needs enough.
This script must be run by root.

## Usage
```
wg-peer [-a|-add|a|add|-r|-revoke|r|revoke] PROFILENAME
```

## Installation and configuration of the script
Create the folder /etc/wireguard/peers: `# mkdir -p /etc/wireguard/peers/`
Download the script from `https://raw.githubusercontent.com/fladna9/wg-peer/main/wg-peer` and copy it to `/usr/local/sbin/wp-peer`.
Edit `/usr/local/sbin/wp-peer`, and tune the following variables:
```
## SERVER INFO AND PEER CONFIGURATION ##
SERVERPUBKEY=""
SERVERIP=""
SERVERPORT=""
PERSISTENTKEEPALIVE="25"
PEERALLOWEDIP="0.0.0.0/0"
DNS="1.1.1.1"
SERVERIFNAME="wg0"
## SCRIPT CONFIG ##
WORKINGDIR="/etc/wireguard/peers/"
INDEXFILE="index"
STARTINDEX="20"
IPNET="192.168.255."
```
Note that this script is quite simple and is written for /24 networks.

Once ready, do a `# chmod 500 /usr/local/sbin/wg-peer`, and see how to use it below.

## Examples
Create the JeanBon profile with:
```
# wg-peer add JeanBon
Creating profile JeanBon...
Allocated IP address: <redacted>
Private key is <redacted>
Public key is dp8hgDTcxaFrl3aM0tjV5L6P6C+qllH4ykyLB6ur+hA=
Peer keys added to wg server.
Done. Configuration file JeanBon.conf generated.

##### CONFIG FILE #####
[Interface]
PrivateKey = <redacted>
Address = <redacted>
DNS = <redacted>

[Peer]
PublicKey = <redacted>
AllowedIPs = <redacted>
Endpoint = <redacted>:<redacted>
PersistentKeepalive = <redacted>
#######################

Put the lines between #s in a conf file, and off you go !
See ya.
```
You can find the `JeanBon.conf` peer profile in `/etc/wireguard/peers/`

Revoke the JeanBon profile with:
```
# wg-peer revoke JeanBon
Revoking profile JeanBon...
Revoking dp8hgDTcxaFrl3aM0tjV5L6P6C+qllH4ykyLB6ur+hA=...
Done. Configuration file JeanBon.conf deleted.
```

# LICENSE
wg-peer - Wireguard Simple Peer Manager
Copyright (C) 2022  Maxence MOHR

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see https://www.gnu.org/licenses/
