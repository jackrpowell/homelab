# Media Stack

A Docker Compose setup for a media server stack including Plex, Sonarr, qBittorrent, and Gluetun VPN, with monitoring through Glance dashboard.

## Prerequisites

- Docker and Docker Compose installed
- A Private Internet Access (PIA) VPN account
- A Plex account

## Getting Started

1. Clone this repository:
```bash
git clone <repository-url>
cd <repository-name>
```

2. Copy the example environment file and update it with your credentials:
```bash
cp .env.example .env
```

3. Update the `.env` file with your:
   - PIA VPN credentials
   - Plex claim token (get it from https://www.plex.tv/claim/)
   - Timezone
   - User/Group IDs if needed
   - Local IP address (LOCAL_IP)

4. Create required directories:
```bash
mkdir -p gluetun qbittorrent/config sonarr/config plex/config plex/transcode downloads tv movies
```

5. Start the stack:
```bash
docker compose -f media-stack.yml up -d
```

## Services

- **Plex**: Media server (http://${LOCAL_IP}:32400/web)
- **Sonarr**: TV show management (http://${LOCAL_IP}:8989)
- **qBittorrent**: Torrent client (http://${LOCAL_IP}:8081)
- **Gluetun**: VPN client (http://${LOCAL_IP}:8888)
- **Glance**: Dashboard for monitoring all services (http://${LOCAL_IP}:8080)

## Configuration

### VPN (Gluetun)
- Currently configured to use PIA's Netherlands servers
- All traffic from qBittorrent and Sonarr routes through the VPN
- Plex runs outside the VPN for better performance

### Ports
- Plex: 32400
- Sonarr: 8989
- qBittorrent: 8081
- Gluetun: 8888
- Glance: 8080

### Volumes
- `./gluetun`: VPN configuration
- `./qbittorrent/config`: qBittorrent settings
- `./sonarr/config`: Sonarr settings
- `./plex/config`: Plex settings
- `./plex/transcode`: Plex transcoding directory
- `./downloads`: Download directory
- `./tv`: TV shows directory
- `./movies`: Movies directory
- `./config`: Glance dashboard configuration

## Monitoring

The services are monitored through the Glance dashboard, which provides:
- Real-time status monitoring of all services
- Quick access to service web interfaces
- Service health checks
- Visual status indicators

Access the Glance dashboard at http://${LOCAL_IP}:8080 to:
- Monitor service status
- Access service web interfaces
- View service health
- Configure additional monitoring settings

## Security Notes

- The `.env` file contains sensitive information and is gitignored
- Never commit the `.env` file to version control
- Use `.env.example` as a template for required environment variables
- Local IP address is configured via environment variable for easy deployment across different networks

## Troubleshooting

1. If services can't connect to the internet:
   - Check VPN status in Gluetun web interface
   - Verify PIA credentials in `.env`

2. If Plex can't be claimed:
   - Get a new claim token from plex.tv/claim
   - Update `.env` with the new token
   - Restart Plex: `docker compose -f media-stack.yml restart plex`

3. If downloads aren't working:
   - Check qBittorrent web interface
   - Verify VPN connection
   - Check download directory permissions

4. If Glance dashboard isn't showing services:
   - Verify LOCAL_IP is correctly set in `.env`
   - Check if services are running
   - Ensure correct IP address is configured

## License

This project is licensed under the MIT License - see the LICENSE file for details.