# Debian Home Lab Server — Acer TravelMate P249-G2-M

## Overview

Repurposed a personal laptop (previously daily-use, low RAM) into a dedicated Debian 13 home lab server: upgraded the hardware, installed Linux from scratch, and resolved a network throughput problem to bring it into stable use as a self-hosted infrastructure server.

## Hardware

| Component | Before | After |
|---|---|---|
| RAM | 1× 8GB SK Hynix DDR4 SO-DIMM 3200MHz | 2× 8GB SK Hynix DDR4 SO-DIMM 3200MHz (16GB dual-channel) |
| Storage | Toshiba THNSNK256GVN8 256GB M.2 2280 SSD (DRAM-less) | Samsung 860 EVO M.2 SATA 500GB SSD (512MB DRAM cache) |
| Thermal | — | Cleaned with compressed air and an anti-static brush |

**Why these upgrades:** the original SSD had no onboard DRAM cache, which risks I/O bottlenecks under sustained server workloads. The Samsung 860 EVO's DRAM cache and the extra RAM were chosen specifically to avoid that under continuous server use.

## Operating system

- **OS:** Debian 13 (XFCE), kernel 6.12.94
- **Install media:** Custom UEFI boot media, built and booted manually
- **Partitioning:**
  - `sda1` — 465.8GB → `/`
  - `sda2` — 487MB → `/boot/efi`
- **BIOS/UEFI:** Configured to boot from the custom UEFI installer media

## Problem: Ethernet link-speed / throughput issue

- **Symptom:** Network throughput on the server was well below expected.
- **Diagnosis:** Ran Ethernet link diagnostics to measure throughput and isolate whether the bottleneck was link negotiation, the NIC, or something upstream.
- **Fix:** Resolved a link negotiation mismatch, restoring stable, full-speed connectivity.

## Current use

Runs a Docker Compose stack hosting Nextcloud for family cloud storage, reachable from outside the LAN through port forwarding configured on the home network (see the companion [Home Network Administration & Gateway Configuration](../home-network) write-up for the network-side setup). The Nextcloud host was given a static IP so the port-forwarding rule stays valid.

## Status

Active — ongoing home lab used for self-hosted infrastructure projects.

## Photos

![Project Screenshot](assets/screenshot.png)
<caption></caption>

![Project Screenshot](assets/screenshot.png)
<caption></caption>

