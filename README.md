# Open WebUI + Jupyter

Leveraging Docker, this project provides a quick and easy way to setup Open WebUI and Jupyter, to take advantage of a [recently added integration](https://github.com/open-webui/open-webui/releases/tag/v0.5.11) that allows Open WebUI to use Jupyter as the engine for executing Python code generated in chats. 

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)

## Overview

The purpose of this project is very simple. Provide a way to very easily spin up both an instance of Open WebUI next to an instance of Jupyter to allow for seamless integration of Code execution and Code interpretation within Open WebUI, leveraging Jupyter as the engine.

## Features

It's really just a `docker-compose.yml` file that helps setup and install Open WebUI and Jupyter in a Docker container. The `docker-compose.yml` contains necessary parameters to enable remote access of Jupyter as it sets it up. As long as you have both Git and Docker installed, you can simply clone the repo and run `docker compose up -d` in a terminal to install and run the software. The rest of this Readme details how to setup the integration of Open WebUI and Jupyter.

## Prerequisites

Before you begin, ensure you have the following installed:
- Docker
- Git

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/crazy-treyn/open-webui-jupyter.git
   ```

2. Navigate to the project directory containing the `docker-compose.yml` file:
   ```bash
   cd open-webui-jupyter
   ```

3. Start the Docker containers:
   ```bash
   docker compose up -d
   ```
   
   This will start both Jupyter and Open WebUI services:
   - Open WebUI: http://localhost:3000
   - Jupyter: http://localhost:8888 (token: `jupyter`)

   To stop the services at any time, run:
   ```bash
   docker compose down
   ```

   To upgrade to the latest version of Open WebUI and Jupyter, run:
   ```bash
   docker compose down && docker compose pull && docker compose up -d
   ```

## Configuration

### Setting up Open WebUI to use Juypter for Python code execution

1. Navigate to Open WebUI (http://localhost:3000)
2. Create an admin account
3. Configure Code Execution:
   - Click your `Name (bottom left corner) > Settings > Admin Settings > Code Execution`
   - Configure both Code Execution and Code Interpreter engines:
     - Change engine from pyodide to jupyter
     - Set Jupyter URL to http://host.docker.internal:8888
     - Set Jupyter auth to token
     - Set token value to `jupyter`
     - Save changes

4. Set up API Connections & Models:
   - Go to `Settings > Admin Settings > Connections` and add API connections.
   - Go to `Settings > Admin Settings > Models` and enable the Models you want accessible to interact with inside Open WebUI.

## Usage

1. Start a new chat in Open WebUI, and submit a prompot to generate a Python script that prints something to the terminal, like current working directory.
2. In the code cell in the top right, click `Run` and the code should execute and return the result below the code cell.