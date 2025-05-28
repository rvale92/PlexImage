# Plex Docker Compose Setup

This project provides a simple and robust way to run [Plex Media Server](https://www.plex.tv/) in a Docker container using Docker Compose. It is designed for easy deployment, portability, and maintainability of your home media server.

## 🚀 Project Overview
- **Containerizes Plex Media Server** for isolation and easy management
- **Custom port mapping** to avoid conflicts with existing Plex installations
- **Persistent storage** for configuration and media libraries
- **Easy updates** and rollbacks using Docker

## 📦 Prerequisites
- [Docker Desktop](https://www.docker.com/products/docker-desktop) installed on your system
- [Docker Compose](https://docs.docker.com/compose/) (included with Docker Desktop)
- A Plex account ([sign up here](https://www.plex.tv/sign-up/))

## 🛠️ Setup Instructions

1. **Clone this repository:**
   ```sh
   git clone https://github.com/rvale92/PlexImage.git
   cd PlexImage
   ```

2. **Copy your `docker-compose.yml` file:**
   If not already present, copy or create your `docker-compose.yml` in this directory. Example:
   ```yaml
   version: '3.8'
   services:
     plex:
       image: lscr.io/linuxserver/plex:latest
       container_name: plex
       environment:
         - PUID=1000
         - PGID=1000
         - TZ=America/New_York
         - VERSION=docker
         - PLEX_CLAIM=your-plex-claim-token
       volumes:
         - ./config:/config
         - ./tv:/data/tvshows
         - ./movies:/data/movies
       ports:
         - 32401:32400
         # Add or remove ports as needed
       restart: unless-stopped
   ```
   - Replace `your-plex-claim-token` with your actual Plex claim token ([get one here](https://www.plex.tv/claim/)).
   - Adjust volume paths and timezone as needed.

3. **Start Plex in Docker:**
   ```sh
   docker compose up -d
   ```

4. **Access Plex:**
   - Open your browser and go to: [http://localhost:32401/web](http://localhost:32401/web)
   - Sign in with your Plex account and complete the setup.

## 📝 Usage
- **To stop Plex:**
  ```sh
  docker compose down
  ```
- **To update Plex:**
  ```sh
  docker compose pull
  docker compose up -d
  ```
- **To view logs:**
  ```sh
  docker compose logs -f
  ```

## 🛡️ Troubleshooting
- **Port already in use:** Change the host port in `docker-compose.yml` (e.g., `32401:32400`).
- **Permission issues:** Ensure the correct `PUID` and `PGID` for your user.
- **Media not showing:** Check your volume paths and Plex library settings.
- **For more help:** See the [LinuxServer.io Plex documentation](https://docs.linuxserver.io/images/docker-plex/).

## 🙏 Credits
- [Plex Media Server](https://www.plex.tv/)
- [LinuxServer.io Plex Docker Image](https://hub.docker.com/r/linuxserver/plex)

---

Feel free to fork, contribute, or open issues! 