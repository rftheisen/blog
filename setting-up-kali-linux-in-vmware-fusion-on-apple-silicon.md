# Setting Up Kali Linux in VMware Fusion on Apple Silicon

***

If you are getting into cybersecurity, penetration testing, or just want a dedicated environment to learn and experiment with security tools, Kali Linux is the go-to distribution. In this guide, I'll walk you through setting up a Kali Linux VM in VMware Fusion on an Apple Silicon Mac. This is one of the first things I recommend setting up when building out your home lab on a Mac.&#x20;

***

### What You'll Need

Before we get started, make sure you have the following:&#x20;

* An Apple Silicon Mac (M1, M2, M3, M4 or newer)
* VMware Fusion installed (the free Personal Use version works great)
* The Kali Linux ARM64 installer ISO

If you don't have VMware Fusion yet, you can download it from Broadcom's website. Since Broadcom acquired VMware, the download process has changed a bit. You'll need to create a Broadcom account, then navigate to the VMware Fusion download page. The Personal Use license is free.&#x20;

For the Kali ISO, head over to the official Kali downloads page and grab the **Installer** image for **ARM64**. Since we are on Apple Silicon, we need the ARM64 version. Do not download the AMD64 version, that is for Intel-based systems.&#x20;

***

### Creating the Virtual Machine

Once you have VMware Fusion installed and the Kali ISO downloaded, follow these steps:&#x20;

1. Open VMware Fusion
2. Go to **File → New** (or click the **+** button)
3. Select **Install from disc or image**
4. Click **Use another disc or image** and browse to your downloaded Kali ISO
5. VMware will try to auto-detect the OS. It may detect it as Debian, which is fine since Kali is Debian-based
6. Click **Continue**

When VMware asks you to choose the operating system, select:&#x20;

* **Linux** → **Debian 12.x ARM**

Kali is built on top of Debian, so this is the closest match. Don't worry if the exact Debian version doesn't perfectly align. This setting mainly just affects the default VM hardware profile, not the actual installation.&#x20;

***

### Configuring VM Settings

Before you start the installation, I recommend adjusting the VM settings. You can do this by clicking **Customize Settings** before the first boot. Here are my recommended settings:&#x20;

| Setting | Recommended Value |
| ------- | ----------------- |
| RAM | 4 GB minimum (8 GB if you can spare it) |
| CPU Cores | 2 or more |
| Disk Size | 80 GB |
| Network | NAT (default) |

A few notes on these settings:&#x20;

* **RAM** - Kali's desktop environment (Xfce by default) runs pretty lean but if you plan on running resource-heavy tools or multiple services, give it more RAM
* **Disk** - 80 GB gives you plenty of room for tools and wordlists. VMware uses thin provisioning by default, so it won't actually consume 80 GB on your Mac right away
* **Network** - NAT is the safest default. It lets your VM access the internet through your Mac's connection. If you need the VM to appear as a separate device on the network (useful for pentesting labs), switch to **Bridged** mode later

***

### Installing Kali Linux

Now for the fun part. Boot up the VM and you should see the Kali installer boot menu.&#x20;

1. Select **Graphical Install**
2. Choose your language, location, and keyboard layout
3. Set a **hostname** (e.g., `kali`)
4. When asked for a domain name, you can leave it blank
5. Set up your **user account** and **password** (remember these, you'll need them to log in)
6. For disk partitioning, select **Guided - use entire disk**
7. Choose **All files in one partition** (recommended for new users)
8. Confirm the partition changes and select **Yes** to write changes to disk
9. The installation will begin copying files. This may take a little while
10. When asked about software selection, keep the defaults. The **Xfce desktop** and **standard system utilities** are a great starting point
11. Install **GRUB** to the primary disk when prompted
12. Finish the installation and let it reboot

After the reboot, you should be greeted with the Kali Linux login screen. Log in with the username and password you set during installation.&#x20;

***

### Post-Installation Setup

After your first login, open a terminal and run the following commands to get your system fully up to date and install VMware's guest tools for a better experience:&#x20;

```bash
# Update the package lists and upgrade all packages
sudo apt update && sudo apt full-upgrade -y

# Install open-vm-tools for VMware integration
sudo apt install -y open-vm-tools-desktop

# Reboot to activate the tools
sudo reboot
```

The `open-vm-tools-desktop` package gives you some really nice quality of life features:&#x20;

* **Auto screen resizing** - The VM display will resize when you resize the window
* **Clipboard sharing** - Copy and paste between your Mac and the VM
* **Drag and drop** - Move files between your Mac and the VM
* **Shared folders** - Access Mac folders from within Kali

***

### Take a Snapshot

This is a step I always recommend. Before you start installing additional tools or making changes, take a snapshot of your clean installation:&#x20;

1. Go to **Virtual Machine → Snapshots** (or press **Command + Shift + S**)
2. Click **Take Snapshot**
3. Name it something like "Clean Install"

This gives you a restore point you can always come back to if something breaks or you want to start fresh without reinstalling.&#x20;

***

### Tips and Next Steps

Now that you have Kali up and running, here are some tips:&#x20;

* **Shared Folders** - Enable via **Virtual Machine → Settings → Sharing** to easily pass files between your Mac and Kali
* **Bridged Networking** - Switch from NAT to Bridged if you want the VM on your actual network. This is useful for practicing with tools like Nmap and Responder in a lab environment
* **Explore the tools** - Kali comes loaded with security tools. Open the Applications menu and browse through the categories to see what's available
* **Practice legally** - Set up vulnerable VMs like DVWA, Metasploitable, or sign up for Hack The Box to practice your skills in a legal and ethical way

Building a Kali VM is one of the most practical first steps you can take in your cybersecurity journey. It gives you a dedicated environment to learn, break things, and build your skills without affecting your main system. If you found this guide helpful and want more lab setup content, feel free to connect with me on Discord. I'd love to hear about what you're building.&#x20;

Keep learning!
