# MEMORY.md - Memória de Longo Prazo

## Estratégia de IA e Modelos
- **Modelo Dante:** Prioridade `google/gemini-3-flash-preview`. 
- **Hierarquia de Fallback:** Gemini 3 Pro > Gemini 2.5 Flash > Sonnet 4.5. 
- **Protocolo de Emergência:** NUNCA alternar para um modelo de fallback ou nova chave API sem antes realizar um "ping" de validação (teste de token/conectividade). Só alternar se o status for 200/OK.
- **Regra:** Sempre notificar o humano quando houver troca de modelo (fallback).
- **Consumo:** Monitorizar TPM/RPM no Google AI Studio (projeto gen-lang-client-0616971507).
- **Custo:** Anthropic/Claude é caro. Priorizar automações via n8n para economizar.

## CMTecnologia - Planejamento Estratégico 10/02/2026
- **Dante:** Foco em Arquitetura de Sistemas, Deep Coder e Treinamento de IA.
- **Nero:** Transição para n8n completa. Lead Generator PRO ativo.
- **Lead Generator:** Sistema automatizado de prospecção (Brave Search → Qualificação → Email).
- **Infra:** VPS Hostinger (72.62.179.56), n8n via Docker (Easypanel), Evolution API ativa.
- **Segurança:** Tokens GitHub removidos da memória. Deploy manual apenas.

## Incidente 10/02/2026 - Site cmtecnologia.pt
- **Erro Crítico:** Sobrescrevi o repositório `website-mark` por engano, destruindo o histórico.
- **Recuperação:** Site restaurado via Vercel Deployment History.
- **Lição Aprendida:** NUNCA fazer push direto para `main` sem verificar o histórico completo.
- **Protocolo de Segurança Anti-Pico:** Antes de cada turno, resumo logs extensos para manter o contexto abaixo de 800k tokens e evitar estourar o Rate Limit de 1M/min.
- **Protocolo Novo:** Sempre clonar repositório completo antes de modificar. Verificar `git log` extenso.

## Lead Generator PRO (Criado 10/02/2026)
- **Workflow n8n:** `n8n_lead_generator_professional.json`
- **Schema SQL:** `schema_leads_cmtecnologia.sql`
- **Documentação:** `SETUP_LEAD_GENERATOR.md`
- **Funcionalidades:**
  - Busca automática de empresas com sites ruins (Brave Search API)
  - Verificação e scoring (0-100)
  - Qualificação (≥40 pontos = lead qualificado)
  - Armazenamento PostgreSQL (Supabase)
  - Email automatizado personalizado
- **Nichos:** Restaurantes, Clínicas, Advogados, Ginásios, Salões (Portugal)
- **Frequência:** 4x por dia (a cada 6h)
- **Custo:** €0 (dentro dos limites gratuitos)

## Configurações de Servidor
- VPS Hostinger (72.62.179.56)
- n8n via Docker (Easypanel) - http://72.62.179.56:5678
- Evolution API ativa para WhatsApp
- Supabase PostgreSQL (banco de dados de leads)

## Consolidação e Segurança - 15/02/2026
- **Conta Madalena Rocha:** Configurada via Project ID `project-1ab25cf8-2ccf-407e-b53`. Saldo de €251 ativos. Usar perfil `google:manual` para acesso direto via Vertex AI.
- **Dívida IA Studio:** Detectada fatura de €62.00 pendente no Google IA Studio (Conta antiga).
- **Proibição Crítica:** Dante/Nero/Lúcio estão PROIBIDOS de editar o `openclaw.json` sem ordem direta do Mateus.
- **Balanço Geral:** Burn rate acumulado de ~$238.00. Histórico salvo em `financials/BALANCO_HISTORICO_V1.md`.
- **Campanha Porto:** Pasta criada na VPS (`/root/squad/porto`). Nero aguarda sinal para busca de leads.
