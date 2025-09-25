#THM #Cybersecurity101-Networking #Cybersecurity101-NetworkingCoreProtocols 

TODO merge with other HTTP on ubuntu
## HTTPS
HTTPS = HTTP over TLS
1. Establish a TCP 3-way handshake with the target server
2. Establish a TLS session
3. Communicate using the HTTP protocol. For ex. issue HTTP requests.
**=> The reason the TLS encryption doesn't happen first is because TLS is an application layer protocol that requires a reliable transport channel (TCP) to be established first.** ❗(25/09/25)
### Encrypted packets example
The screenshot below shows that a TCP session is established in the first three packets, marked with `1`. Then, several packets are exchanged to negotiate the TLS protocol, marked with `2`. `1` and `2` are where the **TLS negotiation and establishment** take place.

Finally, HTTP application data is exchanged, marked with `3`. Looking at the Wireshark screenshot, we see that it says “Application Data” because there is no way to know if it is indeed HTTP or some other protocol sent over port 443.

![Wireshark displaying a TCP connection getting established, a TLS session getting established, and encrypted application data](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1721903449717.png)

As expected, if one tries to follow the stream of packets and combine all their contents, they will only get gibberish, as shown in the screenshot below. The exchanged traffic is encrypted; the red is sent by the client, and the blue is sent by the server. There is no way to know the contents without acquiring the encryption key.

![Wireshark displaying assembled encrypted HTTPS traffic](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1721903354908.png)

#### Getting the Encryption Key

Adding TLS to HTTP leads to all the packets being encrypted. We can no longer see the contents of the exchanged packets unless we get access to the private key. Although it is improbable that we will have access to the keys used for encryption in a TLS session, we repeated the above screenshots after providing the decryption key to Wireshark. The TCP and TLS handshakes don’t change; the main difference starts with the HTTP protocol marked 3. For instance, we can see when the client issues a `GET`.

![Wireshark displaying a TCP connection getting established, a TLS session getting established, and HTTP request sent and response received.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1729689224251.png)

If you want to see the data exchanged, now is your chance! It is still regular HTTP traffic hidden from prying eyes.

![Wireshark displaying assembled HTTPS request and response after decryption](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1721903477148.png)

The key takeaway is that TLS offered security for HTTP without requiring any changes in the lower or higher layer protocols. In other words, TCP and IP were not modified, while HTTP was sent over TLS the way it would be sent over TCP.