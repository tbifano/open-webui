# Open WebUI Troubleshooting Guide

## Understanding the Open WebUI Architecture

The Open WebUI system is designed to streamline interactions between the client (your browser) and the Ollama API. At the heart of this design is a backend reverse proxy, enhancing security and resolving CORS issues.

- **How it Works**: The Open WebUI is designed to interact with the Ollama API through a specific route. When a request is made from the WebUI to Ollama, it is not directly sent to the Ollama API. Initially, the request is sent to the Open WebUI backend via `/ollama` route. From there, the backend is responsible for forwarding the request to the Ollama API. This forwarding is accomplished by using the route specified in the `OLLAMA_BASE_URL` environment variable. Therefore, a request made to `/ollama` in the WebUI is effectively the same as making a request to `OLLAMA_BASE_URL` in the backend. For instance, a request to `/ollama/api/tags` in the WebUI is equivalent to `OLLAMA_BASE_URL/api/tags` in the backend.

- **Security Benefits**: This design prevents direct exposure of the Ollama API to the frontend, safeguarding against potential CORS (Cross-Origin Resource Sharing) issues and unauthorized access. Requiring authentication to access the Ollama API further enhances this security layer.

## Python Version Requirements

Open WebUI is recommended to run with Python versions 3.8 through 3.11. While newer versions like 3.13 might work, they haven't been extensively tested and could cause compatibility issues with some dependencies.

### Setting Up a Python Environment (Recommended)

Instead of downgrading your system Python, we recommend using a virtual environment:

1. **Using pyenv (Recommended for version management)**:
```bash
# Install pyenv (macOS)
brew install pyenv

# Add pyenv to your shell (add to ~/.zshrc or ~/.bash_profile)
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc

# Restart your shell or run
source ~/.zshrc

# Install a compatible Python version
pyenv install 3.11

# Set up the environment
pyenv local 3.11
pyenv rehash  # Rebuild the shim executables

# Now create and activate the virtual environment
python3 -m venv venv
source venv/bin/activate
```

For your current situation, try these commands to fix the error:

```bash
# Rehash pyenv
pyenv rehash

# If that doesn't work, restart your shell or run
source ~/.zshrc

# Then try creating the venv again
python3 -m venv venv
source venv/bin/activate
```

2. **Using conda**:
```bash
# Create a new environment with Python 3.11
conda create -n open-webui python=3.11
conda activate open-webui
```

3. **Using venv with existing Python**:
```bash
# If you already have a compatible Python version
python3.11 -m venv venv
source venv/bin/activate  # On Unix/macOS
# or
.\venv\Scripts\activate  # On Windows
```

After setting up your environment, verify the Python version:
```bash
python --version  # Should show 3.8-3.11
```

To install a specific Python version, visit [Python's official downloads page](https://www.python.org/downloads/).

## Open WebUI: Server Connection Error

If you're experiencing connection issues, it’s often due to the WebUI docker container not being able to reach the Ollama server at 127.0.0.1:11434 (host.docker.internal:11434) inside the container . Use the `--network=host` flag in your docker command to resolve this. Note that the port changes from 3000 to 8080, resulting in the link: `http://localhost:8080`.

**Example Docker Command**:

```bash
docker run -d --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://127.0.0.1:11434 --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

### Error on Slow Responses for Ollama

Open WebUI has a default timeout of 5 minutes for Ollama to finish generating the response. If needed, this can be adjusted via the environment variable AIOHTTP_CLIENT_TIMEOUT, which sets the timeout in seconds.

### General Connection Errors

**Ensure Ollama Version is Up-to-Date**: Always start by checking that you have the latest version of Ollama. Visit [Ollama's official site](https://ollama.com/) for the latest updates.

**Troubleshooting Steps**:

1. **Verify Ollama URL Format**:
   - When running the Web UI container, ensure the `OLLAMA_BASE_URL` is correctly set. (e.g., `http://192.168.1.1:11434` for different host setups).
   - In the Open WebUI, navigate to "Settings" > "General".
   - Confirm that the Ollama Server URL is correctly set to `[OLLAMA URL]` (e.g., `http://localhost:11434`).

By following these enhanced troubleshooting steps, connection issues should be effectively resolved. For further assistance or queries, feel free to reach out to us on our community Discord.
