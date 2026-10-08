# AI_DEVS_4_publ

This repository contains experimental notebook from the AI DEVS challenge series, focused on agentic LLM patterns and task-solving workflow.

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

## Technical notes

- The notebook uses Python with libraries such as pandas, requests, OpenAI-compatible API clients, and regex-based log processing.
- The code reads API keys from local files such as klucz_API_AIDEVS.txt and klucz_API_openrouter.txt.
- It is intended to be run in a Jupyter environment.
