# A comprehensive setup guide for my own personal Proxmox homelab

I started this project as a companion piece to my homelab, documenting what I was doing for future reference. It quickly grew into something that required a lot of time, research, and trial and error. This guide is the result of that effort, created to help others who want to follow a similar path and hopefully avoid the same challenges I faced. 

Most pages include a **troubleshooting** section at the bottom. If you encounter an issue, you’ll hopefully find your solution there. If not, feel free to open an issue and I’ll do my best to help!

## Overview

My intention for this setup was to achieve the following goals:
- **Media server** with full *arr* automation stack  
- **Smart home automation** using Home Assistant with local + remote AI voice assistants  
- **File storage** with SMB shares and a Google Drive replacement  
- **Network services** such as self-hosted DNS with filtering  
- **Monitoring and dashboards** for comprehensive system metrics and quick links

As with all projects of this nature, I'm certain the scope will only increase with time, but from the onset these are my initial goals.

## Contents

### Infrastructure

* Proxmox installation and setup
    * [Getting started](infrastructure/getting_started.md)
    * Initial setup
    * VMs vs LXC
    * GPU passthrough
    * Backups
    * Power efficiency and optimisations
* SSD and HDD configuration
* Cloudflared
* Adguard
* Unbound

### Internet of Things

* Samba via Turnkey
* Homarr
* Metrics stack
    * Grafana
    * InfluxDB
    * Telegraf


### Automation

* Home Assistant stack
    * Home Assistant
    * Piper
    * Whisper
    * OpenWakeWord
    * Wyoming Satellite
* Ollama
* diyHue

### Personal Cloud

* Nextcloud
* Immich

### Media

* Jellyfin
* Emby
* qBittorrent
* Arr suite
    * Bazarr
    * Lidarr
    * Prowlarr
    * Radarr
    * Sonarr

### Other
* Fedora VM
* Windows VM
* Sources

*This guide reflects my personal setup. Adapt at your own risk.*
