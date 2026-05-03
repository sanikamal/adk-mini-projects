# My Config Agent

This is a configuration-based agent project generated with the Google Agent Development Kit (ADK).

## Overview
Instead of Python code, this project uses a `root_agent.yaml` file to configure the agent's model, description, and instruction. This approach allows for quick experimentation and easier version control without needing to write code.

## Quick Start
1. Ensure your virtual environment is activated.
2. Copy `env.example` to `.env` and add your API key.
3. Start the agent:
   ```shell
   adk web my_config_agent
   ```
4. Navigate to the provided local URL (typically `http://localhost:8000`) to interact with your agent.
