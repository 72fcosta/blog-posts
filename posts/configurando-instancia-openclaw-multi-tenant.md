[2026-04-19]

# OpenClaw multi-tenant

## Configurando uma instância do OpenClaw multi-tenant

### Objetivo

- Atendimento via WhatsApp ao customer do consumer
   - Customer envia uma mensagem ao consumer
      - O core do OpenClaw deve ser capaz de bloquear a mensagem antes do agente
      - O core do OpenClaw deve ser capaz de responder a mensagem antes do agente
      - O core do OpenClaw deve ser capaz de bloquear o acesso do agente às slashes (/new, /status, etc)
      - O core do OpenClaw deve ser capaz de permitir o desenvolvimento de uma tool/plugin get-customer
      - O core do OpenClaw deve ser capaz de invocar uma tool/plugin get-customer no hook on mounted session
      - O core do OpenClaw deve ser capaz de injetar com prompt inicial da sessão, o current customer ou uma informação de primeiro contato

### Required

- Como funciona o gateway do OpenClaw?

### Steps
