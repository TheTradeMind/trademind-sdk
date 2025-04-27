# TradeMind SDK

A TypeScript library designed to provide a simple, programmatic interface for interacting with the TradeMind Agent Network through the [TradeMind API](https://trademind-api.vercel.app/).

## Installation

```bash
npm install trademind-sdk
```

## Configuration

The SDK requires an API key to authenticate with the TradeMind API:

```bash
# TradeMind API Configuration
TRADEMIND_API_KEY=your_api_key
# Optional: Custom API URL (defaults to https://trademind-api.vercel.app)
TRADEMIND_API_URL=custom_api_url
```

You can also provide these directly when initializing the SDK:

```typescript
const sdk = TradeMindSDK.initialize({
  apiKey: 'your_api_key',
  // Optional: custom API URL
  apiUrl: 'https://custom-api-url.com'
});
```

## Usage

```typescript
import { TradeMindSDK } from 'trademind-sdk';

// Initialize the SDK
const sdk = TradeMindSDK.initialize();

// Create a new agent
async function createAgent() {
  const agent = await sdk.createAgent({
    name: 'Trading Expert',
    personality: 'Professional, analytical, and insightful',
    description: 'An AI assistant specializing in financial markets and trading strategies',
    model: 'gpt-4' // or 'gpt-3.5-turbo'
  });
  
  console.log('Created agent:', agent);
}

// List all agents
async function listAgents() {
  const agents = await sdk.listAgents();
  console.log('Available agents:', agents);
}

// Get an agent by name
async function getAgent() {
  const agent = await sdk.getAgentByName('Trading Expert');
  if (agent) {
    console.log('Found agent:', agent);
  } else {
    console.log('Agent not found');
  }
}

// Chat with an agent
async function chatWithAgent() {
  const response = await sdk.chatWithAgent(
    'Trading Expert', 
    'What are your thoughts on the current market conditions?'
  );
  
  console.log('Agent response:', response);
}
```

## API Reference

The SDK interacts with the following TradeMind API endpoints:

- `POST /api/agents` — Create a new agent
- `GET /api/agents` — List all agents
- `GET /api/agents/:name` — Get details of a specific agent by name
- `POST /api/agents/:name/chat` — Send a message to an agent and get a response

### SDK Methods

#### `TradeMindSDK.initialize(config?: TradeMindSDKConfig): TradeMindSDK`

Initializes the SDK with the provided configuration or environment variables.

#### `createAgent(agentData: CreateAgentDTO): Promise<Agent>`

Creates a new agent with the provided data.

#### `listAgents(): Promise<Agent[]>`

Lists all available agents.

#### `getAgentByName(name: string): Promise<Agent | null>`

Gets an agent by name, or returns null if not found.

#### `chatWithAgent(agentName: string, message: string): Promise<string>`

Sends a message to an agent and returns their response.

## License

MIT 