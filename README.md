# Wraiter

A full-stack BHVR AI assisted writing app.
powered by cloudflare workers.

## Why bhvr?

While there are plenty of existing app building stacks out there, many of them are either bloated, outdated, or have too much of a vendor lock-in. bhvr is built with the opinion that you should be able to deploy your client or server in any environment while also keeping type saftey. Also, I just wanted to try using hono for backend rather than following the MERN conventions which feels a bit restrictive, along with avoiding the few drawbacks that come with using npm.

## Features

- **Rich text editor** \- one that provides various styling options for your notes.
- **Save/delete** \- save/delete your notes across sessions.
- **AI** \- with the ollama model from meta, get the cutting edge help you need with your content.
- **pass context** \- pass your written text as context by including @writer in your prompt.

## Project Structure

```
.
├── client/               # React frontend
├── server/               # Hono backend
├── shared/               # Shared TypeScript definitions
│   └── src/types/        # Type definitions used by both client and server
└── package.json          # Root package.json with workspaces
```

```mermaid
graph TB
A[React Frontend] ----> B[AI Chat Interface]
A ----> C[Text Editor]
A ----> D[Side Bar]
B <----> E[Hono Backend]
C <----> E
D <----> E
E <----> F[Cloudflare Agents]
F <----> G[Cloudflare AI]
E <----> H[Cloudflare D1]
A --hosted using--> I(Cloudflare Pages)
E --hosted using--> J(Cloudflare Workers)
``` 

### Server

bhvr uses Hono as a backend API for it's simplicity and massive ecosystem of plugins. If you have ever used Express then it might feel familiar. Declaring routes and returning data is easy.

```
server
├── bun.lock
├── package.json
├── README.md
├── src
│   └── index.ts
└── tsconfig.json
```

### Client

Uses some components from shadcn, and a few other self-defined styles.
Uses the React + vite framework

## Getting Started

### Installation

```bash
# Install dependencies for all workspaces
bun install
```

### Development

```bash
# Run shared types in watch mode, server, and client all at once
bun run dev

bun run dev:server  # Run the Hono backend
bun run dev:client  # Run the Vite dev server for React
```

### Building

```bash
# Build everything
bun run build

# Or build individual parts
bun run build:shared  # Build the shared types package
bun run build:client  # Build the React frontend
```
