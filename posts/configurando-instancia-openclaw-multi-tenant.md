[2026-04-19]

# OpenClaw multi-tenant

## Configurando uma instância do OpenClaw multi-tenant

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

### Required

- A porta 18789?
- Como configurar ControlUI use?
- Como funciona o gateway?

openclaw models auth login --provider openai

### Steps

- su - openclaw <!-- use openclaw user -->
- curl -fsSL https://openclaw.ai/install.sh | bash
- openclaw gateway
- Definir configs em ~/.openclaw/openclaw.json
- OpenClaw responde pelo ControlUI

### Bash Aliases

- openclaw: oc
- openclaw gateway status: ogs
- openclaw gateway restart: ogr
- openclaw config set: ocs
