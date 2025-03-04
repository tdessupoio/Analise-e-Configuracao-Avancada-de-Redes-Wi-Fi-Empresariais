# Advanced Wi-Fi Network Analysis and Configuration for Businesses
This document presents the records of the studies for a proposal to optimize the Wi-Fi network infrastructure, aiming to improve network performance, which currently uses **U6 Pro Devices** from UniFi Ubiquiti.

## Introduction
The buildings today use the **Wi-Fi 6 Access Point** mounted on the ceiling with 6 spatial streams, designed for large office environments.

Its characteristics are:
- **Wi-Fi 6**
- 6 spatial streams
- Coverage of 140 m² (1,500 ft²)
- More than 350 connected devices
- Powered using **PoE**
- Uplink **GbE** link

Looking at the layout for the new auditorium, it becomes clear that special attention must be given to the internet points. Based on this, the idea is to have a system focused on a **U6 PRO Access Point** and **U6 Mesh devices** that use mesh technology. This allows the creation of a Wi-Fi system formed by two or more devices (also called modules) that communicate with each other to form a single network. Mesh is a cutting-edge technology that ensures high-quality connection.

The **U6 Mesh** functions as an Access Point but with the Mesh function, making it more practical as it is an outdoor version designed to cover a larger area (usually used in parks or shopping malls). It has fewer **interferences** due to the physical barriers (walls, doors) than the U6 Pro, with its semi-outdoor version.

The biggest benefit of using this technology is **Resilience and Fault Tolerance**:

- Better tolerance to individual access point failures, as the mesh network can dynamically adjust traffic routing to maintain connectivity.
- Great for environments with **Interference** or where physical obstacles can affect coverage.

However, the **U6 Mesh** struggles to match the power of the **U6 PRO Access Point**, as the Pro offers high performance and low latency, while the mesh cannot achieve the same performance. For this reason, the **Access Point** is used to provide a stronger connection quality, but it does not address the **Interference** issues.

## Improving Connection with the U6 Pro
An analysis of the current network was conducted, and improvements can be made with just a few configuration changes to the APs:

- ### Band Steering
  **Band Steering** is a technique used in Wi-Fi networks to automatically steer compatible devices to the most appropriate frequency band, either 2.4GHz or 5GHz. This improves network performance and efficiency by balancing the load across the bands to optimize the user experience.
  Currently, the automatic setting was left as is, which has led to poor connections. The 2.4GHz band has a lot of competition and very few available channels, competing with devices like remote controls, Bluetooth mice, and microwaves. This band only has 3 **non-overlapping 20 MHz channels**.
  The 5GHz band offers more available channels, and a better path can be mapped to make the most of the connection. Therefore, **Band Steering** directs compatible devices to prefer the 5GHz band, relieving the load on 2.4GHz. The **AP** receives association and connection requests for both, resulting in a delay when connecting to machines.
  This practice improves both the 5GHz clients, which will automatically connect to the best band, and the 2.4GHz clients, which will have the band to themselves.

- ### Declaring Channels to Improve Extended Service Set (ESS)
  A WLAN can have multiple access points (APs) connected to each other through a distribution system to extend the coverage area, i.e., the geographical reach of the network.
  Each **AP** creates a cell (coverage area), and to allow clients to seamlessly switch between APs, roaming is used, which is a transparent transmission from one cell to another.

  ![image](https://github.com/user-attachments/assets/159c2091-b4c6-40bb-9320-ddf6e3843758)

  When the red client moves out of coverage, it will need to reassociate to connect with the green AP. Therefore, it must be ensured that no new associations are made, as the connection will be affected (the link will drop). This is why **Cells** are visualized overlapping each other, but in different colors.

  ![image](https://github.com/user-attachments/assets/c5982cf9-e143-44e4-9e89-21d0b246d0e9)

  In the example above, different colors indicate that **non-overlapping channels** should be used so that one cell doesn't cause **interference** in the neighboring cell.

  ![image](https://github.com/user-attachments/assets/0cd44ad5-e6c9-429e-b169-246dd3af345a)

  In this image, you can see that the Wi-Fi Matrix is competing with all these networks on channel 48 while many channels are free. By specifying this, the signal will stop competing.

- ## MinRSSI to Optimize **Roaming**
  When a cell is propagated from an AP, it will cover an area where the signal will extend up to a predefined limit, and it's common for devices to receive signals below **-75dBm**, which are very weak.

  ![image](https://github.com/user-attachments/assets/a6f6b1d4-71ae-4f90-a42a-48ff91ac2961)

  The larger the coverage area, the farther clients (in the blue area of the image) will be from the **AP**, and they will receive weaker signals. The client's device will understand that it needs to work with lower modulations, so the time slots used in the network will carry less information, where more could have been transmitted. More bits will be sent for processing, which negatively impacts clients near the center of the AP, causing delays in their connection.
  The purpose of using **MinRSSI** is to limit the cell's propagation area to a higher quality level. Once the client reaches the weak signal limit, it will automatically disconnect and search for a better signal in another cell.

## Conclusion
Based on this study, an area analysis in the building will be required, including floor plans for the lobby, second and third floors, and the common room.
Therefore, it's not possible to calculate the signal range without the floor plans to determine whether it's better to continue with the APs or switch to a Mesh system. Observing how it currently works, it's recommended to keep the APs and apply configurations like **Band Steering, Extended Service Set (ESS), and MinRSSI**, as these technologies will make the most of connection performance.
It is advisable to purchase a **U6 Mesh** device for testing the connection directly via cable, as it functions as an **AP** with mesh capabilities.

### References
[Free Ubiquiti UniFi Course](https://youtube.com/playlist?list=PLozhsZB1lLUO293mVoY_aqOpMKmTPRQ02&feature=shared)

[UniFi - Tutorials](https://youtube.com/playlist?list=PLA1dWf7UkJ8rGmdNWTH6LV8Rxwjow1ah-&feature=shared)

[Master Class: What is MESH in Wi-Fi?](https://youtu.be/VxI-pdhMG5Q?feature=shared)

[Understanding in Detail UniFi APs: Which UAP is Ideal for Each Type of Application?](https://medium.com/ubntbr/conhecendo-em-detalhes-os-aps-unifi-qual-o-uap-ideal-em-cada-tipo-de-aplica%C3%A7%C3%A3o-ff0d82da74a0)

[Which WiFi Setup DO YOU NEED? Router vs Access Point vs Mesh - WiFi 6E?](https://youtu.be/7_wftlWheac?feature=shared)

[Minimum RSSI: How to Set Client Signal Quality and Optimize Roaming on Wi-Fi Network?](https://medium.com/ubntbr/minimum-rssi-como-definir-a-qualidade-do-sinal-dos-clientes-e-otimizar-o-roaming-na-rede-wifi-8d590f2ab09)

[Understand Why to Change Your WiFi Channel](https://youtu.be/DPl_R68tBDI?feature=shared)

[5 Functions Every Corporate Network Should Have](https://youtu.be/G-_8TsbK27w?feature=shared)

[Wireless Uplink: How to Set Up a Mesh Wi-Fi Network in Difficult Cable Routing Areas](https://medium.com/ubntbr/wireless-uplink-como-montar-uma-rede-wifi-mesh-em-locais-de-dif%C3%ADcil-passagem-de-cabos-8d8beb2ef589)
