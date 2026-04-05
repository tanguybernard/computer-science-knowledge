

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
