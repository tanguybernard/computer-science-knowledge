
Tu cherchais un agent de coding comparable à Claude Code, gratuit et qui fonctionne à la fois sur VS Code (React/TS) et IntelliJ (Kotlin).
Le cheminement :

- LLM local → trop lourd pour ton M1 Max 32Go, tool calling qui ne marche pas vraiment
- OpenCode + MiniMax M2.5 gratuit → bon mais limité sur l'agentique local
- Cline + OpenCode Zen → agent qui appelle vraiment les outils, même config sur les deux IDEs, gratuit pour l'instant



## Cline


Pour OpenCode Zen (MiniMax M2.5 gratuit) :

Va sur opencode.ai/auth
Connecte-toi avec GitHub
La clé API est générée automatiquement

Ensuite dans Cline, tu configures :

Provider : OpenAI Compatible
Base URL : https://opencode.ai/zen/v1
API Key : ta clé OpenCode Zen
Model : minimax-m2.5-free

C'est tout ! Tu as déjà un compte GitHub ?



## openCode


vi ~/.config/opencode/opencode.json

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama (local)",
      "options": {
        "baseURL": "http://localhost:11434/v1"
      },
      "models": {
        "deepseek-coder-v2": {
          "name": "DeepSeek Coder V2"
        }
      }
    }
  }
}
```


Lancer opencode

Choisir un models

/models

> DeepSeek Coder V2 Ollama (local)


## Aider

    export OLLAMA_API_BASE=http://localhost:11434
    aider --model ollama/deepseek-coder-v2 
