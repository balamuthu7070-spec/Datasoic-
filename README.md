# Datasoic-# Datazoic Scalable Agentic System

## Problem

The task asks for an agentic system that can work with a very large number
of tools/APIs. The system should understand a natural-language request,
select the correct tool or sequence of tools, provide parameters, execute
the action, and return the result.

It should also support:

1. RAG Pipeline Tool
2. System Search Tool
3. Tool selection/routing
4. State management
5. Scalability
6. Error handling
7. Observability

## Current prototype

This implementation uses pure Python so it can run without an API key.

Flow:

User
  |
  v
Agent
  |
  v
Tool Router
  |
  v
Tool Registry
  |
  +---- PayPal Invoice Tool
  +---- Sales Report Tool
  +---- Dispute Tool
  +---- RAG Tool
  +---- System Search Tool
  |
  v
Result

## Run

Python 3.10+ recommended.

```bash
python main.py
```

Example requests:

- Send an invoice for $50
- What was my total sales volume last month?
- Is there a dispute open from user_123?
- Search the product documentation
- What tools are available?
- What is the status of my last request?

## Scaling to 100+ / 1000+ tools

Instead of placing every tool definition inside the LLM prompt:

1. Store tool metadata in a registry/database.
2. Create embeddings for tool descriptions.
3. Retrieve only top-k candidate tools.
4. Use an LLM/reranker to select the final tool.
5. Validate parameters with schemas.
6. Execute the selected tool.
7. Record state, errors and traces.
8. Add retries/timeouts/circuit breakers.
9. Use observability such as LangSmith/OpenTelemetry.

## Important

This is a prototype demonstrating the architecture.
The PayPal, RAG and system-search integrations are intentionally mocked.
For a production implementation, connect real APIs and an LLM-based
router/agent.
