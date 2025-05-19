# IPTV Proxy for Synology NAS

This package provides a simple yet effective IPTV proxy solution for Synology NAS using Docker. It retrieves your M3U and XMLTV files, serves them through a clean web interface, and provides URLs that you can use with Emby or any other IPTV player.

## Features

- Automatic daily updates of M3U playlist and XMLTV guide
- Clean web interface for easy access
- Optimized for Emby integration
- Runs entirely in Docker containers
- No need for complex Synology configuration

## Prerequisites

- Synology NAS with Docker package installed
- Docker Compose installed (comes with Docker package)
- Port 8081 available on your Synology NAS
- Basic knowledge of SSH or File Station for file management

## Installation

1. **Create Directory Structure**

   Create a directory in your preferred location, for example:
   ```
   /volume3/docker/iptv-proxy/
   ```

2. **Copy Files**

   Inside this directory, create the following structure:
   ```
   /volume3/docker/iptv-proxy/
   ├── docker-compose.yml
   ├── nginx/
   │   ├── nginx.conf
   │   └── conf.d/
   │       └── default.conf
   ├── scripts/
   │   └── update-iptv.sh
   ├── data/
   └── www/
   ```

3. **Edit Configuration**

   Open the `docker-compose.yml` file and update the following environment variables:
   - `SERVER_IP`: Your Synology NAS IP address
   - `SERVER_PORT`: The port (default is 8081)
   - `TZ`: Your timezone

4. **Start the Containers**

   Open Terminal in your Synology or connect via SSH, navigate to your directory and run:
   ```bash
   cd /volume3/docker/iptv-proxy/
   docker-compose up -d
   ```

5. **Access Your IPTV Portal**

   Open a web browser and navigate to:
   ```
   http://your-synology-ip:8081/
   ```

## Usage with Emby

1. In Emby, go to Dashboard → Live TV
2. Click "Add TV Provider"
3. Select "M3U Tuner"
4. Enter the M3U URL: `http://your-synology-ip:8081/playlist.m3u`
5. For guide data, enter the XMLTV URL: `http://your-synology-ip:8081/epg.xml`
6. Save your settings and refresh guide data

## Maintenance

### Checking Logs
```bash
cd /volume3/docker/iptv-proxy/
docker-compose logs
```

### Manual Update
If you need to manually trigger an update:
```bash
cd /volume3/docker/iptv-proxy/
docker-compose exec iptv-updater /scripts/update-iptv.sh
```

### Stopping the Service
```bash
cd /volume3/docker/iptv-proxy/
docker-compose down
```

### Upgrading
1. Stop the containers: `docker-compose down`
2. Pull the latest images: `docker-compose pull`
3. Start the containers: `docker-compose up -d`

## Troubleshooting

- **No data appearing**: Check the logs to see if there were any errors downloading or processing the files.
- **Can't connect to web interface**: Verify that port 8081 is not blocked by Synology's firewall.
- **M3U file not working in Emby**: Some M3U formats need additional processing. Check the update script logs.

## License

This project is for personal use only. Do not redistribute the proxy or use it for commercial purposes.
