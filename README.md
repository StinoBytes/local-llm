# Run LLMs locally with a web UI

Custom Open-WebUI configuration with Ollama in Docker containers for running local LLMs, optimized for systems with Nvidia GPU's.
Accessible from all devices on your local network.

## Quickstart

### Prerequisites

- Linux system with [CUDA-capable GPU](https://developer.nvidia.com/cuda-gpus).
- Have Docker and Docker Compose installed.
- Have the CUDA Toolkit correctly installed. ([Documentation](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/))
- Have the NVIDIA Container Toolkit installed. ([Documentation](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/))

### Clone repository

```bash
git clone https://github.com/StinoBytes/local-llm.git
```

And move working directory the the project's directory:

```bash
cd local-llm
```

### Folder creation for persistency

```bash
mkdir -p data/ollama data/openwebui
```

```bash
sudo chown -R $(id -u):$(id -g) data
```

### Spin up containers

```bash
docker compose up -d
```

### Configure Open WebUI and add models

1. Open WebUI is accessible on [port 3000](http://localhost:3000).
2. Create admin account in the web interface.
3. Go to [admin panel > settings > models](http://localhost:3000/admin/settings/models) to add and download models from [Ollama's library](https://ollama.com/library).
4. Enjoy!

Optional: Add extra's according to the [Open WebUI Documentation](https://docs.openwebui.com/) such as integrating web search for models.
