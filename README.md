# Home-Lab-Cybersecurity-Project
# Overview
This repository documents the setup and configuration of a cybersecurity home lab focused on Windows event monitoring using Sysmon and log analysis using Splunk Cloud. It includes configuration files, scripts, lab setup steps, and notes on log collection and analysis.

# Step 1: Lab Environment Setup
Created two virtual machines:
    Victim machine: Windows 10
    Attacker machine: Kali Linux


# Step 2: Setting Up Internal Network Connection Between VMs
To enable communication between the attacker (Kali Linux) and victim (Windows 10) machines, I set up an internal virtual network with static IP addresses.

   # Why This Is Important
    - Allows attacker and victim to communicate securely without exposing them to your real network or internet.
    - Provides a controlled environment to practice attacks and monitoring.
    
   # Step 2.1: Configure Virtual Network Adapter
      - In VirtualBox (or your VM software):
      - Open Settings for each VM (Victim and Attacker).
      - Go to Network settings.
      - For Adapter 1, set Attached to: to Internal Network (or Host-Only Adapter if preferred).
      - Name the internal network (e.g., lab-net).

  # Step 2.2: Assign Static IP Addresses
    Assign static IP addresses on each VM within the same subnet, for example:

            **Machine**	     **  IP Address**	  **Subnet Mask	Gateway**
            Victim (Win)	      10.10.10.2	    255.255.255.0	(leave blank)
            Attacker (Kali)	    10.10.10.3	    255.255.255.0	(leave blank)

  # Step 2.3: Set Static IP on Windows (Victim)
      - Open Control Panel > Network and Internet > Network and Sharing Center.
      - Click Change adapter settings.
      - Right-click on the internal network adapter → Properties.
      - Select Internet Protocol Version 4 (TCP/IPv4) → Properties.
      - Select Use the following IP address and enter:
      - IP Address: 10.10.10.2
      - Subnet Mask: 255.255.255.0
      - Default Gateway: leave blank or 10.10.10.1 (not necessary for internal network)
      - Click OK to save.

# Step 2.4: Set Static IP on Kali Linux (Attacker)
    Run these commands in terminal:
    **sudo ip addr add 10.10.10.3/24 dev eth0
    sudo ip link set eth0 up**

# Step 2.5: Test Connectivity
   ** From Kali terminal:**
            ping 10.10.10.2
            
    **From Windows Command Prompt:**
            cmd
            ping 10.10.10.3

            
    Both should respond successfully, confirming the network setup is working.
