I am using a MacBook Air M2 with 8 GB memory for my daily work.

## Homelab

My Homelab consists of three main components:
- Portainer Business Edition
	- Raspberry Pi 4, with 4 GB RAM and 500 GB USB 3.0 storage
	- Dell Wyze 5070, with 20 GB RAM and 240GB SSD storage
- Proxmox Hypervisor
	- 8 Cores
	- 32 GB RAM
	- 2x 4TB HDD as RAID1 with ZFS within TrueNAS Core as main storage
	- 2x 1TB SSD as RAID1 with ZFS as system storage for Proxmox
	- 1x 1TB SSD as temporary storage for non critical data