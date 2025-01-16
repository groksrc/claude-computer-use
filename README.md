Here's a brief README to help others get started with the Claude Computer Use demo:

# Claude Computer Use Demo Setup Guide

This guide helps you set up and run the Claude Computer Use demo, which allows Claude to interact with a virtual desktop environment.

## Prerequisites
- Docker installed
- Python 3.x installed
- An Anthropic API key

## Installation Steps

1. Clone the repository:
```bash
mkdir -p ~/code/claude-computer-use
cd ~/code/claude-computer-use
git clone https://github.com/anthropics/anthropic-quickstarts.git
cd anthropic-quickstarts/computer-use-demo
```

2. Set up Python environment:
```bash
# Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate

# Install requirements
cd computer_use_demo
pip install -r requirements.txt
cd ..
```

3. Build the Docker image:
```bash
docker build -t claude-computer-use .
```

4. Run the container:
```bash
docker run -e ANTHROPIC_API_KEY=$ANTHROPIC_API_KEY \
    -v $HOME/.anthropic:/home/computeruse/.anthropic \
    -p 5901:5900 -p 8501:8501 -p 6080:6080 -p 8080:8080 \
    -it claude-computer-use
```

## Accessing the Demo

Once running, you can access the demo in two ways:
- VNC viewer at `localhost:5901`
- Web browser at `http://localhost:6080`

## Notes
- The default instructions use port 5900 for VNC by default, but port 5900 may already be in use (common on macOS). This demo will use port 5901 instead
- Claude interacts with the docker container in a secure environment, but care should still be taken to ensure it does not behave unexpectedly
- Make sure your `ANTHROPIC_API_KEY` environment variable is set before running the container

## Troubleshooting
- If you see a "user computeruse" error, make sure you're building the image from the provided Dockerfile rather than using the pre-built image
- On macOS, if VNC ports are in use, you can check running services with `sudo lsof -i :5900`
