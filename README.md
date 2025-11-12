# 📦 Run LLMs Locally on an NVIDIA GPU with a Web UI

> Custom Open-WebUI configuration with Ollama in Docker containers for running large‑language‑models locally on an NVIDIA GPU with a simple web UI.
Accessible from all devices on your local network.
> All you need is a CUDA‑capable Linux box (or Docker‑powered Windows/Mac with WSL‑2).

---

## 📋 Prerequisites

- System with [CUDA-capable GPU](https://developer.nvidia.com/cuda-gpus).
- Have Docker and Docker Compose installed.
- Have the CUDA Toolkit correctly installed. ([Documentation](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/))
- Have the NVIDIA Container Toolkit installed. ([Documentation](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/))

---

## 🚀 Quickstart

### 1️⃣ Clone repository

```bash
git clone https://github.com/StinoBytes/local-llm.git
cd local-llm
```

### 2️⃣ Folder creation for persistency

```bash
mkdir -p data/ollama data/openwebui
```

```bash
sudo chown -R $(id -u):$(id -g) data
```

### 3️⃣ Spin up containers

```bash
docker compose up -d
```

### 4️⃣ Configure Open WebUI and add models

1. Open WebUI is accessible on [port 3000](http://localhost:3000).
2. Create admin account in the web interface.
3. Go to [admin panel > settings > models](http://localhost:3000/admin/settings/models) to add and download models from [Ollama's library](https://ollama.com/library).
4. Enjoy!

Optional: Add extra's according to the [Open WebUI Documentation](https://docs.openwebui.com/) such as integrating web search for models.

---

## 📦 What’s actually running?

| SERVICE    | IMAGE                              | GPU support |
| ---------- | ---------------------------------- | ----------- |
| Ollama     | ollama/ollama:latest               | CUDA        |
| Open WebUI | ghcr.io/open-webui/open-webui:cuda | CUDA        |

Both images are built with the CUDA‑runtime (nvidia/cuda:12.3.1-cudnn8-runtime-ubuntu22.04) and the NVIDIA Container Toolkit so that GPU memory is visible inside the containers.

    ⚠️ If you want to run on a non‑GPU machine, replace the Open WebUI 'image:' line in docker-compose.yml with the non‑GPU variant (openwebui/openwebui:latest) and drop the device_requests block in the Ollama service. The containers will still start but will run in CPU‑only mode and will be far slower.

---

## 📚 Troubleshooting

| Symptom                                                   | Likely cause                                     | Fix                                                                                                       |
| --------------------------------------------------------- | ------------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| Containers fail to start: “no such device /dev/nvidiactl” | NVIDIA drivers / toolkit not installed correctly | Re‑run nvidia-setup from the toolkit docs; make sure the `nvidia-container-toolkit` package is installed. |
| Ollama logs show “CUDA error: not initialized”            | GPU driver isn’t exposed to Docker               | Install NVIDIA Container Toolkit and restart the Docker daemon (`sudo systemctl restart docker`).         |
| Data dirs stay empty after restart                        | Permissions issue                                | `sudo chown -R $(id -u):$(id -g) data` or add the user to the docker group.                               |
| UI doesn’t open                                           | Port 3000 blocked by firewall                    | `sudo ufw allow 3000` (or the firewall you use).                                                          |
| Models never download                                     | Network restrictions (e.g., corporate proxy)     | Set `HTTP_PROXY` / `HTTPS_PROXY` env vars in `docker-compose.yml`.                                        |

---

## 📄 License

This project is released under the MIT License – see the `LICENSE` file for details.

---
