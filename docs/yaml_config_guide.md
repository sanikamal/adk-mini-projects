# Agent Config (YAML) Guide

## Two ways to define agents
we created agents using Python code in `agent.py`:
```python
from google.adk.agents.llm_agent import Agent

root_agent = Agent(
    model='gemini-2.5-flash',
    name='math_tutor_agent',
    description='Helps students learn algebra',
    instruction='You are a patient math tutor...'
)
```
This works great for development. But ADK also supports defining agents using YAML configuration files, which can be easier for:
*   Non-programmers to edit
*   Version control and sharing
*   Quick experimentation
*   Separating configuration from code

This guide introduces Agent Config, which is ADK's YAML-based approach to building agents.

### Language support note
Important: ADK supports multiple programming languages:
*   **Python**: Full support for both Python code and YAML Agent Config
*   **Java**: Supports Python code-based agents

*Agent Config (YAML) is currently Python-only.*

---

## 2 methods to define agents

### Method 1: Python code
Created with: `adk create my_agent`
Generates:
```
my_agent/
 ├── agent.py      # Python code defining your agent
 ├── __init__.py
 └── .env
```

### Method 2: YAML configuration
Created with: `adk create --type=config my_agent`
Generates:
```
my_agent/
 ├── root_agent.yaml   # YAML configuration file
 └── .env
```
Notice the `--type=config` flag. This tells ADK to create a YAML-based agent instead of the default Python code-based agent.

---

## Creating a YAML-based agent

### Step 1: Create the agent project
Run the following command to create a config-based agent:
```shell
adk create --type=config my_config_agent
```

### Step 2: Configure your API key
Configure your `.env` file with your API key, just as you would for a Python-based agent. Add your `GOOGLE_API_KEY`.

### Step 3: Edit the YAML configuration
Instead of writing Python code, you'll edit a YAML file. Open `root_agent.yaml`.

The default generated file looks like this:
```yaml
# yaml-language-server: $schema=https://raw.githubusercontent.com/google/adk-python/refs/heads/main/src/google/adk/agents/config_schemas/AgentConfig.json

name: assistant_agent
model: gemini-2.5-flash
description: A helper agent that can answer users' questions.
instruction: You are an agent to help answer users' various questions.
```

**Understanding YAML syntax:**
*   **`name`**: The agent's unique identifier
*   **`model`**: Which LLM to use
*   **`description`**: What the agent does (for other agents to understand)
*   **`instruction`**: How the agent should behave
*   The vertical bar `|` after `instruction:` tells YAML everything that follows is multi-line text.

**Example of a customized agent (`root_agent.yaml`):**
```yaml
# yaml-language-server: $schema=https://raw.githubusercontent.com/google/adk-python/refs/heads/main/src/google/adk/agents/config_schemas/AgentConfig.json

name: math_tutor_agent
model: gemini-2.5-flash
description: Helps students learn algebra by guiding them through problem-solving steps.
instruction: |
  You are a patient and encouraging algebra tutor.

  Your teaching approach:
  1. When a student asks a question, first understand what they're struggling with
  2. Break down the problem into smaller, manageable steps
  3. Guide them to discover the answer rather than giving it directly
  4. Provide positive reinforcement for effort and progress
  5. Use simple language and avoid jargon

  Always maintain a supportive, patient tone. Learning takes time, and every
  question is an opportunity to grow.
```

### Step 4: Run your YAML-based agent
Running a YAML-based agent is exactly the same as running a Python-based agent:
```shell
adk web my_config_agent
```

---

## YAML versus Python: When to use each

Both methods create agents that work identically, but they're suited for different scenarios.

| Aspect | YAML config | Python code |
| :--- | :--- | :--- |
| **Ease of editing** | Very easy (text file) | Requires coding knowledge |
| **Best for** | Simple agents, quick prototypes | Complex agents, custom logic |
| **Version control** | Clean differences | Code changes |
| **Flexibility** | Limited to config options | Full programmatic control |
| **Non-programmers**| Can edit | Need coding skills |
| **Advanced features**| Coming soon | Full access |

### Choose YAML when:
*   **You want simplicity and accessibility.** Non-programmers can easily edit a YAML file.
*   **You need quick experimentation.** Edit the YAML file, and restart your agent.
*   **Configuration should be separate from code.** Makes it easier to manage different configurations across environments.

### Choose Python when:
*   **You're building complex multi-agent systems.** Workflows, delegation, and custom orchestration require Python code.
*   **You need custom tools and callbacks.** Advanced features require Python code.
*   **You want programmatic control.** Dynamically generate configurations or integrate tightly with other Python libraries.

---

## Key takeaways
*   ADK gives you flexibility in how you define agents.
*   YAML configuration shines when you need quick experimentation or when non-technical team members need to adjust agent behavior.
*   Python code becomes essential as your agents grow more sophisticated.
*   Both methods are first-class citizens in ADK. Pick the approach that best fits your current needs.
