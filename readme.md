# JARVIS - Personal Voice AI Assistant

This repository is a customized and actively maintained version of a JARVIS-style voice assistant for Windows.

- Maintainer: Rohit Ramakant Prajapati
- Repository: [J.A.R.V.I.S](https://github.com/Rohitramakantprajapati/J.A.R.V.I.S)

## About This Project

JARVIS is a real-time assistant that listens to voice input, responds with voice output, and executes practical tasks on the computer.
It is designed for everyday productivity, automation, and smart desktop control.

## Attribution and My Work

This project is based on an existing open-source JARVIS/Mark-style assistant codebase.

My work in this repository includes:
- Runtime fixes and startup behavior improvements
- Documentation rewrite and project cleanup
- Project structure notes and interview documentation
- Branding, setup messaging, and repository preparation updates

If you use this repository, keep attribution to the original open-source work where required by license.

## What JARVIS Can Do

- Real-time voice conversation
- Open and control desktop applications
- Run browser automation and web search
- Send messages and set reminders
- Manage files and run command workflows
- Use screen/camera processing features
- Remember useful user context with persistent memory
- Execute multi-step tasks with planner and executor modules

## Main Architecture

- `main.py`: Starts runtime, audio loops, live model connection, and tool dispatch
- `ui.py`: JARVIS interface and runtime status log
- `actions/`: Modular tool handlers for apps, browser, messaging, files, and system tasks
- `agent/`: Planning, execution, queueing, and error recovery logic
- `memory/`: Long-term memory and configuration helpers
- `core/prompt.txt`: System behavior prompt
- `config/api_keys.json`: Local API key file

## Requirements

- Windows 10 or 11
- Python 3.10 or newer
- Working microphone
- Gemini API key

## Setup Steps

1. Clone this repository
2. Install dependencies using `setup.py` or `requirements.txt`
3. Install Playwright browser binaries
4. Run `main.py`
5. Enter your own Gemini API key when prompted

## API Key and Privacy

This repository should not include personal API keys.
Each user who downloads this project must insert their own Gemini API key locally.

## Ownership

This customized repository is maintained by Rohit Ramakant Prajapati.
