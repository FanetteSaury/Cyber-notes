#THM #Cybersecurity101 #Cybersecurity101-NetworkingSecureProtocols 
# Virtual Private Network
![[5f04259cf9bf5b57aed2c476-1721903538365.svg]]
*Description : example of a company with two remote branches connecting to the main branch. A VPN client in the remote branches is expected to connect to the VPN server in the main branch. In this case, the VPN client will encrypt the traffic and pass it to the main branch via the established VPN tunnel (shown in blue). The VPN traffic is limited to the blue lines; the green lines would carry the decrypted VPN traffic.*

![[5f04259cf9bf5b57aed2c476-1721903568757.svg]]*Description : Two remote users using VPN clients to connect to the VPN server in the main branch. In this case, the VPN client connects a single device.*
## Leaks and dangers
Finally, although in many scenarios, one would establish a VPN connection to route all the traffic over the VPN tunnel, some VPN connections don’t do this. The VPN server may be configured to give you access to a private network but not to route your traffic. Furthermore, some VPN servers leak your actual IP address, although they are expected to route all your traffic over the VPN. Depending on why you are using a VPN connection, you might need to run a few more tests, such as a DNS leak test.