# 📺 Media Browser

**Media Browser** is a lightweight, self-hosted media directory browser built entirely on **NGINX** — no database, no backend code, no dependencies.  
It provides a clean, responsive interface for browsing SMB/NFS mounted media shares as web accessible including integration with **Authentik** IDaM and **Basic Auth** integration.  
File listings are styled with a dark theme and automatically cleaned up to remove unnecessary prefixes, keeping names simple and readable.

---

## ✨ Features

- ⚙️ **Zero-backend setup** — runs entirely on NGINX  
- 🔐 **Authentik & Basic Auth** integration  
- 🧠 **Smart filename cleanup** using JavaScript:
  - Removes redundant prefixes
  - Hides non-media files like GoPro metadata .etc.
- 🌙 **Dark UI** powered by `autoindex.css`
- 📱 **Responsive design** for mobile and desktop
- 🕒 **Preserves file date and size** from NGINX output
- 🔧 **Fully configurable** — edit a few static files, no rebuild required


## 💬 Contributing

- Pull requests and issues are welcome!
- Potential future improvements:
- Sorting options (by size, date, or name)
- Fancyindex module integration
- Fork the project and submit a PR on GitHub.
