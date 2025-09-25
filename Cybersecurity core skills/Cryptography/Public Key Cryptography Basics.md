#THM #Cybersecurity101 #Cybersecurity101-Cryptography 
✴*Discover how public key ciphers such as RSA work and explore their role in applications such as SSH.* ✴
# Public Key Cryptography Basics
## Words
- **Authentication**: You want to be sure you communicate with the right person, not someone else pretending.
- **Authenticity**: You can verify that the information comes from the claimed source.
- **Integrity**: You must ensure that no one changes the data you exchange.
- **Confidentiality**: You want to prevent an unauthorised party from eavesdropping on your conversations.
## RSA
### Definition
RSA is a method for encrypting data using two keys: one to lock (encrypt) and another to unlock (decrypt) it, relying on the difficulty of factoring large number.
## Algorithm
1. Bob chooses two prime numbers: _p_ = 157 and _q_ = 199. He calculates _n_ = _p_ × _q_ = 31243.
2. With _ϕ_(_n_) = _n_ − _p_ − _q_ + 1 = 31243 − 157 − 199 + 1 = 30888, Bob selects _e_ = 163 such that _e_ is relatively prime to _ϕ_(_n_); moreover, he selects _d_ = 379, where _e_ × _d_ = 1 mod _ϕ_(_n_), i.e., _e_ × _d_ = 163 × 379 = 61777 and 61777 mod 30888 = 1. The public key is (_n_,_e_), i.e., (31243,163) and the private key is $(n,d), i.e., (31243,379).
3. Let’s say that the value they want to encrypt is _x_ = 13, then Alice would calculate and send _y_ = _x__e_ mod _n_ = 13163 mod 31243 = 16341.
4. Bob will decrypt the received value by calculating _x_ = _y__d_ mod _n_ = 16341379 mod 31243 = 13. This way, Bob recovers the value that Alice sent.

The proof that the above algorithm works can be found in [modular arithmetic](https://www.britannica.com/science/modular-arithmetic) and is beyond the scope of this module. It is worth repeating that in this example, we picked a three-digit prime number, while in an actual application, _p_ and _q_ would be at least a 300-digit prime number each.
## Diffie-Hellman Key Exchange
![[5f04259cf9bf5b57aed2c476-1728439878360.svg]]
1. Alice and Bob agree on the **public variables**: a large prime number _p_ and a generator _g_, where 0 < _g_ < _p_. These values will be disclosed publicly over the communication channel. Although insecurely small, we will choose _p_ = 29 and _g_ = 3 to simplify our calculations.
2. Each party chooses a private integer. As a numerical example, Alice chooses _a_ = 13, and Bob chooses _b_ = 15. Each of these values represents a **private key** and must not be disclosed.
3. It is time for each party to calculate their **public key** using their private key from step 2 and the agreed-upon public variables from step 1. Alice calculates _A_ = _g__a_ mod _p_ = 313 mod 29 = 19 and Bob calculates _B_ = _g__b_ mod _p_ = 315 mod 29 = 26. These are the public keys.
4. Alice and Bob send the keys to each other. Bob receives _A_ = _g__a_ mod _p_ = 19, i.e., Alice’s public key. And Alice receives _B_ = _g__b_ mod _p_ = 26, i.e., Bob’s public key. This step is called the **key exchange**.
5. Alice and Bob can finally calculate the **shared secret** using the received public key and their own private key. Alice calculates _B__a_ mod _p_ = 2613 mod 29 = 10 and Bob calculates _A__b_ mod _p_ = 1915 mod 29 = 10. Both calculations yield the same result, _g__a__b_ mod _p_ = 10, the shared secret key.
## SSH
### Server authentication
```shell-session
root@TryHackMe# ssh 10.10.244.173
The authenticity of host '10.10.244.173 (10.10.244.173)' can't be established.
ED25519 key fingerprint is SHA256:lLzhZc7YzRBDchm02qTX0qsLqeeiTCJg5ipOT0E/YM8.
This key is not known by any other name.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.244.173' (ED25519) to the list of known hosts.
```

In the above interaction, the SSH client confirms whether we recognise the server’s public key fingerprint. ED25519 is the public-key algorithm used for digital signature generation and verification in this example. Our SSH client didn’t recognise this key and is asking us to confirm whether we want to continue with the connection. This warning is because a man-in-the-middle attack is probable; a malicious server might have intercepted the connection and replied, pretending to be the target server.

In this case, the user must authenticate the server, i.e., confirm the server’s identity by checking the public key signature. Once you answer with “yes”, the SSH client will record this public key signature for this host. In the future, it will connect you silently unless this host replies with a different public key.
### Client authentication
`ssh-keygen` is the program usually used to generate key pairs. It supports various algorithms, as shown on the page below.
https://tryhackme.com/room/publickeycrypto
### SSH Private keys
- Never share
- Using tools like [Cybersecurity core skills/tools/John the Ripper.md](John the Ripper), you can attack an encrypted SSH key to attempt to find the passphrase, highlighting the importance of using a complex passphrase and keeping your private key private.
- The `~/.ssh` folder is the default place to store these keys for OpenSSH. The `authorized_keys` (note the US English spelling) file in this directory holds public keys that are allowed access to the server if key authentication is enabled.
### CTF : Using SSH Keys to get a "Better Shell"
During CTFs, penetration testing, and red teaming exercises, SSH keys are an excellent way to “upgrade” a reverse shell, assuming the user has login enabled. Note that www-data usually does not allow this, but regular users and root will work. Leaving an SSH key in the `authorized_keys` file on a machine can be a useful backdoor, and you don’t need to deal with any of the issues of unstabilised reverse shells like Control-C or lack of tab completion.
## Digital Signatures and Certificates
**Digital Signatures** verify the authenticity and integrity of a message, ensuring it hasn’t been altered. They are generated using a private key and verified with a public key. Certificates are used to verify the identity of web servers (HTTPS) through a chain of trust starting with a Certificate Authority (CA).

Let’s say you have a website and want to use HTTPS. This step requires having a TLS certificate. You can get one from the various certificate authorities for an annual fee. Furthermore, you can get your own TLS certificates for domains you own using [Let’s Encrypt](https://letsencrypt.org/) for free. If you run a website, it’s worth setting up and switching to HTTPS, as any modern website would do.
## PGP and GPG
**PGP** stands for Pretty Good Privacy. It’s software that implements encryption for encrypting files, performing digital signing, and more. [GnuPG or GPG](https://gnupg.org/) is an open-source implementation of the OpenPGP standard.

**GPG** is commonly used in email to protect the confidentiality of the email messages. Furthermore, it can be used to sign an email message and confirm its integrity.

Below is an example of generating GPG. You are asked about the purpose of using `gpg`, whether signing only or signing and encrypting. Besides selecting the cryptographic algorithm, we needed to choose an expiry date for the generated key. Finally, we provided some information about us: our name, email address, and a comment usually about the purpose of this key.
 ```shell-session
gpg --full-gen-key  
gpg (GnuPG) 2.4.4; Copyright (C) 2024 g10 Code GmbH  
This is free software: you are free to change and redistribute it.  
There is NO WARRANTY, to the extent permitted by law.  
Please select what kind of key you want:  
   (1) RSA and RSA  
   (2) DSA and Elgamal  
   (3) DSA (sign only)  
   (4) RSA (sign only)  
   (9) ECC (sign and encrypt) *default*  
  (10) ECC (sign only)  
  (14) Existing key from card  
Your selection? 9  
Please select which elliptic curve you want:  
   (1) Curve 25519 *default*  
   (4) NIST P-384  
   (6) Brainpool P-256  
Your selection? 1  
Please specify how long the key should be valid.  
         0 = key does not expire  
      <n>  = key expires in n days  
      <n>w = key expires in n weeks  
      <n>m = key expires in n months  
      <n>y = key expires in n years  
Key is valid for? (0)   
Key does not expire at all  
Is this correct? (y/N) y  
GnuPG needs to construct a user ID to identify your key.  
Real name: strategos  
Email address: strategos@tryhackme.thm  
[...]  
pub   ed25519 2024-08-29 [SC]  
      AB7E6AA87B6A8E0D159CA7FFE5E63DBD5F83D5ED  
uid                      Strategos <strategos@tryhackme.thm>  
sub   cv25519 2024-08-29 [E]
```
You may need to use GPG to decrypt files in CTFs. With PGP/GPG, private keys can be protected with passphrases in a similar way that we protect SSH private keys. If the key is passphrase protected, you can attempt to crack it using John the Ripper and `gpg2john`. The key provided in this task is not protected with a passphrase. The man page for GPG can be found online [here](https://www.gnupg.org/gph/de/manual/r1023.html).

#### **Practical Example**

Now that you have your GPG key pair, you can share the public key with your contacts. Whenever your contacts want to communicate securely, they encrypt their messages to you using your public key. To decrypt the message, you will have to use your private key. Due to the importance of the GPG keys, it is vital that you keep a backup copy in a secure location.

Let’s say you got a new computer. All you need to do is import your key, and you can start decrypting your received messages again:

- You would use `gpg --import backup.key` to import your key from backup.key
- To decrypt your messages, you need to issue `gpg --decrypt confidential_message.gpg`