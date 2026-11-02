# Network Packet Analyzer

A Python-based network packet analyzer that captures live network traffic using Scapy, identifies protocols, and stores packet logs in SQLite for analysis.

## Features

- Captures live network packets using Scapy
- Analyzes TCP, UDP, ICMP, and DNS packets
- Extracts source IP, destination IP, ports, and protocol information
- Logs every packet in an SQLite database
- Generates a traffic summary with protocol distribution and packet statistics

## Tech Stack

- Python 3
- Scapy
- SQLite
- Wireshark (for verifying results)

## Installation

1. Clone the repository:

```bash
git clone https://github.com/rahulkumar4002/network-packet-analyze.git
cd network-packet-analyze
```

2. Install the dependency:

```bash
pip install -r requirements.txt
```

On Windows, install [Npcap](https://npcap.com) first (installing Wireshark also installs it).

## Usage

Packet capture needs administrator rights.

```bash
sudo python3 analyzer.py
```

On Windows, run the terminal as Administrator and use `python analyzer.py`.

While the script runs, open a few websites or run `ping google.com` to generate traffic.

## Sample Output

```
DNS   192.168.1.5:54213 -> 8.8.8.8:53 www.google.com.
TCP   192.168.1.5:51822 -> 142.250.183.4:443
ICMP  192.168.1.5:None -> 142.250.183.4:None

--- Summary ---
TCP: 68 packets (68.0%)
UDP: 14 packets (14.0%)
DNS: 10 packets (10.0%)
ICMP: 8 packets (8.0%)
```

## How It Works

1. Scapy's `sniff()` captures packets from the network interface.
2. The `handle()` function checks each packet's layers (IP, TCP, UDP, ICMP, DNS).
3. Source and destination IPs, ports, and protocol are extracted.
4. Each packet is saved to the `packets` table in `packets.db`.
5. When capture ends, a protocol distribution summary is printed.

## Database Schema

| Column | Description |
|--------|-------------|
| id | Auto-increment ID |
| time | Capture timestamp |
| src | Source IP |
| dst | Destination IP |
| proto | TCP, UDP, ICMP, DNS or OTHER |
| sport | Source port |
| dport | Destination port |
| info | Extra info (e.g. DNS domain) |

## Future Improvements

- IPv6 and ARP support
- CSV export from the command line
- Filters by port or IP
- Alerts for suspicious traffic

## Author

Rahul Kumar
[GitHub](https://github.com/rahulkumar4002) | [LinkedIn](https://linkedin.com/in/rahul-kumar-1065621b5)
