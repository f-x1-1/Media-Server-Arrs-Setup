# Media-Server-Arrs-Setup
This is media server setup for Arrs apps (Sonarr, Radarr, Jellyserr and Prowlarr)

version: '3.8'

services:
  # Sonarr - Manages and downloads TV shows
  sonarr:
    image: linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
    volumes:
      - /path/to/sonarr/config:/config
      - /path/to/tv/shows:/tv
      - /path/to/downloads:/downloads
    ports:
      - 8989:8989
    networks:
      - the_arrs_stack
    restart: unless-stopped

  # Radarr - Manages and downloads movies
  radarr:
    image: linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
    volumes:
      - /path/to/radarr/config:/config
      - /path/to/movies:/movies
      - /path/to/downloads:/downloads
    ports:
      - 7878:7878
    networks:
      - the_arrs_stack
    restart: unless-stopped

  # Jellyseerr - Media request and management system
  jellyseerr:
    image: fallenbagel/jellyseerr:latest
    container_name: jellyseerr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
    volumes:
      - /path/to/jellyseerr/config:/app/config
    ports:
      - 5055:5055
    networks:
      - the_arrs_stack
    restart: unless-stopped

  # Prowlarr - Manages indexers for Sonarr and Radarr
  prowlarr:
    image: linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
    volumes:
      - /path/to/prowlarr/config:/config
    ports:
      - 9696:9696
    networks:
      - the_arrs_stack
    restart: unless-stopped

networks:
  the_arrs_stack:
    driver: bridge
