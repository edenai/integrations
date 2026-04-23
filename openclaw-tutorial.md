# OpenClaw + Eden AI

Connect [OpenClaw](https://openclaw.ai) to Eden AI and route your agent through **500+ models** with smart routing, automatic fallbacks, and a single API key.

> Get your Eden AI key at [app.edenai.run](https://app.edenai.run/) → **API Keys**.

> Follow this tuto in the same time with our video tuto on Youtube : https://youtu.be/HxIAYOQT90Q 

---

## 1. System dependencies

On a fresh Linux machine (Ubuntu / Debian / WSL):

```bash
sudo apt update
sudo apt install -y curl git python3-venv
```

## 2. Install Node.js

OpenClaw requires **Node.js 22.14+** and **npm 9.8+**.

```bash
sudo apt install -y nodejs npm

# Verify
node --version   # v22.14.x or newer
npm  --version   # 9.8.x or newer
```

If the packaged version is too old, install via [nvm](https://github.com/nvm-sh/nvm) or [nodesource](https://github.com/nodesource/distributions).

## 3. Install OpenClaw

Pick one of the two methods below.

```bash
# Option A — official install script
curl -fsSL https://openclaw.ai/install.sh | bash

# Option B — via npm
npm install -g openclaw
```

Reload your shell so the `openclaw` binary is on your PATH:

```bash
source ~/.bashrc
```

## 4. Add Eden AI as a custom provider

OpenClaw stores its config at `~/.openclaw/openclaw.json`. Open it and add the Eden AI provider with the `@edenai` smart-router model:

```bash
nano ~/.openclaw/openclaw.json
```

```json
{
  "provider": {
    "edenai": {
      "name": "Eden AI",
      "baseURL": "https://api.edenai.run/v3/llm",
      "apiKey": "YOUR_EDEN_AI_API_KEY",
      "models": [
        {
          "id": "@edenai",
          "name": "@edenai (Custom Provider)",
          "contextWindow": 128000,
          "maxTokens": 16384,
          "input": ["text", "image"],
          "cost": {
            "input": 0,
            "output": 0,
            "cacheRead": 0,
            "cacheWrite": 0
          },
          "reasoning": false,
          "compat": {
            "requiresAssistantAfterToolResult": true,
            "supportsTools": false
          }
        }
      ]
    }
  }
}
```

### Why `@edenai`?

`@edenai` is Eden AI's **smart router**. For every request, it automatically picks the best-performing model based on quality, latency, cost and live provider health — so your OpenClaw agent always uses the right model without a config change.

[How smart routing works →](https://www.edenai.co/docs/v3/llms/smart-routing)

## 5. Configure OpenClaw interactively

Run the built-in wizard and select the provider you just added:

```bash
openclaw configure
```

Walk through:

- **model** → select `@edenai (Custom Provider)`
- **Gateway** → `https://api.edenai.run/v3/llm`
- **channels** → configure any channels your setup uses

## 6. Start OpenClaw

```bash
openclaw
```

That's it. Every LLM call now flows through Eden AI — with built-in fallbacks, unified billing, and per-request cost visibility.

---

## Using specific models

`@edenai` handles routing automatically, but you can target a specific model by replacing the `id` with a `provider/model` string:

```json
"id": "anthropic/claude-sonnet-4-5"
```

Common choices:

| Model | Best for |
|---|---|
| `@edenai` | **Default** — smart routing across all providers |
| `anthropic/claude-sonnet-4-5` | Balanced reasoning |
| `anthropic/claude-opus-4-7` | Maximum capability |
| `anthropic/claude-haiku-4-5` | Fast and cheap |
| `openai/gpt-5` | OpenAI's frontier model |
| `google/gemini-2.5-pro` | Long context, multimodal |

## Troubleshooting

### `401 Unauthorized`
Verify your Eden AI key — grab a fresh one at [app.edenai.run → API Keys](https://app.edenai.run/).

### `model not found`
Ensure the `id` uses the `provider/model` format (or `@edenai` for the smart router). No bare model names.

### Connection issues
Confirm the base URL is exactly `https://api.edenai.run/v3/llm` and check Eden AI status at [app-edenai.instatus.com](https://app-edenai.instatus.com/).

## Uninstall

```bash
npm uninstall -g openclaw
rm -rf ~/.openclaw
```

---

## Next steps

- [Smart routing](https://www.edenai.co/docs/v3/llms/smart-routing)
- [Fallbacks](https://www.edenai.co/docs/v3/llms/fallback)
- [Eden AI pricing](https://www.edenai.co/pricing)
- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
