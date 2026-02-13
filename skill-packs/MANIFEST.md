# SKILL PACKS - CMTecnologia
# Sistema Inteligente de Carregamento On-Demand

---

## 🎯 FILOSOFIA

**Problema resolvido:**
- Antes: 60 skills carregadas sempre = 100k tokens = 15-200€ por conversa
- Agora: 0 skills por padrão, carrega só o que precisa = 0,05-2€

**Como funciona:**
1. Conversa normal: 0 skills (economia máxima)
2. Projeto específico: DANTE detecta necessidade
3. DANTE pede autorização (mostra custo)
4. Você aprova: skills carregadas
5. Trabalho executado com qualidade

---

## 📦 OS 3 PACKS

### **PACK 1: CORE_OPERATIONS**
**Descrição:** Skills essenciais para operação básica e administrativa
**Custo:** ~6k tokens = 0,70€
**Quando usar:** Tarefas administrativas, organização, manipulação de dados

**Skills incluidas (8):**
- `filesystem` - Criar/editar arquivos
- `antigravity-rotator` - Manter cérebro ativo
- `database-client` - PostgreSQL/Supabase
- `json-processor` - Processar JSON
- `csv-xlsx-handler` - Import/export Excel
- `scheduler` - Agendamento
- `webhook-engine` - Receber webhooks
- `logger` - Logs e debugging

**Exemplo de uso:**
> "Organiza a lista de leads em CSV e salva no banco"

---

### **PACK 2: WEB_BUILDER**
**Descrição:** Criação de sites (simples a 3D premium)
**Custo:** ~12k tokens = 1,50€
**Quando usar:** Qualquer projeto de site (institucional, 3D, landing page)

**Skills incluidas (6):**
- `filesystem` - Base de arquivos
- `antigravity-image-gen` - Gerar logos/assets premium
- `image-processing` - Otimizar imagens (WebP, compressão)
- `playwright` - Research de referências
- `seo-audit` - Validação SEO
- `pdf-generator` - Propostas comerciais

**Playbook:** `workspace/playbooks/WEBSITE_PREMIUM_3D.md`

**Exemplo de uso:**
> "Cria um site institucional para clínica médica"
> "Cria um menu 3D interativo para restaurante"

---

### **PACK 3: LEAD_MACHINE**
**Descrição:** Prospecção, scraping e vendas automatizadas
**Custo:** ~15k tokens = 1,80€
**Quando usar:** Buscar clientes, campanhas, prospecção ativa

**Skills incluidas (9):**
- `crawlee` - Scraping em massa
- `playwright` - Instagram/redes sociais
- `mailhunter` - Descobrir emails de decisões
- `email-verification` - Validar emails (anti-bounce)
- `email-smtp` - Enviar propostas
- `lead-discovery-wrapper` - Wrapper NERO
- `lead-scoring` - Qualificar leads (0-100)
- `n8n` - Workflows automação
- `rate-limiter` - Proteção anti-ban

**Exemplo de uso:**
> "Busca 50 clínicas em Lisboa sem site"
> "Prospecta restaurantes no Instagram com <1000 seguidores"

---

## 📊 COMPARAÇÃO DE CUSTOS

| Cenário | Antes (60 skills) | Agora (on-demand) | Economia |
|---------|-------------------|-------------------|----------|
| Conversa admin | 15€ | 0,05€ | **99,7%** |
| Site simples | 15-25€ | 1,55€ | **90-94%** |
| Site 3D premium | 100-200€ | 1,55€ | **99%** |
| Prospecção | 50-100€ | 1,85€ | **98%** |

---

## ⚠️ PROTOCOLO DE ATIVAÇÃO

### **Como DANTE deve pedir autorização:**

```
⚠️ SKILL PACK REQUERIDO

Tarefa: [descrição do que você pediu]
Pack necessário: [NOME_DO_PACK]
Skills que serão carregadas:
- [skill 1] (descrição do que faz)
- [skill 2] (descrição do que faz)
- ...

Custo adicional estimado: +X,XX€ nesta sessão

Alternativa SIMPLE (sem skills): [descrever o que consegue fazer sem carregar]

Autoriza carregar o pack? (Sim/Não)
```

### **Após autorização:**

```
✅ SKILL PACK [NOME] CARREGADO

Skills ativas: [lista resumida]
Custo sessão atual: ~X,XX€

Prosseguindo com execução...
```

---

## 📝 REGRAS IMPORTANTES

1. **NUNCA carregar skills sem avisar**
2. **SEMPRE mostrar custo antes**
3. **SEMPRE oferecer alternativa SIMPLE**
4. **Skills carregadas duram SÓ a sessão atual**
5. **Próxima conversa: volta a 0 skills**

---

## 🗑️ SKILLS ARQUIVADAS

As seguintes 45 skills foram arquivadas (não deletadas) por serem:
- Redundantes
- Raramente usadas
- Substituíveis por código

Lista completa em: `workspace/archive/old-skills/`

---

## 🚀 EVOLUÇÃO FUTURA

Quando a empresa crescer, podemos:
- Criar pack **SAAS_BUILDER** (para apps complexos)
- Criar pack **MARKETING_ADVANCED** (campanhas em massa)
- Adicionar skills específicas de nichos (advocacia, contabilidade)

**Mas por enquanto:** Estes 3 packs cobrem 100% das operações atuais.

---

**Versão:** 1.0  
**Data:** 13/02/2026  
**Status:** Ativo ✅