# Network Layers and Protocols (7-Layer OSI Model)

| Layer | Name           | Protocols                                              | Data Unit     | Function                                               |
|-------|----------------|----------------------------------------------------------|---------------|--------------------------------------------------------|
| 7     | Application    | HTTP, HTTPS, FTP, DNS, SMTP, SSH, Telnet, SNMP        | Data          | Provides services to applications (user interface)     |
| 6     | Presentation   | SSL/TLS, ASCII, JPEG, MPEG                              | Data          | Data formatting, encryption, compression              |
| 5     | Session        | NetBIOS, RPC,  NFS                                      | Data          | Establishes, manages, and terminates sessions          |
| 4     | Transport      | TCP, UDP                                                | Segment (TCP) / Datagram (UDP) | End-to-end communication, reliability, flow control   |
| 3     | Network        | IP (IPv4, IPv6), ICMP, ARP, Routing Protocols           | Packet        | Logical addressing and routing                         |
| 2     | Data Link      | Ethernet (802.3), Wi-Fi (802.11), PPP                  | Frame         | Error-free transmission over a single link            |
| 1     | Physical       | Ethernet (physical signaling), Wi-Fi (radio waves)     | Bits          | Physical transmission of bits                         |


**Data Units:**

* **Data (Application, Presentation, Session):** This is the information that applications want to exchange.
* **Segments (Transport - TCP):** TCP divides the data into segments and adds headers for reliable transmission.
* **Datagrams (Transport - UDP):** UDP encapsulates data into datagrams with a simpler header.
* **Packets (Network):** IP encapsulates segments or datagrams into packets, adding IP addresses.
* **Frames (Data Link):**  Data link protocols (like Ethernet) encapsulate packets into frames, adding MAC addresses.
* **Bits (Physical):** Frames are converted into a stream of bits for transmission.


