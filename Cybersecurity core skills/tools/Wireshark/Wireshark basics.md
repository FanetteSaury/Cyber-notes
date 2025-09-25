#THM #Cybersecurity101 #Cybersecurity101-Wireshark-the-basics
walkthrough : https://www.youtube.com/watch?v=oSwipo6zSJ4
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
### Traffic Sniffing![[Pasted image 20250925105822.png]]
**= capturing traffic**
- **start : click on the blue "shark button"**
-  the red button will stop the sniffing
- the green button will restart the sniffing process. The status bar will also provide the used sniffing interface and the number of collected packets.
### Merge PCAP Files
Wireshark can combine two pcap files into one single file. You can use the **"File --> Merge"** menu path to merge a pcap with the processed one. When you choose the second file, Wireshark will show the total number of packets in the selected file. Once you click "open", it will merge the existing pcap file with the chosen one and create a new pcap file. Note that you need to save the "merged" pcap file before working on it.  

![Wireshark - merge pcaps](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/bbc3f7938f8d3086953d5b0342422019.png)  

### Check File Details
Knowing the file details is helpful. Especially when working with multiple pcap files, sometimes you will need to know and recall the file details (File hash, capture time, capture file comments, interface and statistics) to identify the file, classify and prioritise it. You can view the details by following "**Statistics --> Capture File Properties"** or by clicking the **"pcap icon located on the left bottom"** of the window.

![Wireshark - file details](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/1ccc88dc2b66e935f2f382387ce3c0ec.png)  
## Packet Dissection
Dissection of the Wireshark packet regarding to the 7 OSI layers
#### The Frame (Layer 1)
This will show you what frame/packet you are looking at and details specific to the Physical layer of the OSI model.
![Wireshark - layer 1](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/9d23e2081fa68e7d6f602aa8b0d316d9.png)

#### Source [MAC] (Layer 2)
This will show you the source and destination MAC Addresses; from the Data Link layer of the OSI model.

![Wireshark - layer 2](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/cd06b372ae6338348ff521afb4c7243f.png)

#### Source [IP] (Layer 3)
This will show you the source and destination IPv4 Addresses; from the Network layer of the OSI model.
![Wireshark - layer 3](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d71eb4efc8d48a968a3e078045bd1511.png)

#### Protocol (Layer 4)
This will show you details of the protocol used (UDP/TCP) and source and destination ports; from the Transport layer of the OSI model.

![Wireshark - layer 4](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c373f8492470524a8f01fded43856a27.png)

#### Protocol Errors
This continuation of the 4th layer shows specific segments from TCP that needed to be reassembled.

![Wireshark - protocol error](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/23bbe6ae6e8168cd0662998ff444b067.png)

#### Application Protocol (Layer 5)
This will show details specific to the protocol used, such as HTTP, FTP,  and SMB. From the Application layer of the OSI model.

![Wireshark - layer 5](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/879aea2816018d27769fc8490e4af51b.png)

#### Application Data
This extension of the 5th layer can show the application-specific data.

![Wireshark - application data](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c2d9c3ce498c6f9044413b68df287c14.png)
## Packet Navigation
### go to packet number (the number is a id given by Wireshark) in *Go > Go to Packet...*![[Pasted image 20250925122942.png]]
### find a packet with filters in *Edit > Find Packet...*![[Pasted image 20250925122938.png]]
### mark a packet. Thus the color becomes black![[Pasted image 20250925122933.png]]
### comment a packet![[Pasted image 20250925123006.png]]
### export a packet![[Pasted image 20250925123034.png]]
### export objects
Wireshark can extract files transferred through the wire. For a security analyst, it is vital to discover shared files and save them for further investigation. Exporting objects are available only for selected protocol's streams (DICOM, HTTP, IMF, SMB and TFTP).

![Wireshark - export objects](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/16c22447c36bff2e415ea75a764854c8.png)
### format time display in *View > Time Display Format*![[Pasted image 20250925123150.png]]![[Pasted image 20250925123156.png]]### Expert Info
Wireshark also detects specific states of protocols to help analysts easily spot possible anomalies and problems. Note that these are only suggestions, and there is always a chance of having false positives/negatives. Expert info can provide a group of categories in three different severities. Details are shown in the table below.

|   |   |   |
|---|---|---|
|**Severity**|**Colour**|**Info**|
|**Chat**|**Blue**|Information on usual workflow.|
|**Note**|**Cyan**|Notable events like application error codes.|
|**Warn**|**Yellow**|Warnings like unusual error codes or problem statements.|
|**Error**|**Red**|Problems like malformed packets.|

Frequently encountered information groups are listed in the table below. You can refer to Wireshark's official documentation for more information on the expert information entries.

|   |   |   |   |
|---|---|---|---|
|**Group**|**Info**|**Group**|**Info**|
|**Checksum**|Checksum errors.|**Deprecated**|Deprecated protocol usage.|
|**Comment**|Packet comment detection.|**Malformed**|Malformed packet detection.|

You can use the **"lower left bottom section"** in the status bar or **"Analyse --> Expert Information"** menu to view all available information entries via a dialogue box. It will show the packet number, summary, group protocol and total occurrence.

![Wireshark - expert info](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/31917b6f1e846d3383218cabf1c07caf.png)

## Packet Filtering
### Two types of filtering
- Capture filters ⚠
- Display filters ⚠
### Apply as Filter

This is the most basic way of filtering traffic. While investigating a capture file, you can click on the field you want to filter and use the "right-click menu" or **"Analyse** **--> Apply as Filter"** menu to filter the specific value. Once you apply the filter, Wireshark will generate the required filter query, apply it, show the packets according to your choice, and hide the unselected packets from the packet list pane. Note that the number of total and displayed packets are always shown on the status bar.

![Wireshark - apply as filter](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/463abd0a5cad55831b54a37c17092505.png)

### Conversation Filter

When you use the "Apply as a Filter" option, you will filter only a single entity of the packet. This option is a good way of investigating a particular value in packets. However, suppose you want to investigate a specific packet number and all linked packets by focusing on IP addresses and port numbers. In that case, the "Conversation Filter" option helps you view only the related packets and hide the rest of the packets easily. You can use the"right-click menu" or "**Analyse --> Conversation Filter**" menu to filter conversations.

![Wireshark - conversation filter](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/6b31a8581e560286aee74fb9a608dfc9.png)

### Colourise Conversation

This option is similar to the "Conversation Filter" with one difference. It highlights the linked packets without applying a display filter and decreasing the number of viewed packets. This option works with the "Colouring Rules" option ad changes the packet colours without considering the previously applied colour rule. You can use the "right-click menu" or **"View --> Colourise Conversation"** menu to colourise a linked packet in a single click. Note that you can use the **"View --> Colourise Conversation --> Reset Colourisation"** menu to undo this operation.

![Wireshark - colourise conversation](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/b7a7ce6afa9c421e6bfaebac719d348c.png)

### Prepare as Filter 

Similar to "Apply as Filter", this option helps analysts create display filters using the "right-click" menu. However, unlike the previous one, this model doesn't apply the filters after the choice. It adds the required query to the pane and waits for the execution command (enter) or another chosen filtering option by using the **".. and/or.."** from the "right-click menu".

![Wireshark - prepare as filter](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/0291e6095277eaebf8f9a8f8df0f1ec6.png)

### Apply as Column

By default, the packet list pane provides basic information about each packet. You can use the "right-click menu" or "**Analyse --> Apply as Column**" menu to add columns to the packet list pane. Once you click on a value and apply it as a column, it will be visible on the packet list pane. This function helps analysts examine the appearance of a specific value/field across the available packets in the capture file. You can enable/disable the columns shown in the packet list pane by clicking on the top of the packet list pane.

![Wireshark - apply as column](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/8eac68abb9c10fccce114f6ad803a5dd.png)

### Follow Stream

Wireshark displays everything in packet portion size. However, it is possible to reconstruct the streams and view the raw traffic as it is presented at the application level. Following the protocol, streams help analysts recreate the application-level data and understand the event of interest. It is also possible to view the unencrypted protocol data like usernames, passwords and other transferred data.

You can use the"right-click menu" or  **"Analyse** **--> Follow TCP/UDP/HTTP Stream"** menu to follow traffic streams. Streams are shown in a separate dialogue box; packets originating from the server are highlighted with blue, and those originating from the client are highlighted with red.

![Wireshark - follow stream](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d578e89a1f4a526fb8ede6fdf1a5f1b5.png) Once you follow a stream, Wireshark automatically creates and applies the required filter to view the specific stream. Remember, once a filter is applied, the number of the viewed packets will change. You will need to use the "**X** **button**" located on the right upper side of the display filter bar to remove the display filter and view all available packets in the capture file.

---

Questions I stumbled upon :
- what is a payload again ?
	- The actual data being transmitted
- what is the difference between TCP payload and TCP segment data ?
	- *todo* 👁 https://ask.wireshark.org/question/3498/what-is-the-difference-between-tcp-payload-and-tcp-segment-data/?answer=3512#post-id-3512 