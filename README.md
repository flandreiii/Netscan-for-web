# 📡 NetScan — Local Network Scanner

> A smooth, beginner-friendly local network scanner that runs entirely in your browser.
> Built by **flandreiii** · v1.0

---

## What is NetScan?

NetScan is a single-file HTML/CSS/JavaScript tool that lets you discover devices on your local network — straight from your browser, no installs required. It asks for your permission before doing anything, keeps all processing local, and never sends data anywhere.

---

## Features

- 🔒 **Permission-first** — always asks before scanning
- 🌐 **Auto subnet detection** via WebRTC
- 📡 **HTTP port probing** across your local subnet
- 🖥️ **Device type identification** (router, server, app, unknown)
- 📊 **Live stats** — hosts probed, responding devices, open ports, scan time
- 🗂️ **Filters** — view All / Online / Gateway devices
- 🖱️ **Expandable cards** — click any device for full details
- 📜 **Live log terminal** with timestamped entries
- ⚙️ **Three scan modes** — Fast, Deep, or This Device Only
- 💻 **100% client-side** — no backend, no server, no tracking

---

## How to Use

1. Open `https://flandreiii.github.io/Netscan-for-web` in any modern browser (Chrome recommended)
2. The subnet is auto-detected on load — or enter it manually (e.g. `192.168.1`)
3. Choose a **Scan Mode**:
   - **Fast** — probes ports 80, 443, 8080, 8443
   - **Deep** — probes more ports and more hosts
   - **This Device Only** — scans localhost only
4. Click **▶ Scan**
5. Review the permission prompt and click **Allow & Scan**
6. Watch devices appear in real time — click any card to expand details

---

## How It Works (Technical)

### Local IP Detection
NetScan uses the **WebRTC API** (`RTCPeerConnection`) to discover your machine's local IP address and derive your subnet (e.g. `192.168.1.x`). This happens client-side with no external STUN servers.

### Host & Port Probing
For each host in the range, NetScan sends a `fetch()` request with `mode: 'no-cors'` to common HTTP ports. The response behavior reveals whether a port is open:

| Response | Meaning |
|---|---|
| Resolves | Port open, HTTP server present |
| Network error (not abort) | Host alive, port refused |
| AbortError (timeout) | Host not responding |

### Concurrency
Up to **8 hosts are probed in parallel** to keep scans fast without overwhelming the network.

---

## Browser Limitations

Browsers enforce strict security policies that limit network scanning:

- ❌ No raw TCP/UDP socket access
- ❌ No ICMP (ping) support
- ❌ HTTPS pages cannot probe HTTP endpoints (mixed content)
- ✅ `fetch` with `no-cors` can detect responding HTTP services

**For deeper scanning**, use dedicated tools like:
- [nmap](https://nmap.org/) — the gold standard for network scanning
- [Angry IP Scanner](https://angryip.org/) — beginner-friendly GUI tool
- [Advanced IP Scanner](https://www.advanced-ip-scanner.com/) — Windows-friendly

---

## File Structure

```
network-scanner.html   ← the entire app (HTML + CSS + JS, single file)
README.md              ← this file
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Structure | HTML5 |
| Styling | CSS3 (custom properties, grid, animations) |
| Logic | Vanilla JavaScript (ES2020+) |
| Fonts | Google Fonts — Outfit + Share Tech Mono |
| Network | WebRTC API, Fetch API |

No frameworks. No dependencies. No build step.

---

## Compatibility

| Browser | Support |
|---|---|
| Chrome / Edge | ✅ Full |
| Firefox | ✅ Full |
| Safari | ⚠️ WebRTC auto-detect may be limited |
| Mobile browsers | ⚠️ Partial (network probing restricted) |

---

## Privacy & Ethics

- All scanning happens **inside your browser** — zero external requests
- NetScan will **only probe IPs on your own subnet**
- Always scan networks **you own or have explicit permission to scan**
- Scanning networks without authorization may be illegal in your jurisdiction

---

## Author

Made with 🩵 by **flandreiii**

---

## 📜 License

MIT License

Copyright (c) 2026 flandreiii

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
