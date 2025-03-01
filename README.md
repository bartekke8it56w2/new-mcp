# Model Context Protocol - Gemini Thinking Server

This is an implementation of the Model Context Protocol (MCP) that integrates with Google's Gemini API to provide analytical thinking capabilities without code generation.

## Overview

The Gemini Thinking Server is a specialized MCP server that leverages Google's Gemini model to provide sequential thinking and problem-solving capabilities. It allows for:

- Breaking down complex problems into steps
- Planning and design with room for revision
- Analysis that might need course correction
- Problems where the full scope might not be clear initially

## Features

- **Gemini-Powered Thinking**: Utilizes Gemini's analytical capabilities to generate thoughtful responses
- **Meta-Commentary**: Provides insights into the reasoning process
- **Confidence Levels**: Indicates how confident Gemini is in its analysis
- **Alternative Paths**: Suggests different approaches to the problem
- **Branching Thoughts**: Allows exploration of different thought paths
- **Revision Capability**: Supports revising previous thoughts
- **Session Persistence**: Save and resume analysis sessions

## Installation

```bash
# Clone the repository
git clone <repository-url>

# Install dependencies
npm install

# Build the project
npm run build
```

## Usage

### Environment Setup

Before running the server, you need to set up your Gemini API key:

```bash
export GEMINI_API_KEY=your_api_key_here
```

### Running the Server

```bash
node dist/gemini-index.js
```

### Tool Parameters

The `geminithinking` tool accepts the following parameters:

- `query` (required): The question or problem to analyze
- `context` (optional): Additional context information
- `approach` (optional): Suggested approach to the problem
- `previousThoughts` (optional): Array of previous thoughts for context
- `thought` (optional): Your current thinking step (if empty, will be generated by Gemini)
- `nextThoughtNeeded` (required): Whether another thought step is needed
- `thoughtNumber` (required): Current thought number
- `totalThoughts` (required): Estimated total thoughts needed
- `isRevision` (optional): Whether this revises previous thinking
- `revisesThought` (optional): Which thought is being reconsidered
- `branchFromThought` (optional): Branching point thought number
- `branchId` (optional): Branch identifier
- `needsMoreThoughts` (optional): If more thoughts are needed

### Session Management

The tool also supports session management commands:

- `sessionCommand`: Command to manage sessions ('save', 'load', 'getState')
- `sessionPath`: Path to save or load the session file (required for 'save' and 'load' commands)

#### Example: Saving a Session

```json
{
  "sessionCommand": "save",
  "sessionPath": "/path/to/save/session.json",
  "query": "dummy",
  "thoughtNumber": 1,
  "totalThoughts": 1,
  "nextThoughtNeeded": false
}
```

#### Example: Loading a Session

```json
{
  "sessionCommand": "load",
  "sessionPath": "/path/to/load/session.json",
  "query": "dummy",
  "thoughtNumber": 1,
  "totalThoughts": 1,
  "nextThoughtNeeded": false
}
```

#### Example: Getting Session State

```json
{
  "sessionCommand": "getState",
  "query": "dummy",
  "thoughtNumber": 1,
  "totalThoughts": 1,
  "nextThoughtNeeded": false
}
```

## Example

Here's an example of how to use the tool:

```json
{
  "query": "How might we design a sustainable urban transportation system?",
  "context": "The city has 500,000 residents and currently relies heavily on personal vehicles.",
  "approach": "Consider environmental, economic, and social factors.",
  "thoughtNumber": 1,
  "totalThoughts": 5,
  "nextThoughtNeeded": true
}
```

## Response Format

The server responds with:

```json
{
  "thought": "The generated thought from Gemini",
  "thoughtNumber": 1,
  "totalThoughts": 5,
  "nextThoughtNeeded": true,
  "branches": [],
  "thoughtHistoryLength": 1,
  "metaComments": "Meta-commentary about the reasoning",
  "confidenceLevel": 0.85,
  "alternativePaths": ["Alternative approach 1", "Alternative approach 2"]
}
```

## Example Clients

Several example clients are provided to demonstrate different use cases:

- `sample-client.js`: Basic client example
- `example-usage.js`: Specific usage example
- `codebase-analysis-example.js`: Example for codebase analysis
- `session-example.js`: Example demonstrating session persistence
- `advanced-filtering-example.js`: Example demonstrating advanced semantic filtering

To run the session example:

```bash
node dist/session-example.js
```

To run the advanced filtering example:

```bash
node dist/advanced-filtering-example.js
```

## License

MIT