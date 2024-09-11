# Home Lab: Active Directory Domain Services

Simulation of a business that uses AD for user and asset management

---

1. Installed VirtualBox for a virtual machine
    - Downloaded Windows Server 2019 ISO as the OS for the Domain Controller that contains an AD server, on the virtual machine
    - Downloaded Windows 10 ISO as the OS for the client that will connect to the domain

2. Created a virtual machine for the domain controller
    - Allocated megabytes for the RAM and hard disk drive, allocated cores for the CPU

3. Configured 2 network adapters
    - One is dedicated to the internet and is using Network Address Translation. Uses DHCP from host’s home router
    - The other is dedicated to the internal network that clients will connect to. Manually configured IP address, Subnet mask, DNS server

4. Installed Active Directory Domain Services

5. Configured Remote Access Server and NAT so the client on the private virtual network can access the internet through the domain controller
    - NAT allows internal clients to connect to the internet using one public IP address

6. Configured DHCP and DNS server on the domain controller, so the client virtual machine can automatically obtain an IP address, and connect to the internet
    - Configured DHCP scope, lease duration, default gateway (domain controller’s IP address), DNS server (domain controller’s IP address)

7. Ran a powershell script that will automatically create 200 users in Active Directory

8. Created a second VM for the client and installed Windows 10
    - This VM will connect to the private VirtualBox network
    - This client VM will be added to the domain and a domain account will be logged into this client VM
    - Joined the domain, mydomain.com. This allows any of the users in the domain to log into this client VM
