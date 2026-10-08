# AI_DEVS_4_publ

This repository contains two experimental notebooks from the AI DEVS challenge series, both focused on agentic LLM patterns and task-solving workflows.

## Repository contents

### S02E03.ipynb

This notebook implements an orchestrator-based agent architecture for the "failure" log analysis task.

The core idea is a hierarchical structure:

- A Lead Orchestrator manages the task and decides what information is missing.
- A specialized Sub-agent is spawned to analyze, filter, and compress the raw log data.
- The orchestrator uses the sub-agent output, validates the result, and submits the final condensed log through the verification API.

In practical terms, the notebook:

- downloads the failure log from the AI DEVS/agent hub,
- parses log lines into a pandas table,
- extracts timestamps, severity levels, and component names,
- filters log entries by level, component, and regex criteria,
- delegates the filtering/compression work to a dedicated agent,
- sends the final cleaned log payload for grading.

This is a classic supervisor-subordinate design: one agent coordinates strategy while another performs targeted analysis work.

### S03E05.ipynb

This notebook demonstrates a different multi-agent pattern: two distinct agents work together, but with a clear separation of responsibilities.

The architecture is:

- an information-gathering agent whose job is to explore the available tools, map data, vehicles, movement rules, and resource constraints,
- a second agent that receives the gathered findings and handles the actual planning/decision-making for the mission.

In this notebook, the first agent repeatedly queries the tool search API to build a structured inventory of available domains such as maps, vehicles, movement rules, and resource management. The second agent then uses those discoveries to reason about a route through a 10x10 grid world, choose a vehicle, manage food and fuel constraints, and produce a travel plan.

This pattern separates reconnaissance from execution: the discovery agent focuses on data collection, while the planning agent focuses on strategy and final output.

## Summary

These two notebooks showcase two different agent design patterns:

- S02E03: orchestrator + sub-agent hierarchy
- S03E05: information gathering + decision-making agent split

Together they illustrate how agentic workflows can be structured around delegation, specialization, and task separation.

## Technical notes

- The notebooks use Python with libraries such as pandas, requests, OpenAI-compatible API clients, and regex-based log processing.
- The code reads API keys from local files such as klucz_API_AIDEVS.txt and klucz_API_openrouter.txt.
- They are intended to be run in a Jupyter environment.
