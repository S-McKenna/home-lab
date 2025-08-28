## Wireshark Micro-Lab — Aug 23, 2025

- Installed Wireshark 4.4.8 on Windows with Npcap 1.8.

- Ran first capture on Wi-Fi while browsing. Other users on home wifi. Son playing Minecraft, Daughter watching streaming on smart TV.

- Applied filters: `dns`.

- Screenshot: `wireshark-first-capture.png`
  
![First capture](https://github.com/S-McKenna/home-lab/blob/212da12fdf0eb94098feb725dd875b72527d39c5/labs/wireshark/Wireshark-first-capture.png)


## Wireshark Micro-Lab — Aug 27, 2025
- Objective: Follow a TCP stream to observe a browser session flow.
- Steps:
  - Opened Wireshark on Wi-Fi adapter and captured traffic while browsing [EDHRec](https://edhrec.com).
  - Selected a TCP packet → **Follow → TCP Stream**.
  - Observed conversation in stream index `tcp.stream == 5`.
  - Applied display filter `tcp.stream == 5` to isolate packets.

### Screenshots
**Follow TCP Stream Window**  
![Follow TCP Stream Window](https://github.com/S-McKenna/home-lab/blob/1ad19ead2a5e96d9b1d4403a548a13497b55c0b9/labs/wireshark/Wireshark-TCP-Stream.png)

**Filtered Packet List (`tcp.stream == 5`)**  
![Filtered TCP Stream Packets](https://github.com/S-McKenna/home-lab/blob/1ad19ead2a5e96d9b1d4403a548a13497b55c0b9/labs/wireshark/Wireshark-TCP-Stream%205.png)

### Notes
- Stream contents appeared as encrypted TLS traffic (expected with HTTPS).
- Demonstrates ability to trace a specific connection end-to-end using Wireshark.

