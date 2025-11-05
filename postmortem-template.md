# 🧠 Post-Mortem: [Título do Incidente]
> **Objetivo:** Documentar e analisar um incidente de forma construtiva, sem atribuição de culpa, identificando causas, impactos e aprendizados.

---

## 📅 Resumo do Incidente
| Campo | Descrição |
|--------|------------|
| ID | INC-XXXX |
| Data/Hora | [Data e hora do início e término] |
| Duração | [Tempo total de impacto] |
| Severidade | [P1, P2, P3...] |
| Serviços Afetados | [Lista de serviços] |
| Impacto | [Breve descrição do impacto no negócio ou usuário] |

---

## 🔍 Detecção
Descreva como o incidente foi identificado:
- Qual alerta disparou?  
- Qual métrica ou evento foi o gatilho?  
- Quanto tempo levou para detectar o problema (MTTD)?

**Exemplo:**
> Alerta "Erro 5xx > 5%" no serviço `checkout-service` detectado via Prometheus.  
> Tempo de detecção: 3 minutos após início da falha.

---

## 🧪 Diagnóstico
Liste os principais sinais e descobertas que levaram à causa raiz:
- Logs, métricas, traces relevantes.  
- Passos realizados durante a investigação.  
- Ferramentas usadas para diagnóstico.

**Exemplo:**
> Logs indicaram `SQLTimeoutException`. Métricas de pool de conexão saturadas.  
> Investigação mostrou aumento de tráfego + limitação de conexões.

---

## 🛠️ Correção
Descreva o que foi feito para restaurar o serviço:
1. Ações tomadas (manual ou automática).  
2. Sequência das ações.  
3. Validação pós-correção (como foi confirmada a normalização).

**Exemplo:**
> Reiniciado deployment `checkout-service` e ajustado `maximum-pool-size` para 30.  
> Healthcheck OK e latência < 300ms após correção.

---

## 💡 Causa Raiz
Explique a origem do problema e os fatores que contribuíram:
- Falha técnica, processo, arquitetura, ou humana.  
- Decisões que agravaram ou atrasaram a resposta.  

**Exemplo:**
> Falha no dimensionamento do pool de conexões do banco de dados.  
> Alerta inexistente para uso de conexões acima de 90%.

---

## 🔁 Ações Corretivas e Preventivas
| Tipo | Descrição | Responsável | Prazo |
|------|------------|--------------|-------|
| Preventiva | Criar alerta para uso de conexões > 90%. | SRE Team | 10/11 |
| Evolutiva | Implementar autoscaling no DB. | DevOps | 20/11 |
| Educacional | Revisar práticas de pooling no onboarding. | Engenharia | 30/11 |

---

## 📚 Lições Aprendidas
Liste aprendizados relevantes para o time e para a organização:
- Quais sinais poderiam ter sido percebidos antes?  
- Quais decisões ajudaram na resolução?  
- Que mudanças de processo ou automação surgiram daqui?

> “Cada incidente é uma oportunidade para melhorar sistemas, pessoas e processos.”

---

## 🧰 Melhorias Relacionadas
- Atualizar runbook relacionado: [link]  
- Criar nova métrica de saturação no dashboard.  
- Incluir alerta de latência no Prometheus.  
- Revisar dependências críticas no pipeline.

---

## 📊 Métricas
| Indicador | Valor | Observação |
|------------|--------|-------------|
| MTTD (Mean Time to Detect) | [minutos] | Tempo até detecção |
| MTTR (Mean Time to Recover) | [minutos] | Tempo até resolução |
| Tempo de Resposta do Alerta | [minutos] | Entre alerta e ação |
| Impacto Estimado | [valor ou percentual] | Financeiro, usuários, etc. |

---

## 🧠 Reflexão Blameless
> O objetivo deste post-mortem não é identificar culpados, e sim compreender **por que o sistema permitiu que o erro acontecesse**.

Perguntas para reflexão:
- O que dificultou a detecção precoce?  
- As decisões tomadas foram baseadas em dados ou suposições?  
- Que tipo de automação poderia ter prevenido ou acelerado a resposta?  
- Que aprendizado o time leva daqui?

---

## 🤖 Uso de IA (opcional)
Se houver uso de ferramentas inteligentes no processo:
- IA correlacionou alertas ou logs?  
- Gerou o rascunho inicial do post-mortem?  
- Identificou incidentes semelhantes?  
- Propôs ações corretivas?

**Exemplo:**
> IA analisou 3 mil linhas de logs e detectou padrão idêntico ao incidente de agosto, sugerindo mesma correção.

---

## 📦 Metadados
```yaml
status: [draft|reviewed|approved]
created_at: [AAAA-MM-DD]
last_updated: [AAAA-MM-DD]
reviewed_by: [responsável]
shared_with: [times envolvidos]
tags:
  - post-mortem
  - blameless
  - incident
  - reliability
```

---

## 📚 Referências e Recursos
- Dashboards: [link para Grafana]  
- Logs: [link para Kibana]  
- Runbook relacionado: [link]  
- Documentação de arquitetura: [link interno]  
- Post-Mortems anteriores: [lista ou repositório]  

---

## 👥 Responsáveis
| Função | Nome / Time | Contato |
|--------|--------------|----------|
| Autor | [Nome] | [Email ou Slack] |
| Revisor Técnico | [Nome] | [Email] |
| Acompanhamento de Ações | [Nome] | [Email] |

---

## 💬 Notas Finais
> Post-mortems são instrumentos de aprendizado contínuo.  
> Devem ser revisados e compartilhados para fortalecer a confiabilidade coletiva.  
> Versão 1.0 — Atualizado em [Data].
