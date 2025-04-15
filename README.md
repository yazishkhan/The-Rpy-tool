# 📡 The Rpy Tool – Raspberry Pi 4 Access Point Router
#### Created by: [Yazish Khan](https://www.linkedin.com/in/yazish-khan-3634752b7?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app)

The Rpy Tool transforms a Raspberry Pi 4 into a secure home router and network monitor. It acts as a middle-man between your internet connection and connected devices, making it ideal for:


- I make this Project to More Secure my home Network. It turns a Raspberry pi 4 into a router.
- Then it becomes a middle-man between the internet and my connected Devices.
- This helps in :
 
    🕵️ Web/App penetration testing

    🔍 API traffic and backend request analysis

    📡 Real-time network monitoring and packet capture

    🎭 Testing Man-in-the-Middle (MITM) scenarios

    🔧 Building various home cybersecurity tools


- It can use in different-different ways by using various tools in respberry pi 4

## ⚠️ Disclaimer

This tool is for EDUCATIONAL and PERSONAL HOME NETWORK monitoring only.
Do NOT use this tool on networks you do not own or have explicit permission to monitor.
Misuse can be illegal and is not supported or encouraged by the developer.
Use responsibly and ethically.


## 💡 How it Works 
 - Connect Ethernet with internet access to your Pi.

 - Pi creates an Access Point using its built-in Wi-Fi adapter.

 - Connect your devices to this new AP.

 - All traffic passes through the Pi, allowing full monitoring & control.

## 🧰 Requirements

- Raspberry Pi 4
- SD card of 32gb 
- Ethernet cable
- 18w Power supply to power the Pi

## 🛠️ Software setup

- Download [Pi imager](https://www.raspberrypi.com/software/)
- Install imager
- Prepare the sd card inside the reader and plug it to laptop.
- Open pi imager > Choose device : Raspberri pi 4 B
- Choose os : Raspberry pi 64bit full version
- Choose storage : mounted sd card is already there select it.
- And flash the image.

## 🛠️ Hardware setup

- Insert the sd card on Pi.
- Insert the Ethernet cable having internet access. 
    modem from (ISP)/Router > Raspberry pi 4.
- Connect Display and mouse. 
- Boot the Pi (it takes time while booting for a first time).

## 📦 Packages Used

- `hostapd`
- `dnsmasq`
- `iptables-persistent`
- `netfilter-persistent`
- `dhcpcd5`

## 📜 How to Use The Rpy tool

1. Now we have an GUI screen of Pi Os on Monitor Display. 


2. Open terminal and clone the git repository.

   ````bash
     git clone https://github.com/yazishkhan/The-Rpy-tool.git
   ````


3. There is an Script named `APYsetup.sh`

4. (optional) You can Change the SSID and PASSWARD of Pi AP before executing the script. 
    ````bash
        nano APYsetup.sh
    ````

    ![Image](https://github.com/user-attachments/assets/2969f8c8-bc69-4543-8ee4-5e7fec0b8fd7)

    - `ssid=Pi_Ap` Replace Pi_AP the name you have to give to your AP
    - `wpa_passphrase=raspberry123` Replace rasperry123 with Password you want to give.


4. Before executing the script Run this following commands.
    ⚠️ make sure the Ethernet cable is connected to pi and it able to access internet before executing these commands. 

    ```bash
        sudo apt purge network-manager wicd
        sudo systemctl disable wpa_supplicant
    ````


5. Give an Executable permission to Script and Execute it.
    ````bash
        chmod +x APYsetup.sh
        ./APYsetup.sh
    ````
6. The script will execute and it takes an time as per internet speed and RAM variant.
    - When the script is successfully executed reboot the system it will take 5-10 minuets.
    - After rebooting it Switches automatically to CLI mode which does not affect anything. 
7. In your mobile search for Wifi You can See `Pi_Ap` connect it.
    
    - Password = `respberry123`
    - Now the all connected devices can access the internet via reapberry pi.
    - Now it is an Mid-point of connected device to internet. 
    - We can monitor everything by Setting-up multiple tools on pi.


## 🌐 Installing and Run tcpdump to monitor Network queries

- In CLI mode run these command to install and run the tcpdump tool
   
    ````bash
        sudo apt update
        sudo apt install tcpdump -y
    ````
- This command will show which domain each device is requesting

    ````bash
        sudo tcpdump -i wlan0 udp port 53 -n
    ````
- To catch simple web traffic (unencrypted HTTP)
    ````bash
        sudo tcpdump -i wlan0 tcp port 80 -n
    ````
- Capture all traffic going through the AP interface
    ````bash
        sudo tcpdump -i wlan0 -n
    ````

## 💡 if we need to capture the single devices network we need to know it's ip for give it to tcpdump

## 🛠️ The tool we need to use for knowing the connected devices/Clint ip's is:
### `arp-scan`
- installation 

    ````bash
        sudo apt install arp-scan
    ````
    The ip must be same as per the script so just copy and past this command.

- Finding connected devices ip

    ````bash
        sudo arp-scan --interface=wlan0 192.168.4.0/24
    ````

- It will show Result like:

    ````bash
        192.168.4.2  aa:bb:cc:dd:ee:ff  Apple Inc
        192.168.4.3  xx:yy:zz:aa:bb:cc  Samsung
    ````

- Copy the ip Which single device network you have to monitor.
    Replace the `192.168.4.29` with your Device ip `xxx.xxx.x.xx`

    ````bash
        sudo tcpdump -i wlan0 udp port 53 and host 192.168.4.29 -n
    ````
- Now we can monitor the single device network queries.


👨‍💻 Author

Yazish Khan 
📧 yazishkhan7@gmail.com
🌍 DevOps & Cybersecurity Enthusiast

# The-Rpy-tool
# The-Rpy-tool
