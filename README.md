# Humanoid Challenge - Software Engineering

***Demo 1: World state querying: the agent counts all instances of a specific Blueprint object in the level in real time***
![OpenClaw.png](Assets/Demo-validation.gif)(https://drive.google.com/file/d/1yCiU0ErI--wYDydDgTGZUlIBayBf9atg/view?usp=drive_link)


This solution uses Unreal Engine 5 as the environment where the 3D world lives, OpenAI 5.3 as the LLM “brain” of the agents, and OpenClaw as the agent platform.
To connect Unreal Engine and OpenClaw, I used the OpenClaw Unreal plugin available in the following repository:
https://github.com/TomLeeLive/openclaw-unreal-plugin

## Pipeline and design choices

![](Assets/pipeline.svg)

- **Unreal Engine:** It is the standard software for real‑time applications, and it has also become very popular in robotic simulation environments thanks to its ability to simulate photorealistic environments, an aspect that is especially valuable when training robots in simulation.
- **OpenAI 5.3:**  I’ve been experimenting with LLMs for a couple of months, testing everything from local models to cloud solutions like DeepSeek, Claude Opus, and OpenAI. So far, in my experience, OpenAI’s models have delivered the most consistent and reliable results. Because of that, I consider OpenAI 5.3 a strong and affordable “brain” for this task.
- **OpenClaw:** In parallel with my LLM experimentation, I’ve been using OpenClaw for personal tasks, and I’m genuinely amazed by what it enables. The platform makes it surprisingly easy to build powerful agent workflows, and it has consistently delivered results.
- **OpenClawUE:** The bridge between Unreal Engine and OpenClaw through an MCP connection.

## Project Spectations 
### virtual environment
![](Assets/env.png)
The assets used to generate the next level were taken from FAB. They are open‑source, and the link to the author’s original source is: https://www.fab.com/listings/709924e0-3128-4d23-9d36-fe35991d03c0

### Characters

| Muxie (main Agent) | Bug (target) |
|--------------------|--------------|
| ![](Assets/muxie.png) | ![](Assets/bug.png) |

### Goal Task
The agent should be able to start the editor and navigate Muxie in the world, killing bugs autonomously. The muxie
can kill the bugs its jumping on the bug.

### Agent Current State

The agent's current state is observed through the OpenClaw UI, which displays
in real time the tools being called, the decisions being made, and the
actions being executed in the Unreal Editor.

Additionally, the `get_world_state` tool provides the agent with structured
information about its surroundings, including:

- Current position and rotation in the world
- Nearby bugs and their directions
- Number of bugs collected so far
- Total bugs remaining in the world

### Actions

To interact with the world, the agent needs to:

1. Start the editor in Play mode to spawn Muxie.
2. Navigate the world using the following actions:

- `move_forward`
- `move_backward`
- `move_left`
- `move_right`
- `jump`
- `rotate_view_camera`

### Collection Mechanic
Bugs are collected automatically when Muxie jump over the bugs and colide with the mesh.
A confetti effect spawns and the bug disappears from the world.

### LLM

The brain of the agent is the GPT-5.3-codex of OpenAI.  It was chosen for its strong reasoning results and competitive pricing per million tokens.

### Goal Validation
```
TODO: The Demo of the agent completing the task

```


### Instructions to Run the System

This setup requires the following running simultaneously:

1. **Unreal Engine 5.6**
2. **OpenClaw** running either via Docker container or installed locally on your machine
3. **Rider, VSCode, or Visual Studio** as the IDE to work with Unreal Engine

>Note: I'm aware this setup is not easy to replicate, but I chose to use the best tools and frameworks available in production-grade environments :)

#### Linux Installation

```bash
# Clone the repository
git clone https://github.com/DanielaHz/Muxie-An-LLM-Agent-in-Unreal-Engine-5.git
cd Muxie-An-LLM-Agent-in-Unreal-Engine-5

# to open project with Rider or vscode
rider .
code .
```

### Experimentation (what works and what not)

#### 1. Natural language prompt with limited context
![OpenClaw.png](Assets/demo2.gif)(https://drive.google.com/file/d/1l3n5s2sVqWyjfvs4_4F7SIFEXLEMT0Zs/view?usp=drive_link)
```
The agent receives a simple instruction in natural language with minimal information about the environment, available tools, or expected outcome.
- Input: Play the Editor level. Once the main character has been spawned, possess it and move it to position X=-330, Y=230, Z=52. The target yaw rotation should be 58°. The task is complete when the character is within an acceptable range of the target position.
- Output: The agent cloned the Blueprint of the main character at the position provided in the input instructions, but it did not move the actual main character as expected
- Comment: The provided input is insufficient to achieve the intended outcome.
```

2. Natural language prompt with full context

```
The agent receives a detailed instruction in natural language, including available tools, character state, world positions, and a clear definition of success.
- Input:
- Output:
- Comment:
```
3. Structured JSON task definition

```
The agent receives a formal JSON file describing the task, available tools, observations, and success conditions in a machine-readable format, reducing ambiguity and making the instructions more deterministic.
- Input:
- Output:
- Comment:
```
