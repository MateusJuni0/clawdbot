\# SKILL: Campaign Orchestrator



\## Role

Orquestrar campanhas outbound coordenando discovery, qualificação, envio e avaliação.



\## Responsibility

\- Definir a ordem de execução dos wrappers

\- Controlar o estado da campanha

\- Decidir quando pausar, continuar ou escalar

\- Consolidar resultados para o Jarvis



\## Inputs

\- campaign\_id (string)

\- target\_profile (object)

\- sources (array)

\- qualification\_rules (object)

\- email\_template (string)

\- limits (object)



\## Outputs

\- campaign\_status

\- stage\_results (object)

\- next\_action

\- execution\_summary



\## Allowed Tools

\- lead-discovery-wrapper

\- outbound-email-wrapper

\- rule-engine

\- state-machine

\- scheduler

\- logger



\## Forbidden Actions

\- Criar copy de vendas

\- Enviar emails diretamente

\- Executar scraping direto

\- Alterar estratégia sem escalar



\## Campaign Stages

1\. Lead Discovery

2\. Lead Qualification

3\. Outbound Execution

4\. Response Monitoring

5\. Evaluation \& Decision



\## Error Handling

\- Falha em qualquer estágio → pausar campanha

\- Resultados abaixo do limite → escalar

\- Erros repetidos → abortar



\## Escalation

Escalar para Jarvis quando:

\- Conversão abaixo do mínimo esperado

\- Erros técnicos recorrentes

\- Dados inconsistentes entre estágios



\## Notes

Este wrapper é o gerente da operação.

Ele coordena, não executa.



