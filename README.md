# Docker Compose Configuration for the 'Arrs' Stack

This setup includes the following services:

- **Sonarr**: Manages and downloads TV shows.
- **Radarr**: Manages and downloads movies.
- **Jellyseerr**: Provides a media request and management system.
- **Prowlarr**: Manages indexers for Sonarr and Radarr.

Each service is configured to operate within a custom Docker network named `the_arrs_stack` to facilitate seamless communication between containers.
