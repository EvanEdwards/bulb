# Wyze SDK Installation Guide

Note: this guide is AI created.  I sort of followed it.  I use Kubuntu.  YMMV.  Check out the original wyze-sdk project for more information, but I'll include this here just as a starting point for y'all.  

## Prerequisites

First, ensure you have Python 3.8 or higher installed:

```bash
python3 --version
```

If you need to install or upgrade Python:

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

## Installation Steps

### 1. Create a Virtual Environment (Recommended)

Create a dedicated virtual environment for the Wyze SDK to avoid conflicts:

```bash
mkdir -p ~/wyze-bulb-controller
cd ~/wyze-bulb-controller
python3 -m venv venv
source venv/bin/activate
```

### 2. Install Wyze SDK

Install the Wyze SDK using pip:

```bash
pip install wyze-sdk
```

### 3. Set Up Authentication

You'll need to set up authentication with Wyze. You have three options:

#### Option A: Using the Bulb Controller (Recommended)
The bulb controller can store your API credentials securely:

```bash
./bulb --auth
```

This will prompt you for your API key and ID, then store them in `~/.local/share/bulb/auth.rc`.

#### Option B: Environment Variables
Create a `.env` file or add to your shell profile:

```bash
export WYZE_EMAIL="your.email@example.com"
export WYZE_PASSWORD="your_password"
```

#### Option C: API Key Environment Variables
If you prefer environment variables for API keys:

```bash
export WYZE_API_KEY="your_api_key"
export WYZE_KEY_ID="your_key_id"
```

To get API credentials, visit: https://support.wyze.com/hc/en-us/articles/16129834216731

### 4. Verify Installation and Set Up Authentication

Test the installation and set up your Wyze API credentials:

```bash
# First, set up authentication
./bulb --auth

# Then test by listing your bulbs
./bulb --list
```

### 5. Create Directories for Bulb Controller

Create the necessary directories for the bulb controller application:

```bash
mkdir -p ~/.local/share/bulb
```

Note: The `bulb --auth` command will create this directory automatically if it doesn't exist.

### 6. Make the Bulb Script Executable (After Creating It)

After creating the bulb script, make it executable and optionally add it to your PATH:

```bash
chmod +x bulb
# Optional: Copy to a directory in your PATH
sudo cp bulb /usr/local/bin/
```

## Troubleshooting

### Permission Issues
If you encounter permission issues:

```bash
pip install --user wyze-sdk
```

### Missing Dependencies
If you get import errors, install additional dependencies:

```bash
sudo apt install python3-dev python3-setuptools
```

### Network Issues
Ensure your firewall allows outbound HTTPS connections to Wyze servers.

## Usage Notes

- Always activate your virtual environment before running the bulb controller:
  ```bash
  source ~/wyze-bulb-controller/venv/bin/activate
  ```

- If you want the bulb controller available globally, you can create a wrapper script in `/usr/local/bin/` that activates the virtual environment first.

- Keep your Wyze credentials secure and never commit them to version control.