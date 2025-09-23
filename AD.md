# "Active Directory"
todo flashcards
## I/ Introduction
[[Active Directory|Definition]]
## II/ Windows Domain
**"DC (Domain Controller)"** : name of the server running the AD services
#### A Real-World Example
If this sounds a bit confusing, chances are that you have already interacted with a Windows domain at some point in your school, university or work.

In school/university networks, you will often be provided with a username and password that you can use on any of the computers available on campus. Your credentials are valid for all machines because whenever you input them on a machine, it will forward the authentication process back to the Active Directory, where your credentials will be checked. Thanks to Active Directory**, your credentials don't need to exist in each machine and are available throughout the network.**

Active Directory is also the component that allows your school/university to restrict you from accessing the control panel on your school/university machines. Policies will usually be deployed throughout the network so that you don't have administrative privileges over those computers.
## III/ Active Directory
### AD Hierarchy
- Users
	- People
	- Services
- Machines
- Security Groups
	- Enterprise Admin
		- Permission: Admin all [[#^cbb8b8|trees]] if they exist
	- Domain admins
		- Permission: Admin any computer in the domain and the DCs
	- Server Operators
		- Permission: administer DCs. Cannot change any admin group roles
	- Backup Operators
		- Permission: access any files, regardless of their permissions. Those operators are used for backups.
	- Account Operators
		- Permission: create or modify other accounts in the domain
	- Domain Users
		- Includes all users
	- Domain Computers
		- Includes all computers
	- Domain Controllers
		- Includes all DCs
#### Configure the AD
1. log in the Domain Controller
2. Run "Active Directory Users and Computers"![[Pasted image 20250923112954.png]]
##### Security Groups vs Organizational Units

While both are used to classify users and computers, their purposes are entirely different:

- **OUs** are handy for **applying policies** to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise. Remember, a user can only be a member of a single OU at a time, as it wouldn't make sense to try to apply two different sets of policies to a single user.
- **Security Groups**, on the other hand, are used to **grant permissions over resources**. For example, you will use groups if you want to allow some users to access a shared folder or network printer. A user can be a part of many groups, which is needed to grant access to multiple resources.
![[Pasted image 20250923115231.png]]
## IV/Managing Users in AD
### Deletion
By default, OUs are protected against accidental deletion. To delete the OU, we need to enable the **Advanced Features** in the View menu.
### Delegation
Delegate some specific controls over an OU to a user.
- Example : Giving Phillip control because he's the IT manager, to reset passwords.![[Pasted image 20250923140935.png]]
![[Pasted image 20250923140950.png]]![[Pasted image 20250923140957.png]]
## V/ Managing Computers in AD
ok
## VI/ Group Policies
### Group Policy Objects (GPO)
: collection of settings that can be applied to OUs. 📍In *Group Policy Management*
### GPO deployment
Over the network via a share called `SYSVOL` stored in the DC. The SYSVOL share points by default to the `C:\Windows\SYSVOL\sysvol\` directory on each of the DCs in our network.

Once a change has been made to any GPOs, it might take up to 2 hours for computers to catch up. If you want to force any particular computer to sync its GPOs immediately, you can always run the following command on the desired computer:
`PS C:\> gpupdate /force
![[Pasted image 20250923142446.png]]`
![[Pasted image 20250923142506.png]]
## VII/ Authentication Methods
### Kerberos
[[Kerberos|Definition]]
### NetNTLM
[[NetNTLM|Definition]]
## VIII/ Trees, Forests and Trusts
### Trees

^cbb8b8

![[Pasted image 20250923144319.png]]
#### Usecase example
Imagine, for example, that suddenly your company expands to a new country. The new country has different laws and regulations that require you to update your GPOs to comply. In addition, you now have IT people in both countries, and each IT team needs to manage the resources that correspond to each country without interfering with the other team. While you could create a complex OU structure and use delegations to achieve this, having a huge AD structure might be hard to manage and prone to human errors.

Luckily for us, Active Directory supports integrating multiple domains so that you can partition your network into units that can be managed independently. If you have two domains that share the same namespace (`thm.local` in our example), those domains can be joined into a **Tree**.
If our `thm.local` domain was split into two subdomains for UK and US branches, you could build a tree with a root **domain** of `thm.local` and two **subdomains** called `uk.thm.local` and `us.thm.local`, each with its AD, computers and users:![[Pasted image 20250923144423.png]]
### Forests
Managed domains can also be configured in different namespaces.
![[Pasted image 20250923144837.png]]
### Trust relationships
Having multiple domains organised in trees and forest allows you to have a nice compartmentalised network in terms of management and resources. But at a certain point, a user at THM UK might need to access a shared file in one of MHT ASIA servers. For this to happen, domains arranged in trees and forests are joined together by **trust relationships**.

In simple terms, having a trust relationship between domains allows you to authorise a user from domain `THM UK` to access resources from domain `MHT EU`.
#### One-way trust relationship
The simplest trust relationship that can be established is a **one-way trust relationship**. In a one-way trust, if `Domain AAA` trusts `Domain BBB`, this means that a user on BBB can be authorised to access resources on AAA:

![Trusts](https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/af95eb1a4b6c672491d8989f79c00200.png)

The direction of the one-way trust relationship is contrary to that of the access direction.

#### Two-way trust relationships
can also be made to allow both domains to mutually authorise users from the other. By default, joining several domains under a tree or a forest will form a two-way trust relationship.

It is important to note that having a trust relationship between domains doesn't automatically grant access to all resources on other domains. Once a trust relationship is established, you have the chance to authorise users across different domains, but it's up to you what is actually authorised or not.
## IX/ Conclusion
ok