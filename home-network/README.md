# Home Network Administration & Gateway Configuration

## Overview

Administered a home network built around a mesh Wi-Fi system: replaced the ISP's default routing setup to fix a double-NAT problem, resolved a mesh signal conflict, and worked with the ISP to remove CGNAT and get a real public IP for self-hosted services.

## Network layout

- **ISP:** PLDT, GPON ONU HG6245D (set to bridge/passthrough mode)
- **Main router/mesh:** TP-Link Deco M4R — 2 units active (1 as router, 1 as extender); 1 spare unit deliberately left out of the mesh (see Problem 1)
- **Connected devices:** ~15, mixed wired and Wi-Fi — laptops, smartphones, a Chromecast with Google TV, IP cameras, a networked printer
- **DHCP / DNS:** Handled by the Deco app, automatic DNS
- **Port forwarding:** Configured for a personal Minecraft server and an ongoing Nextcloud instance for family cloud storage, with a static IP binding set on the Nextcloud host so the port-forwarding rule stays valid

## Problem 1 — Persistent signal disconnection

- **Symptom:** Devices intermittently dropped their Wi-Fi connection.
- **Hypothesis:** All 3 available Deco mesh units were active; overlapping coverage in the middle of the house was likely causing devices to bounce between units with conflicting signal strength.
- **Fix:** Removed one mesh unit, running only 2. Disconnections stopped.

## Problem 2 — Bottlenecked internet speed on Wi-Fi

- **Symptom:** Wi-Fi (5GHz) throughput was roughly 200 Mbps below the subscribed ISP plan.
- **Diagnosis:** A wired connection hit full speed, isolating the problem to the Wi-Fi/mesh path. Suspected double-NAT between the ISP router and the Deco mesh.
- **Fix:** Set the ISP router to bridge/passthrough mode and made the Deco mesh the sole router, restoring full QoS control over the network.

## Problem 3 — Remote access while behind CGNAT

- **Symptom:** The network was behind CGNAT, so self-hosted services (Nextcloud) had no way to accept direct inbound connections from outside the LAN.
- **Fix:** Configured Tailscale (WireGuard-based) VPN with Funnel enabled, giving remote access to the Nextcloud instance without needing a public IP. This was the interim solution ahead of the permanent fix below.

## Problem 4 — Removing CGNAT for a real public IP

- **Goal:** Get off CGNAT entirely so self-hosted services could be reached directly, instead of routing through the Tailscale workaround.
- **Process:** Requested the ISP remove CGNAT and assign a dynamic public IP. Worked live with an ISP technician by phone through a short outage, tried a different ONU port on their instruction, and verified the fix by confirming the IP shown on-device matched the IP shown in the Deco app.
- **Result:** The network now runs on a dynamic public IP, off CGNAT.

## Status

Active — this is the live network for the home lab and family devices.

## Photos

_(Add a network diagram, Deco app screenshots, and before/after speed test results here.)_
