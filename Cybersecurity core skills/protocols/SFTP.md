#THB #Cybersecurity101-Networking #Cybersecurity101-NetworkingSecureProtocols
# Secure File Transfer Protocol
Secure version of [FTP](FTP)
## Definition
SFTP stands for SSH File Transfer Protocol and allows secure file transfer. It is part of the SSH protocol suite and shares the same port number, 22. If enabled in the OpenSSH server configuration, you can connect using a command such as `sftp username@hostname`. Once logged in, you can issue commands such as `get filename` and `put filename` to download and upload files, respectively. Generally speaking, SFTP commands are Unix-like and can differ from FTP commands.