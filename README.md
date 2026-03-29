# Hello World Temporal

[![TypeScript](https://img.shields.io/badge/TypeScript-6.0-blue.svg)](https://www.typescriptlang.org/)
[![Temporal](https://img.shields.io/badge/Temporal-1.15-purple.svg)](https://temporal.io/)
[![License: ISC](https://img.shields.io/badge/License-ISC-green.svg)](https://opensource.org/licenses/ISC)

A simple example demonstrating how to use [Temporal](https://temporal.io/) with TypeScript. This project showcases the basics of Temporal workflows, activities, and workers.

## What is Temporal?

Temporal is a durable execution platform that helps developers build reliable, scalable applications. It handles failures, retries, and state management automatically, allowing you to write code as if failures don't exist.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Build and Run](#build-and-run)
- [Development](#development)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v22 or higher)
- **Yarn** (v1.22 or higher)
- **Temporal CLI** - Install via Homebrew on macOS:
  ```bash
  brew install temporal
  ```

## Project Structure

```
helloworld-temporal/
├── src/
│   └── hello-world/
│       ├── activities.ts   # Activity implementations
│       ├── client.ts       # Workflow client to start workflows
│       ├── worker.ts       # Worker that executes workflows and activities
│       └── workflows.ts    # Workflow definitions
├── dist/                   # Compiled JavaScript output
├── package.json
├── tsconfig.json
└── README.md
```

## Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/indrabasak/helloworld-temporal.git
   cd helloworld-temporal
   ```

2. **Install dependencies:**
   ```bash
   yarn install
   ```

## Build and Run

### 1. Build the Project

Compile the TypeScript code:

```bash
yarn build:hello-world
```

### 2. Start the Temporal Server

Start the Temporal development server with a local SQLite database:

```bash
temporal server start-dev --db-filename indra_temporal.db
```

> **Note:** The Temporal Web UI will be available at http://localhost:8233

### 3. Start the Worker

In a **new terminal**, start the worker to listen for tasks:

```bash
yarn start:hello-world
```

You should see output similar to:
```
Worker started, listening on task queue: hello-world
```

### 4. Run the Workflow

In **another terminal**, trigger the Hello World workflow:

```bash
yarn start:hello-world:workflow
```

**Expected Output:**

In the client terminal:
```
Started workflow workflow-<unique-id>
Hello, Temporal!
```

## Development

### Available Scripts

| Script | Description |
|--------|-------------|
| `yarn build:hello-world` | Compile TypeScript to JavaScript |
| `yarn start:hello-world` | Start the Temporal worker |
| `yarn start:hello-world:workflow` | Run the Hello World workflow |
| `yarn lint` | Run ESLint to check for code issues |
| `yarn lint:fix` | Automatically fix linting issues |

### How It Works

1. **Workflow (`workflows.ts`)**: Defines the `example` workflow that calls the `greet` activity
2. **Activity (`activities.ts`)**: Implements the `greet` function that returns a greeting message
3. **Worker (`worker.ts`)**: Creates a worker that polls the task queue and executes workflows/activities
4. **Client (`client.ts`)**: Starts a new workflow execution and retrieves the result

## Troubleshooting

### Common Issues

**Worker fails to connect:**
- Ensure the Temporal server is running before starting the worker
- Check that the server is accessible at `localhost:7233`

**Build errors with TypeScript:**
- Make sure you have the correct Node.js version (v22+)
- Run `yarn install` to ensure all dependencies are installed

**Workflow not executing:**
- Verify the worker is running and listening on the correct task queue (`hello-world`)
- Check the Temporal Web UI at http://localhost:8233 for workflow status

## Resources

- [Temporal Documentation](https://docs.temporal.io/)
- [Temporal TypeScript SDK](https://docs.temporal.io/develop/typescript)
- [Temporal TypeScript SDK GitHub](https://github.com/temporalio/sdk-typescript)
- [Temporal Web UI](http://localhost:8233) (when server is running)

## License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.

## Author

**Indra Basak** - [GitHub](https://github.com/indrabasak)
