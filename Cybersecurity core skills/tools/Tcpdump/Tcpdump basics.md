#THM #Cybersecurity101 #Cybersecurity101-Wireshark-the-basics 
# Tcpdump basics
*a quick memo that covers all the basics in my own order ✨![[Pasted image 20250925143640.png]]*
*tcpdump website : https://www.tcpdump.org/*
## Definition
**`tcpdump`** is a powerful command-line packet analyzer used to capture and analyze network traffic. It displays packet headers and content that pass through a network interface.
## Essential Command Syntax
 The most basic form of the command is simply:
```bash
sudo tcpdump -i <interface>
```

| Option               | Purpose                                                                               |
| -------------------- | ------------------------------------------------------------------------------------- |
| **`-i <interface>`** | Specifies the **network interface** to listen on (e.g., `eth0`, `wlan0`, `lo`).       |
| **`-n`**             | **Do not** convert addresses to names (faster, shows IP addresses).                   |
| **`-nn`**            | **Do not** convert protocol and port numbers to names (shows numbers).                |
| **`-v`**             | Verbose output. Use `-vv` or `-vvv` for more detail.                                  |
| **`-c <count>`**     | Exit after receiving `<count>` packets.                                               |
| **`-s 0`**           | Capture the entire packet length (don't truncate). Default is usually 68 or 96 bytes. |
| **`-w <file.pcap>`** | Write raw packet data to a file for later analysis (e.g., in Wireshark).              |
| **`-r <file.pcap>`** | Read packets from a saved file instead of a live interface.                           |
| **`-P`**             | Only traffic from or to my computer                                                   |
## Essential filtering
Filters are key to reducing noise. They are placed **after** all other options.
### Host and Port Filters

|Filter Expression|Purpose|
|---|---|
|`host 192.168.1.1`|Traffic only to or from this **IP address**.|
|`src host 10.0.0.5`|Traffic only **from** this IP address.|
|`dst port 80`|Traffic only **to** destination port 80 (HTTP).|

### Protocol Filters

|Filter Expression|Purpose|
|---|---|
|`arp`|Capture only **ARP** packets.|
|`icmp`|Capture only **ICMP** packets (used by `ping`).|
|`tcp`|Capture only **TCP** traffic.|
|`udp`|Capture only **UDP** traffic.|

**Example:** Capture only traffic directly addressed to your host on the `eth0` interface, using IP addresses and port numbers.
```bash
sudo tcpdump -i eth0 -nn -P
```

## Understanding the Output

A typical TCP output line looks like this:

`14:46:57.123456 IP 10.0.0.10.51234 > 172.217.14.78.443: Flags [S], seq 12345, win 65535, length 0`

|Element|Description|
|---|---|
|`14:46:57.123456`|Timestamp (hour:min:sec.microseconds).|
|`IP`|Network layer protocol (Internet Protocol).|
|`10.0.0.10.51234`|**Source IP** and **Port**.|
|`>`|Direction of traffic.|
|`172.217.14.78.443`|**Destination IP** and **Port** (HTTPS).|
|`Flags [S]`|**TCP Flags**: `[S]`=SYN, `[.]`=ACK, `[P]`=PUSH, `[F]`=FIN, `[R]`=RST.|
|`length 0`|Payload size of the TCP segment.|