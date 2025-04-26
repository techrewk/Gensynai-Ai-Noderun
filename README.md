# Gensynai-Ai-Noderun

To successfully set up and run a Gensyn Testnet node on an Ubuntu system, follow this comprehensive step-by-step guide:

**Prerequisites:**

- **Operating System:** Ubuntu 22.04
- **Hardware Requirements:**
  - **CPU:** Minimum 16GB RAM; more RAM (e.g., 32GB+) is recommended for larger models or datasets.
  - **GPU (Optional):** For enhanced performance, CUDA-supported devices are recommended, such as:
    - NVIDIA RTX 3090
    - NVIDIA RTX 4090
    - NVIDIA A100
    - NVIDIA H100
    - Note: The node can also run in CPU-only mode without a GPU.

**Step 1: Update System Packages**

Begin by updating your system's package list and upgrading existing packages:


```bash
sudo apt-get update && sudo apt-get upgrade -y
```


**Step 2: Install Essential Dependencies**

Install the necessary utilities and tools required for the setup:


```bash
sudo apt-get install -y python3 python3-venv python3-pip curl wget screen git lsof
```


**Step 3: Install Node.js and npm**

Install Node.js (version 22.x) and npm:


```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```


Verify the installation:


```bash
node -v
```


**Step 4: Install Yarn**

Set up Yarn, a package manager:


```bash
curl -o- -L https://yarnpkg.com/install.sh | bash
export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
source ~/.bashrc
```


Confirm Yarn is installed:


```bash
yarn -v
```


**Step 5: Install Docker and Docker Compose**

Docker is essential for containerized applications:


```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install Docker packages:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```


Verify Docker installation:


```bash
docker --version
```


**Step 6: Obtain a Hugging Face Access Token**

## Get HuggingFace API Key 
**1- Create account in [HuggingFace](https://huggingface.co/)**

**2- Create an Access Token with `Write` permissions [here](https://huggingface.co/settings/tokens) and save it**

1. Create an account on Hugging Face.
2. Navigate to your account settings and generate an Access Token with 'Write' permissions.
3. Save this token securely; it will be required later.

**Step 7: Clone the RL Swarm Repository**

Download the RL Swarm project from GitHub:


```bash
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm
```


**Step 8: Run the RL Swarm Node**

To ensure the node continues running even after closing the terminal, use `screen`:

1. Start a new screen session:

   ```bash
   screen -S gensyn
   ```


2. Set up a Python virtual environment and activate it:

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```


3. Execute the setup script:

   ```bash
   ./run_rl_swarm.sh
   ```


4. During the setup, you'll be prompted with:

   - **"Would you like to connect to the Testnet? [Y/n]"**: Type `Y` and press Enter.
   - **"Would you like to push models you train in the RL swarm to the Hugging Face Hub? [y/N]"**: Type `y` and press Enter.
   - **"Please enter your Hugging Face access token:"**: Input the token you obtained earlier.

5. Once the setup completes, you can detach from the screen session by pressing `Ctrl + A`, then `D`. This allows the node to run in the background.

**Step 9: Monitor Node Activity**

To reattach to the screen session and monitor the node:


```bash
screen -r gensyn
```

end


To detach again, press `Ctrl + A`, then `D`.

**Additional Resources:**

- **Official Gensyn Testnet Page:** Provides an overview and additional details about the testnet. citeturn0search5
- **Community Support:** For assistance and to engage with other participants, consider joining the Gensyn Discord community.

By following these 
