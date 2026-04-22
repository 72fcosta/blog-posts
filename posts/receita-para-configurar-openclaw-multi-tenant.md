[2026-04-21]

# Receita para configurar OpenClaw (multi tenant)

### Ingredientes

- VPS com Ubuntu
- API Key OpenRouter
- Aliases
   ```bash
   alias cd..='cd ..'
   alias ls='ls -la'
   alias oc='openclaw'
   alias ogs='openclaw gateway status'
   alias ogr='openclaw gateway restart'
   alias ocs='openclaw config set'
   alias ocg='openclaw config get'
   ```

### Preparo do user root

- apt update
- apt upgrade -y
- apt install git
- apt install curl
- adduser openclaw

### Preparo do user 'openclaw'

- criar pasta .bash_aliases
- adicionar aliases na pasta .bash_aliases
- criar pasta .local
- instalar node
   - curl -fsSL https://nodejs.org/dist/v24.15.0/node-v24.15.0-linux-x64.tar.xz -o node.tar.xz
   - tar -xf node.tar.xz
   - mv node-v24.15.0-linux-x64 ~/.local/node
   - rm node.tar.xz

   ```bash
   export PATH="$HOME/.local/node/bin:$PATH"
   ```

- instalar https://tmuxai.dev na pasta .local

```bash
export PATH="$HOME/.local/tmuxai:$PATH"
```

### Preparo OpenClaw

- npm install -g openclaw@latest
- oc onboard --install-daemon
- oc update

- config (restaurar openclaw.json from local file)
- config main telegram

- env (.env)

```bash
  OPENCLAW_WEBHOOK_SECRET=xxx...
  TELEGRAM_BOT_TOKEN=xxx...
  OPENCLAW_GATEWAY_TOKEN=xxx...
  OPENCLAW_NO_RESPAWN=1
  NODE_COMPILE_CACHE=/.local/var/tmp/openclaw-compile-cache
```

- gateway
   - ogr
   - ogs

_Listening: 127.0.0.1:18789_

- instalar https://caddyserver.com/docs/install#debian-ubuntu-raspbian

- plugins flow
   -

- estrutura de pastas dos agentes
   - main
   - debug
   - tenants
      - tenant_id_01
      - tenant_id_02
