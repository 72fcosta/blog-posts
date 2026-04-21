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
- instalar node com nvm (ex: nvm install 24)
- instalar https://tmuxai.dev na pasta .local
   ```bash
   export PATH=$PATH:"$HOME/.local/tmuxai"
   ```

### Preparo OpenClaw

- npm install -g openclaw@latest
- openclaw onboard --install-daemon
- oc update
- oc gateway
- ocs gateway.controlUi.allowInsecureAuth false
- ocs gateway.controlUi.allowedOrigins '["https://openclaw.XXX"]' --strict-json
- ocs gateway.trustedProxies '["127.0.0.1"]' --strict-json
- ocs hooks '{"token":"${OPENCLAW_HOOKS_TOKEN}"}' --strict-json

- Caddy

#cookbook
