# Setup Cheatsheet

## 1. VM Setup
- Provision a virtual machine with your preferred OS (Ubuntu recommended).
- Ensure the VM has internet access and sufficient resources (CPU, RAM, disk).

## 2. Docker Installation
- Update package index: `sudo apt update`
- Install Docker: `sudo apt install docker.io -y`
- Enable and start Docker: `sudo systemctl enable --now docker`
- Add your user to the docker group: `sudo usermod -aG docker $USER`

## 3. Ollama + Open WebUI Deployment
- Pull the latest Ollama image: `docker pull ollama/ollama`
- Run Ollama: `docker run -d --name ollama -p 11434:11434 ollama/ollama`
- Pull Open WebUI: `docker pull ghcr.io/open-webui/open-webui:main`
- Run Open WebUI: `docker run -d --name open-webui -p 3000:3000 --add-host=host.docker.internal:host-gateway -e OLLAMA_API_BASE_URL=http://host.docker.internal:11434 ghcr.io/open-webui/open-webui:main`

## 4. SSH Configuration
- Generate SSH keys: `ssh-keygen -t ed25519 -C "your_email@example.com"`
- Copy public key to VM: `ssh-copy-id user@vm_ip`
- Test SSH connection: `ssh user@vm_ip`

## 5. Model Pulling
- Use Ollama to pull a model: `ollama pull llama2`
- List available models: `ollama list`

## 6. Exposing Port 3000
- Ensure Docker container is running with `-p 3000:3000` to expose Open WebUI.
- Check firewall rules: `sudo ufw allow 3000/tcp`
- Verify with: `curl http://localhost:3000`

## 7. Connecting from Other Machines (e.g., DevKit 2)
- On DevKit 2, open a browser and navigate to `http://<VM_IP>:3000`
- Ensure both machines are on the same network or port 3000 is accessible externally.
- If using SSH tunneling: `ssh -L 3000:localhost:3000 user@vm_ip`
- Then access `http://localhost:3000` on DevKit 2.
