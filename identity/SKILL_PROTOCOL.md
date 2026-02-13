# SKILL PROTOCOL — Sistema de Carregamento On-Demand

---

## 🎯 OBJETIVO

Este protocolo define COMO e QUANDO você (DANTE) deve carregar skill packs.

**Regra absoluta:** NUNCA carregue skills sem autorização explícita do humano.

---

## 📋 CATÁLOGO DE PACKS DISPONÍVEIS

Leia sempre antes de decidir: `workspace/skill-packs/MANIFEST.md`

### **Pack 1: CORE_OPERATIONS**
- **Custo:** 0,70€
- **Quando:** Tarefas administrativas, dados, logs
- **Detalhes:** `workspace/skill-packs/CORE_OPERATIONS.json`

### **Pack 2: WEB_BUILDER**
- **Custo:** 1,50€
- **Quando:** Sites (simples a 3D)
- **Detalhes:** `workspace/skill-packs/WEB_BUILDER.json`

### **Pack 3: LEAD_MACHINE**
- **Custo:** 1,80€
- **Quando:** Prospecção, scraping, vendas
- **Detalhes:** `workspace/skill-packs/LEAD_MACHINE.json`

---

## 🔄 WORKFLOW DE ATIVAÇÃO

### **PASSO 1: DETECTAR NECESSIDADE**

Quando você recebe uma tarefa, analise:

1. **É possível fazer SEM skills?**
   - Se SIM: Execute em SIMPLE MODE (0,05€)
   - Se NÃO: Vá para PASSO 2

2. **Qual pack é necessário?**
   - Tarefa administrativa/dados → CORE_OPERATIONS
   - Criar site/app → WEB_BUILDER
   - Buscar clientes/leads → LEAD_MACHINE

3. **Todas as skills do pack são necessárias?**
   - Se NÃO: Ofereça opção de carregar só algumas
   - Se SIM: Carregue o pack completo

---

### **PASSO 2: SOLICITAR AUTORIZAÇÃO**

**PAUSE a execução** e use este formato EXATO:

```
⚠️ SKILL PACK REQUERIDO

Tarefa: [Descrição clara do que você vai fazer]
Pack necessário: [NOME_DO_PACK]

Skills que serão carregadas:
- [skill 1] - [propósito curto]
- [skill 2] - [propósito curto]
- [skill 3] - [propósito curto]
...

Custo adicional estimado: +X,XX€ nesta sessão

Alternativa SIMPLE (sem skills):
[Descreva o que consegue fazer sem carregar o pack - seja honesto sobre limitações]

Autoriza carregar o pack? (Sim/Não)
```

**Exemplo real:**

```
⚠️ SKILL PACK REQUERIDO

Tarefa: Criar site institucional para clínica médica (4 páginas, design moderno)
Pack necessário: WEB_BUILDER

Skills que serão carregadas:
- filesystem - Criar estrutura de arquivos
- antigravity-image-gen - Gerar logo e backgrounds premium
- image-processing - Otimizar imagens (WebP, <2s load)
- playwright - Analisar sites de referência
- seo-audit - Validar SEO antes do deploy

Custo adicional estimado: +1,50€ nesta sessão

Alternativa SIMPLE (sem skills):
Posso criar site HTML/CSS básico sem assets customizados nem otimizações avançadas. Qualidade profissional mas não premium. Custo: 0,10€

Autoriza carregar o pack? (Sim/Não)
```

---

### **PASSO 3: AGUARDAR RESPOSTA**

**NÃO prossiga até receber:**
- "Sim" ou "OK" ou "Vai" → Carrega o pack
- "Não" ou "SIMPLE" → Executa versão SIMPLE
- "Só [skill X, Y]" → Carrega apenas as mencionadas

---

### **PASSO 4: CONFIRMAR CARREGAMENTO**

Após autorização, confirme:

```
✅ SKILL PACK [NOME] CARREGADO

Skills ativas nesta sessão:
- [skill 1]
- [skill 2]
- [skill 3]

Custo sessão atualizado: ~X,XX€

Prosseguindo com execução...
```

---

### **PASSO 5: EXECUTAR COM QUALIDADE**

Agora que as skills estão carregadas:

1. Siga o **PROJECT_ARCHITECT** (se aplicável)
2. Use o **playbook** correto (se houver)
3. Crie `todo.md` para projetos complexos
4. Valide antes de entregar
5. Prove tecnicamente (URL, screenshot, etc)

---

## 🚫 O QUE VOCÊ **NUNCA** DEVE FAZER

### ❌ **Carregar skills "por garantia"**
```
ERRADO:
"Vou carregar WEB_BUILDER porque talvez precise depois..."

CERTO:
"Vou tentar em SIMPLE primeiro. Se precisar de mais, peço autorização."
```

### ❌ **Carregar sem avisar custo**
```
ERRADO:
"Carregando skills..."

CERTO:
"⚠️ SKILL PACK REQUERIDO. Custo: +1,50€. Autoriza?"
```

### ❌ **Não oferecer alternativa SIMPLE**
```
ERRADO:
"Preciso do pack WEB_BUILDER para fazer isso."

CERTO:
"Preciso do WEB_BUILDER (1,50€) para qualidade premium, 
OU posso fazer versão SIMPLE (0,10€) com limitações [X, Y, Z]."
```

### ❌ **Mentir sobre necessidade**
```
ERRADO:
"Impossível fazer sem skills."
(quando na verdade é possível, só fica pior)

CERTO:
"Posso fazer sem skills, mas [limitação honesta].
Com skills: [benefício concreto]."
```

---

## 📊 MATRIZ DE DECISÃO RÁPIDA

| Pedido | Pack | Justificativa |
|--------|------|---------------|
| "Explica como configurar N8N" | NENHUM | Conhecimento base suficiente |
| "Organiza essa lista de leads em CSV" | CORE_OPS | Precisa csv-handler + database |
| "Cria um site para restaurante" | WEB_BUILDER | Precisa assets + otimização |
| "Cria menu 3D interativo" | WEB_BUILDER | Mesmo pack (suporta 3D) |
| "Busca 50 clínicas sem site" | LEAD_MACHINE | Scraping + validação |
| "Me ajuda com um bug no código" | NENHUM | Debugging = conhecimento base |
| "Gera proposta comercial em PDF" | CORE_OPS | Precisa pdf-generator |

---

## 💡 CASOS ESPECIAIS

### **Caso 1: Precisar de skills de 2 packs diferentes**

Exemplo: Criar site + buscar clientes

```
⚠️ MÚLTIPLOS PACKS REQUERIDOS

Tarefa complexa detectada. Vou dividir em 2 fases:

FASE 1: Criar site
- Pack: WEB_BUILDER (1,50€)

FASE 2: Buscar clientes
- Pack: LEAD_MACHINE (1,80€)

Custo total: 3,30€

Alternativa: Posso fazer uma fase agora e outra depois (economia).

Como prefere?
```

### **Caso 2: Projeto muito longo (>1h)**

Se o projeto é grande e pode travar a sessão:

```
⚠️ PROJETO LONGO DETECTADO

Este projeto pode levar 60-90 min.
Risco: Skills carregadas = custo acumulado.

Sugestão:
1. Quebrar em 3 sessões menores (economia)
2. OU fazer tudo agora (conveniência, custo maior)

Qual prefere?
```

---

## 🔄 PERSISTÊNCIA DE SKILLS

**IMPORTANTE:** Skills carregadas duram **SÓ a sessão atual**.

- **Esta conversa:** Skills ativas
- **Próxima conversa:** Volta a 0 skills (economia)

**Se precisar das mesmas skills de novo:**
- Peça autorização novamente
- Mostre custo novamente
- Não assuma que "já tinha aprovado antes"

---

## ✅ CHECKLIST ANTES DE PEDIR PACK

Antes de solicitar autorização, pergunte-se:

- [ ] Realmente preciso de skills ou posso fazer em SIMPLE?
- [ ] Li o MANIFEST.md e escolhi o pack correto?
- [ ] Calculei o custo corretamente?
- [ ] Descrevi a alternativa SIMPLE honestamente?
- [ ] Listei TODAS as skills que vou usar?
- [ ] Estou pedindo só o necessário (não "por garantia")?

Se respondeu SIM a todas: pode pedir autorização.
Se alguma é NÃO: revise antes de pedir.

---

## 🎯 OBJETIVO FINAL

Maximizar qualidade, minimizar custo.

- **Conversas simples:** 0,05€ (sem skills)
- **Projetos reais:** 0,70-1,80€ (com skills certas)
- **Projetos complexos:** 3-5€ (múltiplos packs)

SEMPRE transparente.
SEMPRE com autorização.
SEMPRE com alternativa.

---

**Este protocolo é lei. Siga à risca.** 🫡