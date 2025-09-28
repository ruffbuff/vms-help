# VirtualBox Gaming VM Setup Guide

This guide helps you set up multiple virtual machines (VMs) for gaming promotions and referral programs. Each VM will appear as a separate device to external systems, allowing you to run multiple instances of games or promotional campaigns.

## Prerequisites

- **Minimum System Requirements:**
  - 16GB RAM (32GB recommended for multiple VMs)
  - 4+ CPU cores
  - 80GB+ free disk space
  - Internet connection (WiFi or Ethernet)

## Step 1: Download and Install VirtualBox

### 1.1 Download VirtualBox
1. Go to [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads)
2. Download **VirtualBox** for your operating system (Windows/Mac/Linux)
3. Download **VirtualBox Extension Pack** (same page, "All supported platforms")

### 1.2 Install VirtualBox
1. Run the VirtualBox installer with default settings
2. Complete the installation and restart if prompted

### 1.3 Install Extension Pack
1. Double-click the downloaded `.vbox-extpack` file
2. Or in VirtualBox: **File -> Preferences -> Extensions -> Add**
3. Accept the Oracle license agreement
4. Restart VirtualBox

## Step 2: Configure VirtualBox Settings

### 2.1 Initial VirtualBox Configuration
1. Open VirtualBox
2. **File -> Preferences -> General:**
   - Set "Default Machine Folder" to a drive with plenty of space
3. **Input:** Leave Host Key as Right Ctrl (or change to preference)

## Step 3: Create Your First Virtual Machine

### 3.1 Create New VM
1. Click **"New"** in VirtualBox
2. **Name:** GameVM_1
3. **Type:** Microsoft Windows
4. **Version:** Windows 10 or Windows 11 (64-bit)
5. Click **Next**

### 3.2 Allocate Resources
**For systems with 32GB RAM:**
- **Base Memory:** 8192 MB (8GB)
- **Processors:** 4 cores

**For systems with 16GB RAM:**
- **Base Memory:** 4096 MB (4GB)
- **Processors:** 2-4 cores

### 3.3 Create Virtual Hard Disk
1. **Create a virtual hard disk now**
2. **Hard disk file type:** VDI
3. **Storage:** Dynamically allocated
4. **Size:** 80-100 GB
5. Click **Create**

## Step 4: Configure VM for Gaming and Network Isolation

### 4.1 Display Settings
1. Select your VM -> **Settings -> Display:**
   - **Video Memory:** 128 MB (maximum)
   - **Graphics Controller:** VMSVGA or VBoxSVGA
   - **Enable 3D Acceleration:**  (if available)

### 4.2 Network Configuration (CRITICAL for isolation)
1. **Settings -> Network -> Adapter 1:**
   - **Attached to:** Bridged Adapter
   - **Name:**
     - **For WiFi (laptops):** Select your WiFi adapter
     - **For Ethernet (desktops):** Select your Ethernet adapter
   - **Advanced -> MAC Address:** Click refresh button =
   - **Cable connected:** 

### 4.3 System Optimization
1. **Settings -> System -> Motherboard:**
   - **Enable I/O APIC:** 
2. **Settings -> System -> Processor:**
   - **Enable PAE/NX:** 

### 4.4 Storage Configuration
1. **Settings -> Storage:**
   - **Controller IDE -> Empty**
   - Click disk icon -> **Choose a disk file**
   - Select your Windows ISO file

## Step 5: Install Windows

### 5.1 Start Installation
1. Click **Start** (green arrow)
2. Install Windows normally
3. Complete Windows setup with unique computer name (e.g., "GamePC-1")

### 5.2 Install Guest Additions
1. In running VM: **Devices -> Insert Guest Additions CD image**
2. Open **This PC** -> double-click **CD Drive (Guest Additions)**
3. Run **VBoxWindowsAdditions.exe** as administrator
4. Install with default settings
5. **Restart the VM**

### 5.3 Configure Display
After restart:
- **View -> Auto-resize Guest Display** 
- The screen will now resize properly with the window

## Step 6: Verify Network Isolation

### 6.1 Check VM Network Configuration
In the VM, open Command Prompt and run:
```cmd
ipconfig /all
```
Note down:
- **IPv4 Address** (e.g., 192.168.1.100)
- **Physical Address (MAC)** (e.g., 08-00-27-XX-XX-XX)

### 6.2 Compare with Host System
On your main computer, run the same command:
```cmd
ipconfig /all
```

**Success indicators:**
-  Different IP addresses (e.g., Host: 192.168.1.50, VM: 192.168.1.100)
-  Different MAC addresses
-  Same default gateway (router IP)

### 6.3 Test External IP
In VM browser, visit: https://whatismyipaddress.com/
- External IP may be the same (normal for home networks)
- The important part is different internal IPs and MAC addresses

## Step 7: Optimize VM Performance for Gaming

### 7.1 Windows Performance Settings
In the VM:
1. **System -> Advanced system settings -> Performance -> Settings**
2. Select **"Adjust for best performance"**
3. **Power Options:** Set to **"High performance"**

### 7.2 Disable Unnecessary Services
- Temporarily disable Windows Defender (for better performance)
- Turn off automatic updates during gaming
- Close background applications

## Step 8: Create Additional VMs

### 8.1 Clone Existing VM
1. **Shut down** the first VM completely
2. **Right-click VM -> Clone**
3. **Name:** GameVM_2
4. **MAC Address Policy:** -> **Generate new MAC addresses for all network adapters**
5. **Clone Type:** Full clone
6. Click **Clone**

### 8.2 Verify New VM Isolation
1. Start the cloned VM
2. Run `ipconfig /all` - should show different IP and MAC
3. Change computer name: **Settings -> System -> About -> Rename this PC**

### 8.3 Browser Isolation (Important)
For each VM, use different browsers or clear all data:
- **VM 1:** Chrome
- **VM 2:** Firefox
- **VM 3:** Edge
- Or clear all browser data between uses

## Step 9: Best Practices for Gaming Promotions

### 9.1 VM Management
- **Run VMs one at a time** for better performance
- **Different screen resolutions** per VM
- **Unique computer names** for each VM
- **Different browsers** or cleared browser data

### 9.2 Network Considerations
- Each VM gets a unique IP from your router
- MAC addresses must be different (automatic when cloning correctly)
- Use private/incognito browsing modes
- Avoid DNS/AdBlock software as some promotions detect this

### 9.3 Resource Management
**For 32GB RAM systems:**
- Run 2-3 VMs simultaneously (8GB each)
- Or 4-5 VMs (4-6GB each)

**For 16GB RAM systems:**
- Run 1 VM at a time (6-8GB)
- Or 2 VMs (4GB each)

## Troubleshooting

### Low FPS in Games
- Increase VM RAM allocation
- Assign more CPU cores
- Enable 3D acceleration if available
- Close unnecessary programs on host system

### Network Issues
- Verify Bridged Adapter is selected
- Check that different MAC addresses are generated
- Restart router if VMs get same IP

### 3D Acceleration Grayed Out
- Install Extension Pack
- Try different Graphics Controllers (VBoxSVGA, VBoxVGA)
- Some hardware doesn't support VM 3D acceleration

## Important Notes

-> **Legal Disclaimer:** Only use this setup for legitimate promotional campaigns that allow multiple accounts. Always read terms of service.

-> **Performance:** VMs run 30-50% slower than native systems. Choose games accordingly.

-> **Security:** Each VM is isolated but shares your internet connection and external IP address.

## Quick Setup Checklist

- [ ] VirtualBox installed
- [ ] Extension Pack installed
- [ ] VM created with 8GB RAM, 4 cores, 80GB disk
- [ ] Bridged network adapter configured
- [ ] Unique MAC address generated
- [ ] Windows installed and updated
- [ ] Guest Additions installed
- [ ] Network isolation verified (different IPs/MACs)
- [ ] Performance optimized
- [ ] Additional VMs cloned with new MAC addresses

---

**Success:** Each VM will appear as a separate computer to external systems, perfect for gaming promotions and referral programs.