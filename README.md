# Description
PoC | Use liteLLM UI to access remote ollama from Claude Code

## Steps

- **STEP01**: Deploy/Remove LiteLLM Proxy Server. \
Deploy LiteLLM Proxy Server using Docker.
```shell
$ docker compose up -d
```

Remove LiteLLM stack and volumes
```shell
$ docker compose down -v
```

We can access to swagger API:
http://localhost:4000

!["LiteLLM Swagger"](./images/litellm_swagger_api.png "LiteLLM Swagger")

We can open the UI using default credentials: admin/sk-1234
http://localhost:4000/ui

- **STEP02**: Create a API_KEY. \
Create an API_KEY to be used by Claude Code from liteLLM UI

![LiteLLM API KEY](./images/litellm_api_key.png "LiteLLM API KEY")

- **STEP03**: Add LLM Model. \
Add model `qwen3:8b` from Ollama Chat provider from liteLLM UI

![LiteLLM model](./images/litellm_model.png "LiteLLM model")

- **STEP4**: Install Claude Code. \
Install Claude Code in your system
```shell
$ curl -fsSL https://claude.ai/install.sh | bash
```

- **STEP5**: Configure Claude Code. \
Configure Claude Code from your code base to connect to liteLLM Proxy server

```
{
  "env": {
    "ANTHROPIC_BASE_URL": "http://localhost:4000",
    "ANTHROPIC_AUTH_TOKEN": "sk-GtxpICZURffJf6QOtqbXJQ",
    "ANTHROPIC_MODEL": "qwen3-8b"
  }
}
```