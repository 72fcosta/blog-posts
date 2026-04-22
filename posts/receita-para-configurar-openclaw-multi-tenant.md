[2026-04-21]

# Receita para configurar OpenClaw (multi tenant)

### Objetivo

- Interações via Welcome page
   - Programaticamente é gerado um novo place
   - Dekbot Server envia para uma rota (POST https://openclaw.XXX/setup/api/agent)
      - É gerado um workspace e um agente

- Interações via Schedly Dash ao consumer
   - Consumer desliga o agente
      - Dekbot Server envia o request ao OpenClaw por uma rota (POST https://openclaw.XXX/setup/api/disable-agent)
         - O core do OpenClaw deve ser capaz de bloquear todas as mensagens seguintes
   - Consumer cria um customer contact
      - Dekbot Server envia o objeto ao OpenClaw por uma rota (POST https://openclaw.XXX/setup/api/customer)
         - É assigned ao objeto ao file tenants.json que vive fora dos workspaces dos agentes

- Atendimento via WhatsApp ao customer do consumer
   - Customer envia uma mensagem ao consumer
      - O core do OpenClaw deve ser capaz de bloquear a mensagem antes do agente
      - O core do OpenClaw deve ser capaz de responder a mensagem antes do agente
      - O core do OpenClaw deve ser capaz de bloquear o acesso do agente às slashes (/new, /status, etc)
      - O core do OpenClaw deve ser capaz de permitir o desenvolvimento de uma tool/plugin get-customer
      - O core do OpenClaw deve ser capaz de invocar uma tool/plugin get-customer no hook on mounted session
      - O core do OpenClaw deve ser capaz de injetar com prompt inicial da sessão, o current customer ou uma informação de primeiro contato

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

- git backup (1 vez push changes commit de .openclaw/agents)

- bloquear slash cmds from tenant

- sandbox?
