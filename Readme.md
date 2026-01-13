
# 📘 Respellion Employment Handbook

Welcome! This repository contains the source for our internal **Employment Handbook**, built as a clean, modern, and easy-to-navigate documentation site.

---

## 🛠️ Tech Stack

We keep things simple and containerized:

- **Static site generator**: [MkDocs](https://www.mkdocs.org/)
- **Theme**: [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) (via the official Docker image)
- **Container runtime**: Docker or Podman
- **Orchestration**: Docker Compose
- **Deployment**: Ansible
- **Web server**: [Caddy](https://caddyserver.com/) (as a reverse proxy)

---

## 🧰 Requirements

To run or contribute to this project locally, you’ll need:

- A working internet connection  
- Git  
- An OCI-compatible container runtime (e.g., **Docker** or **Podman**)  
- *(Optional)* A web browser to preview the site  

> 💡 The entire app is containerized—no Python or MkDocs installation needed on your host!

---

## ▶️ Getting Started

### 1. Preview the Site Locally

Run this command to start a live-reloading development server:

```bash
podman run --rm -it -p 8000:8000 -v ${PWD}:/docs:z squidfunk/mkdocs-material serve --dev-addr 0.0.0.0:8000
```

> 🔍 **Note**: We bind to `0.0.0.0` so the site is accessible outside the container (e.g., from your browser).  
> If port `8000` is busy, change it (e.g., `-p 8080:8000`).

Then open your browser to: [http://localhost:8000](http://localhost:8000)

Edit any Markdown file in the `docs/` folder—changes appear instantly!

---

### 2. Starting a New MkDocs Project (Optional)

If you ever want to spin up a fresh MkDocs site from scratch:

```bash
podman run --rm -it -v ${PWD}:/docs:z squidfunk/mkdocs-material new .
```

This creates the basic `mkdocs.yml` and `docs/` structure.

---

### 🔗 Helpful Resources

- [MkDocs User Guide](https://www.mkdocs.org/user-guide/)
- [Markdown Syntax Cheatsheet](https://www.markdownguide.org/basic-syntax/)
- [Material for MkDocs – Getting Started](https://squidfunk.github.io/mkdocs-material/getting-started/)
- [Caddyfile Configuration Patterns](https://caddyserver.com/docs/caddyfile/patterns)

---

## 🤝 How to Contribute

We welcome improvements! Just:

1. Fork the repo  
2. Make your changes  
3. Open a **Pull Request**  

All updates to the handbook go through PRs—no direct pushes to `master`.

---

## 🚀 Deploying the Site

Deployment is fully automated with Ansible:

```bash
ansible-playbook -i hosts.ini ./deploy_playbook.yml
```

> ✅ Make sure you have SSH access to the target host listed in `hosts.ini`.

### What the playbook does:

1. Installs Docker (if missing)  
2. Copies the entire project to `/opt/mkdocs` on the remote host  
3. Runs `docker compose up -d` to start the site  

That’s it! The live site is served via Caddy as a reverse proxy.

---

✨ **Happy documenting!**  
*— The Respellion Team*