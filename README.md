# Dummy Plug

Cloud-based automated recording and streaming of metauni events.

The aim of the dummy plug system is to make it trivial to both record and stream high-quality audio and video of metauni events. The system consists of OBS ([Open Broadcaster Software](https://obsproject.com)) and Windows PowerShell scripts running on a Google Cloud Platform (GCP) instance with a T4 NVIDIA GPU (using the `nvidia-gaming-windows-server-2019-1-vm` image), and some Luau scripts running on the Roblox server.

When the dummy plug (= the GCP instance) is turned on and you connect to it with Remote Desktop with your local machine, there is a script on the desktop which you run that will automatically do the following:

1. Start Roblox and join the metauni Hub with a dedicated dummy plug account.
2. Waits for instructions (the dummy plug will attempt to stay in the Hub by sending keystrokes and rejoin if it is disconnected).

A user with dummy plug privileges, who is attached to an [orb](https://github.com/metauni/orb) in a metauni experience as a speaker, can use a GUI element in the Orb system to "request a dummy plug". If one is available then 

3. Server scripts in the Hub use `TeleportService` to send the dummy plug to the requested place.
4. The dummy plug attaches to the requested orb and enables listening mode and OrbCam.
5. The GCP instance begins to record audio (including spatial voice) and video using OBS.

The dummy plug will pause recording when the speaker detaches from the orb, and will resume recording when they reattach, until it is dismissed by the speaker at which point it will return to Step 2.

6. Completed videos are moved to an S3 bucket and a URL for download is sent (via the Discord bot) to the Discord account of the speaker (who must have registered in Discord with their Roblox username).

Throughout this process somebody has to have their local machine connected via RDP to the GCP instance (but beyond keeping this connection alive they do not need to manually do anything). It may be technically more difficult to run this completely headless (see below).

Running [OBS on a GCP machine](https://obsproject.com/forum/threads/running-obs-on-google-gcp-cloud-vm-with-tesla-t4-gpu-it-works.135072/) with the NVIDIA T4 GPU and gaming image (note the bit about "enable the GPU whilst using RDP"). For streaming [NVENC](https://www.nvidia.com/en-us/geforce/guides/broadcasting-guide/) seems to be important.

## FAQ

* **Where do the dummy plug accounts come from?** Since they have to be spatial voice enabled, these accounts have to be age-verified. For the time being these will be accounts belonging to metauni administrators that are available for recording. Roblox's Terms of Use [terms of use](https://en.help.roblox.com/hc/en-us/articles/115004647846-Roblox-Terms-of-Use) explicitly say "You may never allow anyone else to use your Account (except your parents or legal guardian)" so users can't provide "camera alt" account details to us to use on their behalf.

## First trial

The first trial will be running on my Windows laptop rather than a cloud machine, but will otherwise be as described above. 

## Headless mode?

There [may be some issues](https://support.parsec.app/hc/en-us/articles/115002683491-Running-Parsec-On-A-Headless-Gaming-PC-Or-A-Server) with capturing video on headless servers. See also [OBS websocket](https://github.com/obsproject/obs-websocket/blob/4.x-current/README.md).
