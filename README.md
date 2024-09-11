# Home Lab: Active Directory Domain Services

Simulation of a business that uses AD for user and asset management

![Active Directory](images/Active%20Directory.PNG)

---

### 1. Installed VirtualBox to create Client and Domain Controller virtual machines
![VirtualBox](images/VirtualBox.png)
- Downloaded Windows Server 2019 ISO as the OS for the Domain Controller that contains an AD server, on the virtual machine
- Downloaded Windows 10 ISO as the OS for the client that will connect to the domain

### 2. Created a virtual machine for the domain controller
- Allocated megabytes for the RAM and hard disk drive, allocated cores for the CPU
- Configured 2 network adapters
    - One is dedicated to the internet and is using Network Address Translation. Uses DHCP from host machine's home router
    - The other is dedicated to the internal virtual network that the client VM can connect to. Manually configured the IP address, Subnet mask, DNS server

    ![Internal network configurations](images/internal%20network%20configurations.PNG)
   
- Configured Routing and Remote Access Server so the client on the private virtual network can access the internet through the domain controller
    - Uses NAT to allow internal clients to connect to the internet using one public IP address

    ![Remote Access Server](images/RAS.PNG)

- Configured DHCP and DNS server on the domain controller, so the client virtual machine can automatically obtain an IP address, and connect to the internet
    - Configured DHCP scope, lease duration, default gateway (domain controller’s IP address), DNS server (domain controller’s IP address)

    ![DHCP Configuration](images/DHCP%20Scope.PNG)

- Installed Active Directory Domain Services
- Ran a PowerShell script that will automatically create 200 users in Active Directory

    ![PowerShell Script](images/PowerShell%20Script.PNG)

- Created groups that represent the departments of the company, and added members to the groups

### 3. Created a second VM for the client and installed Windows 10
- This VM will connect to the private VirtualBox network. The client will be added to the domain, and a user in the company can log into this client VM

    ![Client name and Domain](images/client%20name%20and%20domain.PNG)
  
- Encountered an issue where the client VM could not connect to the network. The solution was to correct network portion of the DHCP scope on the domain controller VM (was 176.16.0 instead of 172.16.0)

### 4. Created a Group Policy and shared folders for each group

![Network drives](images/user%20dearls%20has%20access%20to%20RND%20network%20drive.PNG)

- Mapped network drives to the shared folders so the users can access them based on their permissions. Users had access to the appropriate department drives.
- Encountered an issue where the mapped drives were not appearing when a user logged in. The solution was to link the GP to the users organizational unit

### 5. Reset user password and forced user to change their password on the next login attempt

![User must change password](images/user%20must%20change%20password%20at%20next%20log%20in.PNG)
