# Description
PoC | Use LiteLLM UI to configure your models. In our case ollama LLM models to be used by Claude Code

## Steps

- **STEP01**: Deploy/Remove LiteLLM Proxy Server. \
To deploy LiteLLM Proxy Server using Docker.
```shell
$ docker compose up -d
```

![LiteLLM Stack](./images/litellm_stack.png "LiteLLM Stack")

To remove LiteLLM stack and volumes
```shell
$ docker compose down -v
```

After deployed, we can open the UI using default credentials: admin/sk-1234
http://localhost:4000/ui

![LiteLLM UI](./images/litellm_login.png "LiteLLM UI")

From any SDK we have the LiteLLM Swagger API documentation:
http://localhost:4000

!["LiteLLM Swagger"](./images/litellm_swagger_api.png "LiteLLM Swagger")

- **STEP02**: Create an API_KEY. \
Create an API_KEY to be used by Claude Code from LiteLLM UI

![LiteLLM API KEY](./images/litellm_api_key.png "LiteLLM API KEY")

- **STEP03**: Add LLM Model. \
Add model `qwen3:8b` from Ollama Chat provider from liteLLM UI

![LiteLLM model](./images/litellm_model.png "LiteLLM model")

If you have ollama native installed in your host. You must use this uri to configure your ollama model: `http://host.docker.internal:11434`. If you ahve some problems you can use your host IP.

- **STEP4**: Install Claude Code TUI. \
Install Claude Code TUI in your host:
```shell
$ curl -fsSL https://claude.ai/install.sh | bash
```

- **STEP5**: Configure Claude Code. \
Create a code base directory when code your project and inside it, configure Claude Code to connect to LiteLLM Proxy server and use its LLM published models.
```
{
  "env": {
    "ANTHROPIC_BASE_URL": "http://<LITELLM_HOST>:4000",
    "ANTHROPIC_AUTH_TOKEN": "<LITELLM_API_KEY>",
    "ANTHROPIC_MODEL": "<LITE_LLM_MODEL_ID>"
  }
}
```