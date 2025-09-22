# A *somewhat* comprehensive setup guide for my own personal Proxmox homelab

This is mainly for my own reference, however, some of these things took a lot of research, trial and error and could potentially help save someone else some time, hence why I've made this a public repository.

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
    * Getting started
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
