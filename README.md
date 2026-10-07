# WarDriving-and-Cybersecurity
# Complete Beginner’s Walkthrough: Wardriving for Learning Wireless Security

This guide pulls together everything we’ve discussed into one practical path. It is written for someone new to the hobby who already knows basic Linux and networking, drives regularly, and lives in the United States. 

The goal is twofold:
1. Start a fun mapping hobby.
2. Use the activity as a hands-on way to learn real-world wireless security concepts.

---

## 1. What Wardriving Actually Is

Wardriving is the act of moving through an area (usually by car) while passively listening to Wi-Fi networks (and often Bluetooth devices) that are broadcasting their presence. You record:
- **SSID:** Network name
- **BSSID:** Unique hardware MAC address
- **Channel**
- **Encryption Type**
- **Signal Strength (RSSI)**
- **GPS Coordinates**

It is simply listening to public radio beacons that every access point sends out roughly ten times per second. **Nothing is transmitted toward the networks, no passwords are attempted, and no traffic is intercepted.** Variations exist for walking, biking, etc., but driving is the most common starting method.

> **Historical Context:** The practice originated from “wardialing” in the 1983 movie *WarGames* and was formalized with GPS mapping around 2000–2001 by researcher Peter Shipley.

---

## 2. How It Relates to Cybersecurity (and Why It’s Valuable for Learning)

Wardriving sits at the **reconnaissance layer** of wireless security.

* **Defenders and Researchers:** Use it to understand the actual wireless landscape: how many networks still use weak or no encryption, how dense 2.4 GHz vs 5 GHz coverage is, how often default SSIDs appear, and where signal leakage occurs.
* **Attackers:** Historically used the same passive data for target selection.

By doing it yourself, you gain direct, observable experience with:
- **Real-world encryption distribution:** Open, WEP remnants, WPA2, WPA3.
- **Hidden SSIDs:** Observing how they suppress the SSID name yet still reveal their BSSID.
- **Channel congestion and signal propagation:** Attenuation through buildings, foliage, and vehicles.
- **Spectrum dynamics:** The difference between 2.4 GHz (longer range, more interference) and 5 GHz (shorter range, cleaner spectrum).
- **Telemetry accuracy:** How GPS lock, accuracy, and vehicle movement speed affect captured data quality.

This knowledge transfers directly to understanding wireless risk, site surveys, and defensive hardening. It is one of the most accessible ways to move from theoretical concepts to real radio-frequency observation.

---

## 3. Legality in the United States (Critical)

> [!WARNING]
> **Passive scanning and logging of publicly broadcast beacon frames is generally legal.** 
> Connecting to a network without authorization, capturing the content of traffic (payloads), transmitting deauthentication frames to disconnect clients, or attempting to crack passwords is **illegal** under the Computer Fraud and Abuse Act (CFAA) and related state/federal laws.

* **Stay strictly passive:** Listen only.
* **Upload only metadata:** SSIDs, BSSIDs, signal levels, and coordinates.
* **Treat every network as belonging to someone else.** 

This guide and all recommended tools stay firmly on the legal side of that line.

---

## 4. The Main Platforms You’ll Use

| Platform | Primary Purpose | Key Features |
| :--- | :--- | :--- |
| **[WiGLE.net](https://wigle.net)** | Global Database & Mapping | Long-standing global repository. Upload logs, inspect coverage heatmaps, compete on leaderboards, and join teams (e.g., Nerd Sec). Official Android app is the simplest zero-cost starting point. |
| **[WDGWars](https://wdgwars.pl)** | Gamified Territory Control | *"Watch Dogs Go Wars"* — teams claim real-world map cells by scanning them. Features points, badges, gangs, bounties, and leaderboards. Ingests standard WiGLE-format CSV files; many modern microcontrollers support direct/one-tap uploads. |
| **[Wardrift](https://wardrift.net)** | RPG Layer & Progression | Newer cybersecurity-themed RPG utilizing passive scan logs for character progression, factions, exploration, and privacy awareness. Complements WiGLE and WDGWars. |

*Most practitioners upload the same session CSV file to both WiGLE and WDGWars. Wardrift is optional once you have logged a few baseline drives.*

---

## 5. Step-by-Step Getting Started Path

### Day 1 – Zero Cost
* [ ] Create free accounts on [wigle.net](https://wigle.net) and [wdgwars.pl](https://wdgwars.pl).
* [ ] Install the official **WiGLE WiFi Wardriving** app on an Android phone *(iOS sandbox restrictions make passive Wi-Fi scanning far more limited)*.
* [ ] Enable GPS, start a run, and drive normally for 20–30 minutes.
* [ ] Export and upload the results. Review the map layout and encryption breakdown in your dashboard.

---

### Week 1 – First Dedicated Hardware *(Recommended First Purchase)*
Move to a dedicated dual-band logger so you capture modern 5 GHz broadcasts alongside legacy 2.4 GHz signals without tying up your phone.

#### Top Recommended Beginner Hardware
* **Biscuit Ecosystem (Biscuit Pro, Biscuit Ultra, or DIY Biscuit):**
  * Simplest setup, native auto-upload, excellent for beginners and experts alike, supports multi-node clustering.
* **LILYGO T-Dongle C5 (flashed with Biscuit firmware):**
  * Ultra-compact, low-cost dual-band USB form factor.
* **Just Call Me Coco’s Ecosystem:**
  * Marauder Mini V3, Marauder V8, or dedicated C5 War Driver (robust firmware with auto-upload support for WiGLE and WDGWars).
* **Piglet (Midwest Gadgets):**
  * Compact open-source build featuring a Seeed Studio XIAO board, display, ATGM336H GPS module, and MicroSD logging.

> **Budget Target:** ~$40–$80 total (including a small USB power bank). Plug it into a 12V car socket or power bank, leave it on the dashboard, and drive.

---

### Next Level – Linux-Native Deeper Learning *(Leverages Existing Skills)*
Build a modular, headless or mobile Raspberry Pi rig running **Kismet**:

* **SBC:** Raspberry Pi 5 (or Pi 4 / Zero 2 W)
* **Radio:** Dual-band USB Wi-Fi adapter with reliable monitor mode and packet injection support (e.g., Alfa AWUS036ACH or similar chipset)
* **GPS:** USB GPS dongle (u-blox 7/8/9 architecture, G-Mouse, etc.)
* **Power:** Regulated vehicle 12V USB adapter or high-capacity power bank

Kismet functions as a full-featured RF inspection engine providing a local web UI, multi-radio channel hopping, rich PCAP/kismet log formats, and deep 802.11 protocol parsing. Total cost: **~$150–$220**.

#### Other Proven Hardware in Current Community Testing
* **Flipper Zero + Add-ons:** Lab 5 / Project Zero or ESP32-C5 GPS daughterboards running Marauder or Project Zero firmware.
* **Hak5 Pineapple Pager:** Paired with a GPS dongle and Alfa tri-band adapters.
* **Portable Handhelds:** Raspi Jack, Clockwork Pi uConsole + Hacker Gadgets AIO, and CYD (Cheap Yellow Display) units running PorkChop or Bruce firmware.
* **Specialized Rigs:** Hail Hound (optimized for dedicated 2.4 GHz sweeps) or multi-node mesh clusters (Biscuit, Marauder, or Piglet architectures).

> *Note: You do not need every device. Start simple and expand hardware based on the specific bands or protocols you want to study. I started by using an old android phone, you can download software to it from the play store, I don't know of any ios devices being used currently.*

---

## 6. How to Use Wardriving to Learn Cybersecurity

Treat every drive as an active RF field lab:

1. **Audit Encryption Transitions:** Review post-drive statistics. Count the ratio of legacy WEP/WPA networks and open access points compared to modern WPA2-Personal/Enterprise and WPA3 deployments.
2. **Analyze Propagation & Attenuation:** Compare the physical reach of 2.4 GHz vs. 5 GHz across varying topographies (dense urban downtowns vs. open suburban layouts, building materials, and tree canopies).
3. **Inspect Frame Headers & Hidden SSIDs:** Observe how hidden networks suppress the SSID in standard beacon frames while still revealing their BSSID, channel, and capability parameters.
4. **Enumerate Hardware via OUIs:** Review the manufacturer Organizationally Unique Identifier (the first 3 bytes of the BSSID) to identify hardware vendors, ISP-issued gateways, and common IoT infrastructure.
5. **Parse Session Data Manually:** Open exported CSV files in a spreadsheet editor or ingest them into Kismet/Wireshark to analyze channel overlap, co-channel interference, and received signal strength indicators (RSSI).
6. **Collaborate:** Join a team on WiGLE or WDGWars to share logs, study regional data sets, and analyze coverage gaps.
7. **RF Hardware Experimentation:** Test different antenna gains (dBi ratings), directional vs. omnidirectional antennas, and multi-radio configurations to see how receiver sensitivity impacts spatial capture.

---

## 7. Best Practices and Mindset

* **Stay Passive:** Strictly log beacon and probe broadcast metadata. Never deauthenticate users, attempt handshakes, or connect
When ready, add a Raspberry Pi + Kismet setup for deeper Linux-based analysis.
