# NetWatch — Network Monitor & Threat Detection

NetWatch is a lightweight, real-time network monitoring and intrusion detection system. It features a modern web dashboard for visualizing network traffic, a custom threat detection engine using `scapy`, and an integrated Nmap scanner for host discovery and vulnerability assessment.

## Features
- **Live Packet Capture**: Captures network packets on a specified interface in real-time.
- **Threat Detection Engine**: Automatically detects anomalies and common attacks:
  - SYN Flood (DoS)
  - Ping Sweeps
  - Port Scans
  - ARP Spoofing
  - SSH Brute-force
  - DNS Abuse
  - Oversized Packets
- **PCAP Offline Analysis**: Upload existing `.pcap` or `.pcapng` files for fast historical threat analysis.
- **Network Scanner**: Integrated Nmap capabilities for subnet ping sweeps, port scanning, and service detection.
- **Dynamic Web Dashboard**: Real-time traffic visualization, live threat feed, and packet logging.

## Project Structure
```
.
├── backend/
│   ├── app.py              # Main Flask server entry point
│   ├── requirements.txt    # Python dependencies
│   ├── engine/             # Core logic (packet capture, threat detection, nmap scanning)
│   └── routes/             # API Endpoints
├── frontend/
│   └── index.html          # HTML/JS/CSS Web Dashboard
├── requirements.txt        # Root requirements file (mirrors backend)
└── README.md
```

## Prerequisites

- **Python 3.8+**
- **Nmap**: Must be installed on the host system.
  - MacOS: `brew install nmap`
  - Linux: `sudo apt install nmap`

## Installation

1. **Install Python dependencies:**
   It is highly recommended to install dependencies globally (or use `--break-system-packages` on newer MacOS/Linux) because packet sniffing with `scapy` requires `sudo` privileges.

   ```bash
   sudo pip3 install -r requirements.txt
   ```

## Usage

### 1. Start the Backend Server
Because capturing live network packets on raw sockets requires administrative privileges, you must run the backend script with `sudo`:

```bash
sudo python3 backend/app.py
```
*The API server will start on `http://127.0.0.1:5000`.*

### 2. Open the Dashboard
Simply double-click the `frontend/index.html` file to open it in your web browser. No separate web server is required for the frontend.

### 3. Run a Live Capture
- In the dashboard, enter your network interface (e.g., `en0`, `eth0`, or leave blank for auto).
- Click **Start Capture**.
- Live traffic will appear in the packet log, and threats will populate the threat feed.

### 4. Analyze an Offline PCAP
- Click the **📁 Upload PCAP** button.
- Select a `.pcap` or `.pcapng` file.
- The engine will rapidly analyze the file and display a dedicated Threat Report.

## Troubleshooting
- **No interface found/Permission Denied**: Ensure you are running `app.py` with `sudo`.
- **Nmap not found**: Ensure Nmap is installed and accessible in your system's PATH.
- **Blank UI when starting capture**: Ensure the Flask backend is reachable. You can test this by clicking "Ping API" in the dashboard.
