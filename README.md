# AI/MCP assisted DevOps workflows

## The issue


After Developers recently started using ClaudeCode/Copilot in their coding work the number of required deployment/releases/changes/reviews/approvals to infrastructure spiked at least 30-40% while legacy DevOps workflow still involves manually processed ticket queue (TicketOps), same with pre-AI CI/CD pipelines - they were not designed for increased velocity and needs re-design.



## Proposed solutions


1. The Autonomous AI/MCP Self-Service Infrastructure Workflow - replaces DevOps TicketOps.
2. Production Incident  investigation by Operations/SRE are assisted by AI/MCP querying actual infrastructure (AWS), observability (DataDog) and CI/CD tools (GitHub Actions).
3. AI assisted Instrumenting applications with compliant observability tools (OTEL, DD agent, metrics,logs, traces, alerts, dashboards).


## Pre-requirements


- AI agents are configured with required AuthN/AuthZ and RBAC to 3pv API SaaS and least privileged Just-In-Time access permissions are used

Set of Standards and Compliance requirements for Infrastructure, Observability, CI/CD pipelines are defined, maintained and regularly updated from central repository

- AI Prompts/actions are monitored, logged and validated to avoid too wide privileges or hallucinated changes to production Infrastructure, Data, Networks

- Governance, Audit and Supervision is implemented to make sure  no rogue prompts/skills/requests are applied to production agentic flows.


MCP servers can solve the first  and the third pre-requirements. DevOps/Architects/Vendor community should collectively work on the second - defining standards and compliance requirements.


## Developer’s Self-Service Infrastructure flow adopted to existing tech stack and public cloud



Quote:

"Developers request infrastructure resources directly from their IDE using natural language (perhaps using inputs from approved Cloud Architecture document). The MCP server translates intent into production-ready Terraform, enforces org policies at the point of request, and routes for approval without the DevOps engineer becoming a human ticket resolver.

The key mechanism is policy enforcement at generation time, not review time. If a developer asks for an EC2 instance type that violates cost governance policy, they see the violation immediately with compliant alternatives before any ticket is created or any engineer's time is spent. Security groups, IAM role ARNs, tagging standards, compliance guardrails: all enforced invisibly at the moment infrastructure is defined.
"

## Components

- AI agent with properly configured approved set of MCP servers

- Central company repository with Infra/CI/CD/Security-related compliance requirements (aka as standards and/or metadata, e.g. .md context layer) that used as RAG (Retrieval-Augmented Generation) context

- Remote MCP servers that connects AI agentic workflows with upstream APIs (AWS, GitHub) and provide tools, authN/authZ, skills, documentation etc to decrease hallucination and improve autonomy

- RBAC, Audit, Prompt validation proxies or other mechanism of AI agent/MCP server security and governance preventing unwanted or dangerous changes to production artefacts


## The Autonomous AI/MCP Self-Service Infrastructure Workflow


### The Intent: 

A developer prompts the agent: "I need a standard secure PostgreSQL database for a new microservice called 'billing' in staging." [1]

### Context Gathering (MCP):

The AI Agent uses the Filesystem MCP to find your organization's verified PostgreSQL Terraform module. It automatically extracts mandatory variables. [1, 2]

### Drafting & Auto-Tagging: 

The AI writes the configuration. It automatically injects the tags (Service: billing, Env: staging, CreatedBy: AI-Platform-Agent) based on the prompt context.

### Day-1 Observability Injection: 

The AI automatically appends an OpenTelemetry sidecar config or a Datadog monitor resource to the pull request because its system prompt mandates "never deploy databases without an alert metric."

### Pre-Flight Compliance Check (MCP):

The AI pipes the draft code through the Compliance MCP Server. If Checkov returns a warning (e.g., Database public access not explicitly disabled), the AI catches it, rewrites the code to fix the vulnerability, and tests it again. [1]

### GitOps Execution:

The AI opens a Clean Pull Request. A human platform engineer simply reviews the automated compliance logs and clicks "Merge" to let Atlantis or GitHub Actions deploy it. [1]


