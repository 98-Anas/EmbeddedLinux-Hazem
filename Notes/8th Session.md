# 8th Session

- ## General Discussion of TCP/IP Stack Layers
    - User space --> Application Layer
    - Kernel Space --> [Network Stack] --> Transport Layer, Network Layer (L3,L4)
    - Device Drivers (Hardware) --> Network Access Layer (L1,L2)
> Important Command: `ifconfig` for general monitoring of info about our NICs and our device on the network
---
- ## Some sidetalk on SOMEIP and other protocols
    - In automotive idustry, we use SOMEIP [Based on TCP] for communication between ECUs wired on the network.
    - CAN was a message-oriented way of communication
    - SOMEIP is a service[event]-oriented way of communication <-- More modernS
    - But is SOMEIP a communication protocol ?
        - Yes, SOME/IP (Scalable service-Oriented MiddlewarE over IP) is a communication protocol designed for automotive Ethernet networks. It provides a middleware solution for service-oriented communication between different components within a vehicle. SOME/IP is used to facilitate communication between electronic control units (ECUs) in a car, enabling various vehicle functions such as infotainment, advanced driver-assistance systems (ADAS), and more.

            - Key features of SOME/IP include:

                - **Service Discovery**: SOME/IP provides a mechanism for discovering services and their availability within the network. This allows ECUs to dynamically find and communicate with each other.

                - **Serialization and Deserialization**: It defines a way to serialize and deserialize complex data structures, enabling efficient data exchange between different components.

                - **Reliable Communication**: SOME/IP supports reliable communication over Ethernet, ensuring that messages are delivered correctly and in the right order.

                - **Flexibility**: The protocol is designed to be flexible and scalable, accommodating a wide range of applications and use cases within the automotive industry.

    - **SOME/IP** is part of the AUTOSAR (AUTomotive Open System ARchitecture) standard, which aims to standardize software architecture and communication protocols in automotive systems.
---
- # Operations we can do on network stack
    - ## Monitoring & Configuration
        - `ifconfig` --> gives info about our Hardware, UP or NOT, gives if RUNNING. gives maximum mtu (maximum transmission units), gives IPV4 and IPV6 and it can config each one of them
            - What is **`Loopback`** in the output ?
        - `Network Manager` Configuration of Init Process (Systemd) --> https://www.clearlinux.org/clear-linux-documentation/guides/network/assign-static-ip.html
        - Use `sudo nmcli connection modify "DNS" ipv4.method manual ipv4.addresses "192.168.1.155/24" ipv4.gateway "192.168.1.1" ipv4.dns "8.8.8.8,8.8.4.4"` and restart NetworkManager using `Sudo systemctl restart NetworkManager` to assign **static ip address** to your device
        - Use `sudo nmcli connection modify "DNS" ipv4.method auto ipv4.addresses "192.168.1.155/24" ipv4.gateway "192.168.1.1" ipv4.dns "8.8.8.8,8.8.4.4"` and restart the NetworkManager using `Sudo systemctl restart NetworkManager`  to regain the **dynamic ip address**

---
- ## Extras
    - Simple fundamentals of networks crash course --> https://www.youtube.com/watch?v=S7MNX_UD7vY&list=PLIhvC56v63IJVXv0GJcl9vO5Z6znCVb1P
    - Full course on the book "Computer Networking: A Top Down Approach" --> https://www.youtube.com/watch?v=05FHPbC3Vag&list=PLy_2fgXkPiZuMaG9Jmp8PAwimIumf19hp
---