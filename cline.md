# Cline + Eden AI

Connect [Cline](https://cline.bot) to Eden AI and route your VS Code agent through **500+ models** with smart routing, automatic fallbacks, and a single API key.

> Get your Eden AI key at [app.edenai.run](https://app.edenai.run/) → **API Keys**.

Follow this tuto in the same time with our video tuto on [Youtube](https://youtu.be/_M8PwHSwgMQ)

---

## 1. Install VS Code

Cline runs as a VS Code extension. Grab the latest version from [code.visualstudio.com](https://code.visualstudio.com/) and install it for your OS.

## 2. Install the Cline extension

Open VS Code, go to the **Extensions** panel (`Ctrl+Shift+X` / `Cmd+Shift+X`), search for **Cline**, and click **Install**.

You can also install it straight from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=saoudrizwan.claude-dev).

Once installed, open the Cline sidebar from the activity bar on the left.

## 3. Open Cline settings

In the Cline panel, click the **⚙️ settings icon** at the top to open the configuration screen.

## 4. Add Eden AI as an OpenAI Compatible provider

Cline ships with a built-in **OpenAI Compatible** provider — no plugin fork or extra install required.

In the settings panel:

- **API Provider** → select `OpenAI Compatible`
- **Base URL** → `https://api.edenai.run/v3/llm`
- **API Key** → paste your Eden AI key from [app.edenai.run](https://app.edenai.run/)
- **Model ID** → `@edenai`

Save the settings. Cline will now route every request through Eden AI.

### Why `@edenai`?

`@edenai` is Eden AI's **smart router**. For every request, it automatically picks the best-performing model based on quality, latency, cost and live provider health — so your Cline agent always uses the right model without a config change.

[How smart routing works →](https://www.edenai.co/docs/v3/llms/smart-routing)

## 5. Start coding with Cline

Open any project in VS Code, launch the Cline sidebar, and start a new task. Every LLM call now flows through Eden AI — with built-in fallbacks, unified billing, and per-request cost visibility.

---

## Using specific models

`@edenai` handles routing automatically, but you can target a specific model by replacing the **Model ID** field with a `provider/model` string:

```
anthropic/claude-sonnet-4-5
```

Common choices:

| Model | Best for |
|---|---|
| `@edenai` | **Default** — smart routing across all providers |
| `anthropic/claude-sonnet-4-5` | Balanced reasoning |
| `openai/gpt-5` | OpenAI's frontier model |

Browse the full catalog at [app.edenai.run/models](https://app.edenai.run/models).

## Troubleshooting

### `401 Unauthorized`
Verify your Eden AI key — grab a fresh one at [app.edenai.run → API Keys](https://app.edenai.run/).

### `model not found`
Ensure the **Model ID** uses the `provider/model` format (or `@edenai` for the smart router). No bare model names.

### Base URL field missing
Make sure Cline is updated to the latest version and that **OpenAI Compatible** is selected as the API Provider — the Base URL field only appears for that option.

### Connection issues
Confirm the base URL is exactly `https://api.edenai.run/v3/llm` and check Eden AI status at [app-edenai.instatus.com](https://app-edenai.instatus.com/).

## Uninstall

Remove the Cline extension from the VS Code **Extensions** panel (right-click → **Uninstall**).

---

## Next steps

- [Smart routing](https://www.edenai.co/docs/v3/llms/smart-routing)
- [Fallbacks](https://www.edenai.co/docs/v3/llms/fallback)
- [Eden AI pricing](https://www.edenai.co/pricing)
- [Cline GitHub](https://github.com/cline/cline)
