# Sales-Development-Representive

# Sales Development Representative Agent

An AI-powered Sales Development Representative workflow built with the OpenAI Agents SDK.

This project automates the process of generating, evaluating, formatting, and sending cold sales emails using a multi-agent system. Different sales agents create email drafts with different tones, a sales manager agent selects the strongest draft, and an email manager agent formats and sends the final email.

## What It Does

The system can:

- Generate multiple cold sales email drafts
- Use different sales agent styles such as professional, engaging, and concise
- Select the strongest email using a manager agent
- Create a subject line for the selected email
- Convert the email body into HTML
- Send the final email using SendGrid
- Stream agent output in real time
- Use OpenAI tracing to inspect agent workflows
- Input guardrails to check whether requests are relevant and safe for the SDR workflow

## Tech Stack

- Python
- OpenAI Agents SDK
- OpenAI API
- SendGrid
- python-dotenv
- asyncio
- Function tools
- Agent handoffs
- OpenAI tracing
- Input guardrails

## Key Features

- Multi-agent SDR workflow
- Parallel email generation using multiple agents
- Agent-as-tool pattern for reusable sales agents
- Function tool for sending emails
- Handoff from Sales Manager to Email Manager
- HTML email formatting workflow
- Subject-line generation agent
- Real-time streamed output
- Traceable execution flow using OpenAI traces

## Project Structure

```text
sales-development-representative-agent/
├── sales_dev_rep.ipynb
├── main.py
├── requirements.txt
├── .env
├── .gitignore
└── README.md
```

## How It Works

The project is built around a small team of agents.

First, three sales agents generate cold email drafts using different communication styles:

- Professional Sales Agent
- Engaging Sales Agent
- Busy Sales Agent

Each agent is converted into a tool so the Sales Manager can call them when needed.

The Sales Manager agent then:

1. Calls the sales agent tools to generate multiple drafts
2. Compares the drafts
3. Selects the strongest email
4. Hands off the selected draft to the Email Manager

The Email Manager agent then:

1. Uses a subject writer tool to create a subject line
2. Uses an HTML converter tool to format the email body
3. Uses a SendGrid function tool to send the final email

This demonstrates how agents can collaborate through tools and handoffs to complete a business workflow end to end.

## Agentic Design Patterns Used

This project uses several agentic AI patterns:

### Agent Workflow

Multiple agents are used in sequence to complete a larger task.

### Agents as Tools

Each sales agent is exposed as a tool so the Sales Manager can call them and compare their outputs.

### Function Tools

Python functions are wrapped as tools using `@function_tool`, allowing agents to perform real actions such as sending email.

### Handoffs

The Sales Manager hands off the selected email to the Email Manager, which takes over formatting and delivery.

### Parallel Execution

The sales agents can generate drafts in parallel using `asyncio.gather`.

### Streaming

The project supports streamed model output so generated text can be displayed as it is produced.

### Tracing

OpenAI traces are used to inspect how agents, tools, and handoffs interact during execution.

## Environment Variables

The project uses environment variables for API keys and email configuration.

```text
OPENAI_API_KEY=
SENDGRID_API_KEY=
```

The SendGrid sender email must be verified in SendGrid before emails can be sent.

## Guardrails

The project includes guardrails to make the SDR agent workflow safer and more controlled.

Guardrails help check user input before the main agent continues with the task. This is useful because the system is designed for a specific workflow: generating and sending cold sales emails. If the input is unrelated, unsafe, or outside the expected use case, the guardrail can stop or redirect the workflow before the agents start acting on it.

In this project, guardrails are used to:

- Validate whether the request is relevant to sales outreach
- Prevent the workflow from handling unrelated tasks
- Add an extra safety layer before email generation or sending
- Keep the agent focused on SDR-style email workflows

This makes the system more reliable because the Sales Manager agent does not blindly process every user request.

## Requirements

```text
python-dotenv
openai
openai-agents
sendgrid
```

## Privacy and Security

API keys and email credentials should not be committed to GitHub.

The `.env` file should stay local and be included in `.gitignore`.

## Future Improvements

- Add support for sending emails to a prospect list
- Add lead personalization based on company or prospect data
- Add approval step before sending emails
- Add reply tracking using SendGrid webhooks
- Add CRM-style logging for sent emails
- Add a simple UI for entering prospect details
- Add safeguards to prevent accidental bulk sending

## Status

Core project completed.

The project currently supports multi-agent email generation, best-draft selection, subject generation, HTML formatting, SendGrid email sending, tool usage, handoffs, input guardrails, streaming, and tracing.