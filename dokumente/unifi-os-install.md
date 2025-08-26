# Unifi OS Installation

https://community.ui.com/releases/UniFi-OS-Server-4-2-23/21df94e9-55d6-4298-b849-fbef3e3b1dd6

UniFi OS Server 4.2.23\
Created a month ago\
Last activity: 21 minutes ago\
Overview\
UniFi OS Server allows users to run the full UniFi OS experience on their own Windows, macOS, or Linux hardware. Initially, it will support the UniFi Network and InnerSpace application.

 

Benefits of UniFi OS Server (Compared to Self-Hosting Only the Network Application)

Opting for a UniFi OS Server provides several advantages over simply running the standalone UniFi Network application:

Full UniFi OS Experience: Enjoy the comprehensive and unified UniFi OS interface, providing a consistent management experience similar to that found on official UniFi Consoles.\
Future-Proof Platform: Built on the UniFi OS foundation, this self-hosted solution is better positioned to support new features, updates, and upcoming UniFi applications, offering greater extensibility.\
Unified Updates: Manage updates for the underlying UniFi OS and its applications through a more integrated process.
 

System Requirements

Storage:\
Minimum: 20GB of free disk space.\
Software Dependencies: \
The UniFi OS Server installer will typically include necessary dependencies or guide you through their setup.\
On Linux - Podman 4.3.1 or higher.\
On Windows - WSL (Windows Subsystem for Linux) version 2 - installed during setup.\
Ports used:\
3478, 5005, 5514, 6789, 8080, 8444, 8880, 8881, 8882, 9543, 10003, 11443.
 

Bundled Application\

UniFi Network 9.3.43\
Known issues\
UOS Server Updates: Updates for the Linux UOS Server are currently non-functional, whether initiated from the control plane or the application menu.\
Network Application Status: For up to a minute, the Network application may display a "setup" state even when it is fully functional.\
Windows Upgrades: On Windows, upgrades initiated from Site Manager via remote access require the application to be launched with Administrator privileges.

