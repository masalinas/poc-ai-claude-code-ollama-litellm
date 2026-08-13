# Description
Configure Claude Code to use ollama models throw LiteLLM AI Gateway from UI.

## Steps

- **STEP01**: Deploy/Remove LiteLLM Proxy Server. \
To deploy LiteLLM Proxy Server using Docker.
```shell
$ docker compose up -d
```

![LiteLLM Stack](./images/litellm_stack.png "LiteLLM Stack")

**NOTE**: if you deploy LiteLLM in linux, the node: host.docker.internal is no available, you must registered when start the LiteLLM compose file adding this argument under litellm service like this:

```
services:
  litellm:
    ...
    extra_hosts:
      - "host.docker.internal:host-gateway"
```

Also you must edit ollama configuration add add this configuration

```shell
$ sudo systemctl edit ollama.service
```

Add this env variables: OLLAMA_HOST like this:
```
### Editing /etc/systemd/system/ollama.service.d/override.conf
### Anything between here and the comment below will become the contents of the drop-in file

[Service]
Environment="OLLAMA_HOST=0.0.0.0"

### Edits below this comment will be discarded

### /etc/systemd/system/ollama.service
# [Unit]
# Description=Ollama Service
# After=network-online.target
# 
# [Service]
# ExecStart=/usr/local/bin/ollama serve
# User=ollama
# Group=ollama
# Restart=always
# RestartSec=3
# Environment="PATH=/home/simur/.sdkman/candidates/java/current/bin:/home/simur/.nvm/versions/node/v24.14.1/bin:/home/simur/.local/bin:/usr/lib/nvidia-cuda-toolkit/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin:/home/simur/.lmstudio/bin:/home/simur/.lmstudio/bin"
# 
# [Install]
# WantedBy=default.target
```

And finally restart ollama service:
```shell
$ sudo systemctl restart ollama
```

If you need remove LiteLLM stack and volumes
```shell
$ docker compose down -v
```

After deployed, we can open the UI using default credentials: **admin/sk-1234** at http://localhost:4000/ui

![LiteLLM UI](./images/litellm_login.png "LiteLLM UI")

If we want develop using any SDK we have the LiteLLM Swagger API documentation at http://localhost:4000

!["LiteLLM Swagger"](./images/litellm_swagger_api.png "LiteLLM Swagger")

- **STEP02**: Create an API_KEY. \
Create an API_KEY to be used by Claude Code from LiteLLM UI

![LiteLLM API KEY](./images/litellm_api_key.png "LiteLLM API KEY")

- **STEP03**: Add LLM Models. \
Add model `qwen3:8b` using the Ollama Chat provider from Models + Endpoints from LiteLLM UI:

![LiteLLM model](./images/litellm_model.png "LiteLLM model")

If you installed ollama natively in your host, you must use this uri to configure your model API Base: `http://host.docker.internal:11434`. If you have some problems when test this uri, use your host IP (Be carefull if this one is dynamic).

- **STEP4**: Install Claude Code TUI. \
Install Claude Code TUI in your host as usual:
```shell
$ curl -fsSL https://claude.ai/install.sh | bash
```

- **STEP5**: Configure Claude Code. \
Create Claude Code code base configuration file. First create your code base directory when your project code will be and inside, configure Claude Code configuration file called settings.json, to connect to LiteLLM Proxy server and use its LLM published models.
```
{
  "env": {
    "ANTHROPIC_BASE_URL": "http://<LITELLM_HOST>:4000",
    "ANTHROPIC_AUTH_TOKEN": "<LITELLM_API_KEY>",
    "ANTHROPIC_MODEL": "<LITE_LLM_MODEL_ID>"
  }
}
```