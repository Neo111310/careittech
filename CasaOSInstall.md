# CasaOS auf Ubuntu Installieren

**Here's a more detailed breakdown:**
Verify System Compatibility: Ensure your Ubuntu system is compatible with CasaOS. Ubuntu 20.04 LTS or later is recommended. 

Open a Terminal: Access the command line interface of your Ubuntu system. 
Update Ubuntu
```
sudo apt update
sudo apt upgrade
```

Install Curl
```
sudo apt install curl
```
Run the Installation Script: Execute the following command to download and run the CasaOS installation script: 
Code
```
sudo curl -fsSL https://get.casaos.io | sudo bash
```
This command uses curl to fetch the installation script from the CasaOS website and pipes it to sudo bash for execution with root privileges. 
1. Wait for Installation to Complete: The script will handle downloading necessary packages, setting up Docker, and installing CasaOS. This may take some time depending on your internet speed and system resources. 
2. Access CasaOS: Once the installation is complete, you can access the CasaOS web interface by opening a web browser and navigating to ***http://localhost*** or the IP address of your server followed by :8888. 
3. Create User Account: You will be prompted to create a username and password for your CasaOS account. 
4. Start Using CasaOS: After logging in, you can begin exploring the CasaOS interface and installing applications.


> Note: If you encounter any issues during installation, you can refer to the CasaOS documentation for troubleshooting or seek assistance from the CasaOS community. 
