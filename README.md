# 📺 Media Browser

**Media Browser** is a lightweight, self-hosted media directory browser built entirely on **NGINX** — no database and no additional library dependencies.  
It provides a clean, responsive interface for browsing SMB/NFS mounted media shares as web downloadable files and includes optional integration with **Basic Auth**.  
File listings are styled with a dark theme and cleaned up to remove unnecessary prefixes, keeping names simple and readable.

---

## ✨ Features

- ⚙️ **Zero-backend setup** — runs entirely on NGINX  
- 🔐 **Basic Auth** integration  
- 🧠 **Smart filename cleanup** using JavaScript:
  - Removes redundant prefixes
  - Hides non-media files like GoPro metadata .etc.
- 🌙 **Dark UI** customised by `autoindex.css`
- 📱 **Responsive design** for mobile and desktop
- 🕒 **Preserves file date and size** from NGINX output
- 🔧 **Fully configurable** — edit a few static files, no rebuild required

## 💬 Contributing

- Pull requests and issues are welcome!
- Potential future improvements:
  - Sorting options (by size, date, or name)
  - Fancyindex module integration
  - Find a way to programatically integrate Traefik reverse proxy and Authentik IdAM

## 🧰 Prerequisites

- Docker + Portainer (Can work without Portainer)
- Mounted SMB/NFS media directories on the host (e.g. `/mnt/GoPro`, `/mnt/Insta360`, …)
- A place on the host to store the site/config (e.g. `/var/lib/docker/volumes/mediabrowser`)

---

## 📁 Host folder layout
Create these directories on your **host**. We assume the volume location on the host is `/var/lib/docker/volumes/mediabrowser`:

└─ /site/ # web root: index.html, shares.json, autoindex.css, autoindex-footer.html

└─ /nginx/ # nginx.conf (+ optional .htpasswd)


## 🚀 Quick Start (Portainer Stack)

### 1) Project files
Copy the files to your host folder:

- /nginx/nginx.conf → NGINX server config
- /site/index.html → styled homepage
- /site/shares.json → share definition
- /site/autoindex.css → autoindex styling
- /site/autoindex-footer.html → cleanup JS injector

### 2) Stack file (docker-compose)
In Portainer → **Stacks** → **Add stack**, paste the YAML below:

```yaml
services:
  mediabrowser:
    image: nginx:stable-alpine
    container_name: mediabrowser
    restart: unless-stopped
    environment:
      - TZ=Europe/London
    ports:
      - "8080:80"  # change or remove if fronted by a reverse proxy
    volumes:
      # NGINX config and site assets
      - /var/lib/docker/volumes/mediabrowser/nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - /var/lib/docker/volumes/mediabrowser/site:/usr/share/nginx/html:ro

      # Map host media into /mnt/<id> INSIDE the container (Format is Host:Container)
      - /mnt/GoPro:/mnt/GoPro:ro
      - /mnt/Insta360:/mnt/Insta360:ro
      - /mnt/media3:/mnt/media3:ro

      # Optional Basic Auth file:
      # - /var/lib/docker/volumes/nginx/.htpasswd:/etc/nginx/.htpasswd:ro
```
### 3) Deploy the stack
Navigate to http://host:8080 (or selected port)
