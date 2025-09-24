#THM #Cybersecurity101 #Cybersecurity101-Wireshark-the-basics
![[Pasted image 20250924163857.png]]
## Definition
Wireshark is the world's most widely used **network protocol analyzer** (or network analyzer). This more technical term encompasses two distinct functions:

1. **Packet Sniffing (or Capture):** This is the act of **intercepting** network traffic (data packets or frames) that passes through a computer's network interface, including traffic not specifically addressed to the machine (often by putting the network interface card in "promiscuous mode"). **Wireshark performs this function.**
    
2. **Packet Analysis (or Dissection):** This is the act of **decoding, displaying, and interpreting** the captured data. Wireshark excels at this by providing a comprehensive Graphical User Interface (GUI) that breaks down packets according to hundreds of network protocols (Ethernet, IP, TCP, HTTP, etc.), making the raw data human-readable.
    

In short, Wireshark is a **sniffer** because it captures the data, and an **analyzer** because it helps you understand the data it captured.
## Use cases
Wireshark is one of the most potent traffic analyser tools available in the wild. There are multiple purposes for its use:  

- Detecting and troubleshooting network problems, such as network load failure points and congestion.
- Detecting security anomalies, such as rogue hosts, abnormal port usage, and suspicious traffic.
- Investigating and learning protocol details, such as response codes and payload data. 

Note: Wireshark is not an Intrusion Detection System ([IDS](obsidian://open?vault=Cyber-notes.git&file=Cybersecurity%20core%20skills%2Fdefinitions%2FIDS)). It only allows analysts to discover and investigate the packets in depth. It also doesn't modify packets; it reads them. Hence, detecting any anomaly or network problem highly relies on the analyst's knowledge and investigation skills.
## GUI
![[Pasted image 20250924164527.png]]
### PCAP Files
![[Pasted image 20250924164624.png]]
### Colouring

![[Pasted image 20250924165332.png]]
*description : Default permanent colouring*
