# near-eliza-starter

The starter for building [Eliza](https://elizaos.github.io/eliza/) agents with [NEAR Protocol](https://near.org/) and [NEAR AI](https://docs.near.ai/), created with below awesome technology stack 🔥:

- LLM Model Provider: [NEAR AI](https://docs.near.ai)
- Agent Framework: [Eliza](https://elizaos.github.io/eliza/)
- Plugins
  - [plugin-near](https://github.com/elizaos-plugins/plugin-near) (NEAR)
  - [plugin-multichain](https://github.com/near-agent/plugin-multichain) (BTC / ETH, via [Chain Signatures](https://docs.near.org/chain-abstraction/chain-signatures))
- Memory
  - adapter-sqlite
- Actions / Tools
  - Transfer NEAR, BTC, ETH natively
  - Swap on Ref Finance
- Clients
  - REST API
  - Web Client

Multichain Features:

- For example, send native BTC with your NEAR account via [Chain Signatures](https://docs.near.org/chain-abstraction/chain-signatures)

![dbef7cf3-f79f-430c-9497-f92b61c9d151](https://github.com/user-attachments/assets/6b2c5319-b18f-4eb9-af7a-a3bccb9f6733)



## Prepare Environment

### 1. Install NEAR AI CLI

NEAR AI provides free agent hosting and inference APIs. You can skip this step if you want to use other model providers.

Install NEAR AI CLI following the instructions in https://docs.near.ai/cli. 

```bash
# python 3.11 recommended
python3 -m pip install nearai
# Bitte Wallet is recommended for NEAR account creation
nearai login
```

### 2. Configure environment variables

Duplicate environment template

```bash
cp .env.example .env
```

Add your NEAR account and private key to `.env`

```env
NEAR_NETWORK=testnet
NEAR_RPC_URL=https://neart.lava.build
NEAR_ADDRESS=xxxx.testnet
NEAR_WALLET_SECRET_KEY=ed25519:xxxxxxxx
```

Specify the models to use, e.g. DeepSeek-R1

```env
SMALL_NEARAI_MODEL=  # Default: fireworks::accounts/fireworks/models/llama-v3p2-3b-instruct
MEDIUM_NEARAI_MODEL= # Default: fireworks::accounts/fireworks/models/llama-v3p1-70b-instruct
LARGE_NEARAI_MODEL=fireworks::accounts/fireworks/models/deepseek-v3  # Default: fireworks::accounts/fireworks/models/llama-v3p1-405b-instruct
IMAGE_NEARAI_MODEL=  # Default: fireworks::accounts/fireworks/models/playground-v2-5-1024px-aesthetic
```

## Install and Start Agent

> Node.js version >= 22 is required

### 1. Install pnpm

```bash
npm i -g pnpm
```

### 2. Install dependencies
```bash
# agent dependencies
pnpm i
# web client dependencies
cd client && pnpm i && cd ..
```

### 3. Start agent

In one terminal session, start the agent server, in interactive mode by default.

```bash
pnpm start
```

### 4. Start web client

Start the web client in another terminal session

```bash
pnpm start:client
```

## Customize Your Agent

### Custom characters

Open `src/character.ts` to modify the default character.

To load custom characters instead:
- Use `pnpm start --characters="path/to/your/character.json"`
- Multiple character files can be loaded simultaneously

### Add more clients

Add Discord and Twitter for example

```
# in character.ts
clients: [Clients.TWITTER, Clients.DISCORD],

# in character.json
clients: ["twitter", "discord"]
```

Add login credentials and keys to `.env`

```
DISCORD_APPLICATION_ID="discord-application-id"
DISCORD_API_TOKEN="discord-api-token"

TWITTER_USERNAME="username"
TWITTER_PASSWORD="password"
TWITTER_EMAIL="your@email.com"
```

### Use a different model provider

Use OpenRouter for example

```
# in character.ts
modelProvider: ModelProviderName.OPENROUTER,

# in character.json
"modelProvider": "openrouter",
```

Edit environment variable

```
OPENROUTER_API_KEY="sk-xx-xx-xxx"
```
