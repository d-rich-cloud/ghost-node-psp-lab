# Ghost-Node PSP Lab

A small "field lab" project that turns an old PSP, a Raspberry Pi 5, and an Asus router into a portable pentest / AI assistant setup.

- **PSP** = HUD / field terminal (browser)
- **Raspberry Pi 5** = Brain (Flask app + AI)
- **Asus RT-AX92U** = Legacy WiFi bridge for the PSP
- **Note 8 / Fire Tablet** = C2 and monitoring displays

## Architecture

1. Asus router broadcasts a 2.4 GHz "legacy" WiFi network:
   - SSID: `GHOST_NODE_LAB`
   - 2.4 GHz only, 20 MHz channel width
   - Mode: Legacy / b/g compatible
   - Auth: WPA-Auto-Personal, TKIP+AES

2. Raspberry Pi 5 connects to this network (Ethernet or WiFi) and runs a Flask web app on port `5000`.

3. PSP connects to `GHOST_NODE_LAB` and opens the Pi's IP in its browser:
   - Example: `http://192.168.50.20:5000`

4. Note 8 and Fire Tablet also connect to `GHOST_NODE_LAB` to:
   - SSH into the Pi
   - View the same HUD in a modern browser
   - Run tools like Fing / Termius / Haven / Meshtastic

## Quick Start (once on the Pi)

Install dependencies:

```bash
sudo apt update
sudo apt install -y python3 python3-pip
pip3 install -r requirements.txt

