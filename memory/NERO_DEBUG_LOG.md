# DOSSIÊ TÉCNICO: NERO (OPENCLAW ON VPS) - STATUS: FALHA/PAUSADO
**Data:** 07/02/2026
**Objetivo:** Rodar instância OpenClaw ("Nero") no EasyPanel (VPS Hostinger).

## O Problema
O container sobe e fica "Verde/Running", mas:
1. **Não responde externamente:** Erro 502 Bad Gateway no EasyPanel.
2. **Não conecta Telegram:** Webhook falha ou não inicia.
3. **Isolamento de Rede:** Logs mostram persistentemente `listening on ws://127.0.0.1:18789`.
   - O processo está preso em *localhost* (loopback) dentro do container.
   - O Traefik (EasyPanel) e o Docker Swarm não conseguem rotear tráfego para ele se ele não ouvir em `0.0.0.0`.

## Tentativas Realizadas (Falhas)
1. **Variáveis de Ambiente (ENV):**
   - Tentamos injetar `HOST=0.0.0.0`, `OPENCLAW_HOST=0.0.0.0`, `OPENCLAW_BIND=0.0.0.0`, `OPENCLAW_GATEWAY_BIND=0.0.0.0`, `PORT=3000`.
   - **Resultado:** Ignoradas pelo container. Continuou na porta 18789 e IP 127.0.0.1.

2. **Argumentos de Comando (CLI):**
   - Tentativa de sobrescrever o comando Docker com `gateway start --host 0.0.0.0`.
   - **Resultado:** Crash do container (`Error: Cannot find module`). O entrypoint da imagem `latest` não aceitou os args ou a sintaxe.

3. **Injeção de Configuração (JSON):**
   - Criamos `/root/nero-config.json` na VPS e montamos em `/home/node/.openclaw/config.json`.
   - Conteúdo forçava `"bind": "custom"`.
   - **Resultado:** Inicialmente erro de permissão (`EACCES`), corrigido com `chown`. Depois de corrigir, o container subiu mas **continuou ignorando o bind**, mantendo-se em 127.0.0.1.

4. **Publicação Direta de Porta:**
   - Usamos `docker service update --publish-add 18789:18789`.
   - Liberamos Firewall UFW.
   - **Resultado:** Porta abriu no TCP, mas conexão recusada ao tentar acessar via IP, provando que a aplicação recusa conexões externas (não-localhost).

5. **Modo Desenvolvimento:**
   - Injetamos `NODE_ENV=development`.
   - **Resultado:** Sem mudança no comportamento de rede.

## Hipótese Técnica para Retomada Futura
A imagem Docker `ghcr.io/openclaw/openclaw:latest` atual parece ter o *host* hardcoded para `127.0.0.1` por segurança ou bug no script de entrada, ignorando variáveis padrão de bind.

**Soluções sugeridas para o futuro:**
1. **Network Host:** Rodar o container com `--network host` (compartilha IP da VPS). EasyPanel dificulta isso, melhor via Portainer ou Docker Compose manual.
2. **Reverse Proxy Sidecar:** Instalar um Nginx dentro do container ou ao lado (pod) para fazer ponte `0.0.0.0:80` -> `127.0.0.1:18789`.
3. **Build Customizado:** Criar nosso próprio Dockerfile que força o bind no código.

---
**ESTADO ATUAL:** Container rodando, porta 18789 exposta, token mestre configurado (`MATEUS-TOKEN-SECRETO-123`), mas inacessível.
