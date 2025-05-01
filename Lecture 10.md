# (5/1/25) Wireless Comunication.ppxt

## Things I'm confused about 

## After class TODO

## Notes 

Fundamentals
- Carrier Frequency
  - Central band
  - For WiFi: 2.4 GHz
- Modulation = Data
  - Audio range is 20 Hz to 20 KHz
  - Fault tolerance and throughput
- Transmission / Reception Power
  - Range and sensitivity
- Channel
  - Interference and capacity

Abbreviations
<br/> <img width="520" alt="Screenshot 2025-05-01 at 8 59 25 AM" src="https://github.com/user-attachments/assets/2eb5b161-1d24-4607-969d-66d835bbd49d" />
<img width="475" alt="Screenshot 2025-05-01 at 9 14 39 AM" src="https://github.com/user-attachments/assets/f87a90eb-0cee-4b8b-8f13-a023e05fce82" />


IEEE 802 Working Groups
- 802.2: Logical Link Control
- 802.3: Ethernet
- 802.11: Wi-Fi
- 802.15: Wireless Personal Area Network
  - 802.15.1: Bluetooth
  - 802.15.4: Low-Rate Wireless PAN, e.g., ZigBee
- The services and protocols specified in IEEE 802 map to the lower two layers (Data Link and Physical) of the seven-layer OSI networking reference model
- IEEE 802 splits the OSI Data Link Layer into two sub-layers named Logical Link Control (LLC) and Media Access Control (MAC)



IEEE 802 LAN protocols
- 802.11 is the wireless LAN section
  - media access control (MAC)
  - physical layer (PHY) protocols
  - wireless local area network (WLAN) Wi-Fi communication
- WLAN has evolved over time


Wi-Fi, Bluetooth, and ZigBee
<br/> <img width="648" alt="Screenshot 2025-05-01 at 9 05 16 AM" src="https://github.com/user-attachments/assets/71b7ca56-58fc-42a1-a935-fc2d8f7ecf73" />


Wi-Fi Infrastructure
<br/> <img width="606" alt="Screenshot 2025-05-01 at 9 15 16 AM" src="https://github.com/user-attachments/assets/6453be7c-ec9d-4772-9a88-a48188693fdc" />

Wi-Fi Direct
- Both Ad-hoc mode and Wi-Fi Direct allow devices to connect directly to each other (P2P), without the use of an Access Point
- Wi-Fi Direct is a protocol for forming hierarchical groups, and mostly used to connect just two devices
  - It does not scale beyond a few devices in close proximity
- The devices are only equal peers until they connect to each other, and one of them becomes group owner
- After establishment of connection, both devices follow the hierarchical roles of AP and client – master and slave


Comparison between Wi-Fi Direct (P2P) and Ad-hoc (IBSS) mode
<br/> <img width="507" alt="Screenshot 2025-05-01 at 9 22 38 AM" src="https://github.com/user-attachments/assets/3e7fa7fa-afa7-444e-87dc-2a554866e0d6" />

Wi-Fi Packet Structure
<br/> <img width="530" alt="Screenshot 2025-05-01 at 9 25 25 AM" src="https://github.com/user-attachments/assets/5ac41c25-08ae-41b7-85e4-bf78e4204f79" />

Wi-Fi Data and NetworkManagement Packets
<br/> <img width="563" alt="Screenshot 2025-05-01 at 9 26 23 AM" src="https://github.com/user-attachments/assets/df3a7269-b10c-489f-a5b4-7f93f59504d5" />

Wi-Fi Control Packet Header
<br/> <img width="553" alt="Screenshot 2025-05-01 at 9 27 45 AM" src="https://github.com/user-attachments/assets/8e09c4da-ef69-4cad-809b-43e245e2ec28" />

Wi-Fi Power Saving Mode
- Constantly Awake Mode – CAM
  - This is how most WLANs are operated today, with power-saving features disabled
- Power Save Mode – PSM
  - Mobile devices suspend radio activity after a variable but pre-determined (by the vendor) period of inactivity, and then wake up periodically (usually about three beacon frames) to see if the infrastructure (AP) has queued any traffic for it

Reception of Packets in PSM mode
- AP buffers packets for sleeping nodes
- AP announces which nodes have data buffered in its periodical Beacons (100ms by default) with TIM
- Sleeping nodes wake up to listen to the beacon
- If  there is data buffered for the node, this node sends a poll frame to get the buffered data
- In the data, there is a “more data” flag to tell the node if there is more data to be retrieved  don’t sleep!


What is Bluetooth?
- Bluetooth is a standardized technology that is used to create temporary (ad-hoc) short-range wireless communication systems
- Features
  - Short Range – Typically a few meters but can go up to approximately 100 meters in a open environment
  - Dynamically Created – Bluetooth devices find and setup temporary (ad-hoc) connections (small networks) with other devices
  - Mix of Service Types – Mixture of services such as device control (e.g. mice and keyboard), voice (e.g. headsets), and video (e.g. web cam) can share the same ad-hoc connections


BLuetooth Versions
<br/> <img width="520" alt="Screenshot 2025-05-01 at 9 35 47 AM" src="https://github.com/user-attachments/assets/bae84c4b-6fa1-413b-9445-8d1ba55dea5e" />

BT Abbreviations
<img width="460" alt="Screenshot 2025-05-01 at 9 36 20 AM" src="https://github.com/user-attachments/assets/99b539fd-ab6a-40e7-ad72-c70a7318e69b" />

Core Technology in Bluetooth
- Frequency Hopping: Uses a simple frequency hopping system which has low interference levels
  - 79 channels for Bluetooth Classic (1MHz spacing)
  - 40 channels for BLE (2MHz spacing)
  - Hopping sequence is determined by the master device
- Service Discovery: Dynamically find the capabilities and services offered by nearby Bluetooth devices
- Modulation Types
  - Originally, Frequency Shift Keying (FSK) modulation
  - Additional, Phase Shift Keying (PSK) modulation
    - To increase the data transmission rate

Bluetooth Address
- Globally Unique 48-bit address (BD_ADDR)
  - Upper 24 bits: Organization Unique Identifier (OUI) identifies the manufacturer
    - 16-bits: Non-significant Address Part (NAP)
    - 8-bits: Upper Address Part (UAP)
    - NAP + UAP: Organization Unique Identifier (OUI)
  - Lower 24-bits: unique part of the address – device specific
    - Assigned by manufacturer
- Bluetooth devices can also have user-friendly names given to them
  - Can be up to 248 bytes long, and two devices can share the same name
  - The unique digits of the address might be included in the name to help differentiate devices

Bluetooth Profiles
<img width="594" alt="Screenshot 2025-05-01 at 9 44 07 AM" src="https://github.com/user-attachments/assets/c4101c16-e6ca-484c-a352-6cccd6d249aa" />




