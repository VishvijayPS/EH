# Experiment 1: Network Traffic Capture and Analysis Using Wireshark

## Aim
To capture and analyze network traffic using Wireshark and gain hands-on experience with the OSI model and TCP/IP protocol suite.

## Objective
- Understand the basics of network packet analysis.
- Capture live network traffic using Wireshark.
- Identify source IP, destination IP, protocols, packet length, and timestamps.
- Analyze TCP, DNS, and ICMP packets using display filters.
- Understand how network communication works.
- Save captured network traffic in `.pcapng` format for future analysis.

## Tool Used
**Wireshark** – An open-source network protocol analyzer used to capture and inspect packets transmitted over a network.

Official website: https://www.wireshark.org/

## Introduction
Wireshark is a network protocol analyzer that allows users to capture and examine network packets in real time. It provides detailed information about network communication, including source and destination addresses, protocols, packet lengths, and other packet details.

Wireshark is widely used in network troubleshooting, cybersecurity, ethical hacking, and digital forensics.

## Requirements
- Windows or Kali Linux operating system
- Wireshark installed on the system
- An active Wi-Fi or Ethernet connection
- Internet connection (optional for offline packet analysis)

## Procedure

### Step 1: Install and Open Wireshark
1. Download Wireshark from the official website: https://www.wireshark.org/download.html
2. Install Wireshark by following the installation instructions.
3. Open Wireshark.

On Kali Linux, you can install it using:

```bash
sudo apt update
sudo apt install wireshark -y
```

Launch Wireshark:

```bash
wireshark
```

### Step 2: Select a Network Interface
1. Open Wireshark.
2. Identify the active network interface, such as Wi-Fi, Ethernet, or a wireless interface.
3. Double-click the active interface to start capturing packets.

### Step 3: Generate Network Traffic
1. Open a web browser.
2. Visit a website or perform a normal internet activity.
3. Return to Wireshark and observe the captured packets.

Only capture traffic on networks and devices you own or have permission to analyze.

### Step 4: Observe Captured Packets
The packet list displays information such as:

| Field | Description |
|---|---|
| No. | Packet number |
| Time | Time the packet was captured |
| Source | Sender's IP address or hostname |
| Destination | Receiver's IP address or hostname |
| Protocol | Protocol used for communication |
| Length | Size of the packet |
| Info | Brief description of packet activity |

### Step 5: Inspect Individual Packets
1. Select any packet from the packet list.
2. Examine the Packet Details pane.
3. Expand the relevant protocol sections.
4. Observe the Ethernet, IP, TCP, UDP, DNS, or ICMP fields, depending on the selected packet.

### Step 6: Apply Display Filters
Enter the following filters in the display filter bar and press Enter.

**Display TCP packets:**

```text
tcp
```

**Display DNS packets:**

```text
dns
```

**Display ICMP packets:**

```text
icmp
```

**Display UDP packets:**

```text
udp
```

**Display HTTP packets:**

```text
http
```

**Display traffic to or from a particular IP address:**

```text
ip.addr == 192.168.1.10
```

Replace `192.168.1.10` with an IP address relevant to your capture.

Note: Display filters only change which captured packets are shown; they do not delete packets from the capture.

### Step 7: Analyze the Packets
1. Apply different display filters.
2. Observe the protocols involved in the captured communication.
3. Compare the source and destination addresses.
4. Inspect packet lengths and timestamps.
5. Examine TCP connection activity and DNS queries where available.
6. Record your observations.

The packets displayed depend on your network activity. Some protocols may not appear in every capture.

### Step 8: Stop the Capture
Click the red **Stop** button on the Wireshark toolbar to stop capturing packets.

### Step 9: Save the Capture File
1. Click **File → Save As**.
2. Select a destination folder.
3. Enter a filename, for example:

```text
experiment1_capture.pcapng
```

4. Save the file in `.pcapng` format.

The saved capture can be reopened in Wireshark for future analysis.

## Important Display Filters

| Protocol / Purpose | Display Filter |
|---|---|
| TCP | `tcp` |
| UDP | `udp` |
| DNS | `dns` |
| ICMP | `icmp` |
| HTTP | `http` |
| HTTPS / TLS | `tls` |
| IPv4 traffic | `ip` |
| IPv6 traffic | `ipv6` |
| ARP | `arp` |
| Traffic for an IP address | `ip.addr == 192.168.1.10` |

## Sample Observation Table

| Sl. No. | Protocol | Source | Destination | Observation |
|---|---|---|---|---|
| 1 | DNS | Local system | DNS resolver | DNS query or response observed |
| 2 | TCP | Local system | Remote host | TCP communication observed |
| 3 | UDP | Local system | Remote host | UDP packet observed |
| 4 | ICMP | Depends on the test | Depends on the test | ICMP packet observed, if generated |

*This is a sample format. Record actual values and observations from your own capture.*

## Result
Network traffic was captured and analyzed successfully using Wireshark. Different network protocols were examined using display filters, individual packet details were inspected, and the captured traffic was saved in `.pcapng` format for future reference.

## Conclusion
This experiment provided practical knowledge of network packet capture and analysis. It helped demonstrate how Wireshark can be used to inspect network protocols, understand TCP/IP communication, and support network troubleshooting and cybersecurity investigations.

## Learning Outcomes
- Learned how to capture live network traffic.
- Understood the information displayed in packet lists.
- Practiced applying Wireshark display filters.
- Examined packet headers and protocol details.
- Learned to save and reopen packet capture files.
- Gained introductory experience with network analysis.

## Safety and Ethical Guidelines
- Capture traffic only on networks and devices you own or are authorized to test.
- Do not collect or share other people's private network data.
- Store packet captures securely because they may contain sensitive information.
- Use the experiment for educational, troubleshooting, and authorized security testing purposes.

## References
- Wireshark Official Website: https://www.wireshark.org/
- Wireshark User's Guide: https://www.wireshark.org/docs/wsug_html_chunked/
- Wireshark Display Filter Reference: https://www.wireshark.org/docs/dfref/
