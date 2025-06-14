# VM Setup and Environment Preparation

## 1. VM Setup
- Provision a new virtual machine (VM) with your preferred OS (e.g., Ubuntu 22.04).
- Ensure the VM has sufficient resources (CPU, RAM, disk space) for running Docker and AI models.
- Update the system:
  ```sh
  sudo apt update && sudo apt upgrade -y
  ```

## 2. Install Docker
- Install Docker Engine:
  ```sh
  curl -fsSL https://get.docker.com -o get-docker.sh
  sudo sh get-docker.sh
  ```
- Add your user to the docker group:
  ```sh
  sudo usermod -aG docker $USER
  ```
- Log out and back in for group changes to take effect.
- Verify Docker installation:
  ```sh
  docker --version
  ```

## 3. Install Open WebUI
- Clone the Open WebUI repository or pull the Docker image as per [Open WebUI documentation](https://github.com/open-webui/open-webui).
- Example using Docker:
  ```sh
  docker run -d -p 8080:8080 openwebui/open-webui:latest
  ```
- Access the WebUI at `http://<VM-IP>:8080`.

## 4. Install Ollama
- Download and install Ollama from [https://ollama.com/download](https://ollama.com/download) or use the following commands:
  ```sh
  curl -fsSL https://ollama.com/install.sh | sh
  ```
- Start the Ollama service:
  ```sh
  ollama serve
  ```

## 5. Download and Run Models
- List available models:
  ```sh
  ollama list
  ```
- Pull a model (e.g., llama2):
  ```sh
  ollama pull llama2
  ```
- Run a model:
  ```sh
  ollama run llama2
  ```

## 6. Enable Network Access
- Ensure firewall rules allow inbound connections to required ports (e.g., 8080 for WebUI).
- Example (UFW):
  ```sh
  sudo ufw allow 8080/tcp
  sudo ufw enable
  ```
- Confirm network access by connecting to the VM's IP and specified ports from your local machine.

---

*Document last updated: 2025-06-14*