# Project Changes & Updates

A casual log of changes, improvements, and decisions made along the way.

## 2025-05-09: The Great Migration to Ubuntu Server

After running the media stack on Windows for a while, I finally made the jump to Ubuntu Server LTS. This wasn't just a simple platform switch - it was a complete rethinking of how the stack should run.

### Why the Change?
Windows was working, but it always felt like we were fighting against the OS rather than working with it. Docker on Windows, while functional, never quite felt native. The networking stack was a constant source of headaches, and resource management was... let's say, "interesting."

### What's Better Now?
The move to Ubuntu Server has been a game-changer. Everything just works more smoothly:
- Docker runs natively, no more virtualization overhead
- Network performance is noticeably better - no more weird Windows networking quirks
- Resource usage is more predictable and efficient
- The whole stack feels more stable and "at home" on Linux

### The Technical Details
I've updated all the deployment docs to reflect the new Ubuntu-first approach. The setup is now much cleaner:
- Native Docker installation
- Proper systemd integration
- Better logging and monitoring
- More straightforward networking setup

### Looking Forward
This change has opened up some interesting possibilities. I'm thinking about:
- Migration to Talos Linux and Kubernetes once stable
- Would enable proper container orchestration and scaling
- Better resource management through k8s
- More robust monitoring and deployment options

The stack feels more "production-ready" now, which is exactly what I was aiming for.

## 2025-05-07: The Beginning

Started this project with a simple goal: build a reliable media server that doesn't require constant babysitting. The initial stack included:
- Plex for media serving
- Sonarr for TV show management
- qBittorrent for downloads
- Gluetun for VPN
- Glance for monitoring