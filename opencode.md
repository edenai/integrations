# OpenCode + Eden AI

Connect [OpenCode](https://opencode.ai) to Eden AI and route your terminal agent through **500+ models** with smart routing, automatic fallbacks, and a single API key.

> Get your Eden AI key at [app.edenai.run](https://app.edenai.run/) → **API Keys**.

Follow this tuto in the same time with our video tuto on [Youtube](https://youtu.be/XXXXXXXXXXX)

---

## 1. System dependencies

On a fresh Linux machine (Ubuntu / Debian / WSL):

```bash
sudo apt update
sudo apt install -y curl git python3-venv
```

## 2. Install Node.js

OpenCode requires **Node.js 22.14+** and **npm 9.8+**.

```bash
sudo apt install -y nodejs npm

# Verify
node --version   # v22.14.x or newer
npm  --version   # 9.8.x or newer
```

If the packaged version is too old, install via [nvm](https://github.com/nvm-sh/nvm) or [nodesource](https://github.com/nodesource/distributions).

## 3. Install OpenCode

Pick one of the two methods below.

```bash
# Option A — official install script
curl -fsSL https://opencode.ai/install | bash

# Option B — via npm
npm install -g opencode-ai
```

Reload your shell so the `opencode` binary is on your PATH:

```bash
source ~/.bashrc
```

## 4. Add Eden AI as a custom provider

OpenCode stores its config at `~/.config/opencode/opencode.json`. Open it and add the Eden AI provider with the `@edenai` smart-router model:

```bash
nano ~/.config/opencode/opencode.json
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "edenai": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Eden AI",
      "options": {
        "baseURL": "https://api.edenai.run/v3",
        "apiKey": "YOUR_EDEN_AI_API_KEY"
      },
      "models": {
        "@edenai": {
          "name": "@edenai (Smart Router)"
        }
      }
    }
  }
}
```

### Why `@edenai`?

`@edenai` is Eden AI's **smart router**. For every request, it automatically picks the best-performing model based on quality, latency, cost and live provider health — so your OpenCode agent always uses the right model without a config change.

[How smart routing works →](https://www.edenai.co/docs/v3/llms/smart-routing)

## 5. Start OpenCode and pick the model

Launch the TUI:

```bash
opencode
```

Then select the Eden AI provider and model:

- Run `/models` and pick **`@edenai (Smart Router)`** under **Eden AI**.
- If you'd rather authenticate interactively instead of pasting the key into the config, run `/connect`, scroll to **Other**, enter `edenai` as the provider ID, and paste your Eden AI key when prompted.

That's it. Every LLM call now flows through Eden AI — with built-in fallbacks, unified billing, and per-request cost visibility.

---

## Using specific models

`@edenai` handles routing automatically, but you can target a specific model by adding it as an extra entry under `models`, keyed by `provider/model`:

```json
"models": {
  "@edenai": { "name": "@edenai (Smart Router)" },
  "anthropic/claude-sonnet-4-5": { "name": "Claude Sonnet 4.5" }
}
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
Ensure the model key uses the `provider/model` format (or `@edenai` for the smart router). No bare model names.

### Connection issues
Confirm the base URL is exactly `https://api.edenai.run/v3` and check Eden AI status at [app-edenai.instatus.com](https://app-edenai.instatus.com/).

## Uninstall

```bash
npm uninstall -g opencode-ai
rm -rf ~/.config/opencode
```

---

## Next steps

- [Smart routing](https://www.edenai.co/docs/v3/llms/smart-routing)
- [Fallbacks](https://www.edenai.co/docs/v3/llms/fallback)
- [Eden AI pricing](https://www.edenai.co/pricing)
- [OpenCode GitHub](https://github.com/sst/opencode)
