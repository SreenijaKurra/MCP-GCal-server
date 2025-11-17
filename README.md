# MCP-GCal-server

Google Calendar **Model Context Protocol (MCP)** server with custom extensions, built for connecting AI assistants (like Claude Desktop or any MCP-compatible client) to your Google Calendar in a safe, structured way.

This server acts as a thin layer between an LLM and the Google Calendar API: the MCP client calls tools, the server translates those into Google Calendar operations, and returns structured results the model can reason about.

---

## Features

- **Full MCP server for Google Calendar**
  - Exposes Google Calendar operations as MCP tools.
  - Designed to plug directly into Claude Desktop / MCP clients.

- **Event & calendar management**
  - Read events from one or more calendars.
  - Create and update events with metadata (time, description, etc.).
  - Delete or cancel events.
  - Query upcoming events for a time window (e.g. “today”, “this week”).

- **“Proprietary extensions”**
  - Opinionated higher-level tools for scheduling workflows
    - e.g. helpers for:
      - Checking availability across a time range.
      - Summarizing a day or week of events.
      - Creating events with sensible defaults from natural language inputs.
  - Structured responses tuned for RAG/agent workflows rather than generic API dumps.

- **TypeScript + Node.js**
  - Strongly-typed server implementation.
  - Clear separation between:
    - MCP protocol wiring.
    - Google Calendar API integration.
    - Auth/credential handling.

- **Local-first authentication**
  - Uses your own Google Cloud project + OAuth credentials.
  - Tokens are stored locally (no external backend).
  - You keep control of your data and credentials.

---

## Architecture (High-Level)

At a high level, the project is structured as:

- `src/`
  - **MCP server entrypoint** – wires up the MCP server, registers tools, and starts listening for MCP client connections (stdio or network, depending on how you run it).
  - **Google Calendar client** – wraps Google’s Calendar API for:
    - Listing calendars
    - Listing events
    - Creating / updating / deleting events
  - **Auth & token handling** – manages OAuth flows and token persistence.
  - **Schemas / types** – TypeScript types and schemas for requests and responses.

- Root files:
  - `package.json` – npm scripts and dependencies.
  - `tsconfig.json` – TypeScript configuration.
  - `LICENSE` – mixed license: Anthropic MIT portions plus proprietary extensions.
  - `.nvmrc` – recommended Node.js version.

> **Note:** Some parts of this server are derived from Anthropic’s reference Google Calendar MCP server and remain MIT-licensed; your proprietary logic and extensions are All Rights Reserved (see `LICENSE` in the repo for details).

---

## Prerequisites

- **Node.js** (version specified in `.nvmrc`, or a recent LTS).
- **npm** or **pnpm**.
- A **Google account** with access to Google Calendar.
- A **Google Cloud project** with **Google Calendar API** enabled.
- OAuth 2.0 credentials:
  - Client ID
  - Client Secret
  - Authorized redirect URI (for the auth flow).

---

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/SreenijaKurra/MCP-GCal-server.git
cd MCP-GCal-server


```


























## License

- Portions © 2024 Anthropic, PBC under the MIT License (see [LICENSE](./LICENSE)).
- All other code and modifications © 2025 Sreenija Kurra, All Rights Reserved.
