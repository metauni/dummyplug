# Dummy Plug

Cloud-based automated recording and streaming of metauni events.

The aim of the dummy plug system is to make it trivial to both record and stream high-quality audio and video of metauni events. The system consists of OBS ([Open Broadcaster Software](https://obsproject.com)) and Windows PowerShell scripts running on a Google Cloud Platform (GCP) instance with a T4 NVIDIA GPU (using the `nvidia-gaming-windows-server-2019-1-vm` image), and some Luau scripts running on the Roblox server. 

## Unresolved issues

[Orb system](https://github.com/metauni/orb)

It appears to be against Roblox's Terms of Use for users to provide the username and password of a "camera alt" to metauni

Roblox's [terms of use](https://en.help.roblox.com/hc/en-us/articles/115004647846-Roblox-Terms-of-Use) explicitly say "You may never allow anyone else to use your Account (except your parents or legal guardian)".

Remote Desktop (RDP).

GCP Nvidia T4 instance

## Goals

Running [OBS on a GCP machine](https://obsproject.com/forum/threads/running-obs-on-google-gcp-cloud-vm-with-tesla-t4-gpu-it-works.135072/) with the NVIDIA T4 GPU and gaming image (note the bit about "enable the GPU whilst using RDP"). For streaming [NVENC](https://www.nvidia.com/en-us/geforce/guides/broadcasting-guide/) seems to be important.

There [may be some issues](https://support.parsec.app/hc/en-us/articles/115002683491-Running-Parsec-On-A-Headless-Gaming-PC-Or-A-Server) with capturing video on headless servers.

[OBS websocket](https://github.com/obsproject/obs-websocket/blob/4.x-current/README.md).
