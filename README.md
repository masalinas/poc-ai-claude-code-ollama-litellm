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

- **STEP02**: Create a API_KEY. \
Create an API_KEY to be used by Claude Code from liteLLM UI

- **STEP03**: Add LLM Model. \
Add model `qwen3:8b` from Ollama Chat provider from liteLLM UI

- **STEP4**: Install Claude Code. \
Install Claude Code in your system

- **STEP5**: Configure Claude Code. \
Configure Claude Code from your code base to connect to liteLLM Proxy server