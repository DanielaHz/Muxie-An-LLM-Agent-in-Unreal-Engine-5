# Humanoid Challenge - Software Engineering

- ![OpenClaw.png](Assets/Demo-validation.gif)

This solution to the challenge uses Unreal Engine 5 as the environment where the 3D world lives, OpenAI 5.3 as the LLM “brain” of the agents, and OpenClaw as the agent platform.
To connect Unreal Engine and OpenClaw, I used the OpenClaw Unreal plugin available in the following repository:
https://github.com/TomLeeLive/openclaw-unreal-plugin

## Pipeline
- Unreal Engine: It is the standard software for real‑time applications, and it has also become very popular in robotic simulation environments thanks to its ability to simulate photorealistic environments, an aspect that is especially valuable when training robots in simulation.
- OpenAI 5.3:  I’ve been experimenting with LLMs for a couple of months, testing everything from local models to cloud solutions like DeepSeek, Claude Opus, and OpenAI. So far, in my experience, OpenAI’s models have delivered the most consistent and reliable results. Because of that, I consider OpenAI 5.3 a strong and affordable “brain” for this task.
- OpenClaw: In parallel with my LLM experimentation, I’ve been using OpenClaw for personal tasks, and I’m genuinely amazed by what it enables. The platform makes it surprisingly easy to build powerful agent workflows, and it has consistently delivered results.

## Project Spectations 
### virtual environment

The assets used to generate the next level were taken from FAB. They are open‑source, and the link to the author’s original source is: https://www.fab.com/listings/709924e0-3128-4d23-9d36-fe35991d03c0
![](Assets/env.png)

### Agent Current state

Define an observation format that represents the agent's current state and surroundings

### Actions

Define an action space the agent can use to interact with the world (e.g. move, turn, look, pick up)

### LLM

Wire up an LLM (e.g. Claude, GPT, or any model with an API) to observe state, reason, and choose actions in a loop

### Goal
- 
- Demonstrate the agent completing at least one goal-directed task (e.g. "go to the red cube", "find the key and open the door", "explore and describe the room")
  how you represent observations, why you chose your action space, what worked and what didn't

### Instructions to run the system 

### Inputs and outputs

### Design choices 

