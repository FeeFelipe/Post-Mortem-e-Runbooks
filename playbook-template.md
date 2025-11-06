# 🎯 Playbook: [Nome do Cenário ou Categoria de Incidente]
> **Objetivo:** Coordenar a resposta organizada a incidentes de [tipo de incidente], garantindo comunicação clara, papéis definidos e execução eficiente.

---

## 📍 Escopo
Descreva o tipo de incidente que este playbook cobre:
- Falhas críticas de infraestrutura  
- Interrupções de serviço em produção  
- Vazamentos de dados  
- Perda de conectividade ou dependência externa  

> *Exemplo:* Este playbook é aplicado a incidentes P1 que afetam disponibilidade de clientes por mais de 5 minutos.

---

## 🚨 Critérios de Ativação
Liste as condições que disparam o uso do playbook:

- Violação de SLO crítico.  
- Alerta de múltiplos serviços simultâneos.  
- Incidente escalado por canal de suporte.  
- Indisponibilidade regional detectada.  

📘 *Exemplo:* Latência acima de 5s em 3 ou mais microserviços por mais de 10 minutos.

---

## 👥 Papéis e Responsabilidades
| Papel | Responsabilidade | Contato |
|--------|------------------|----------|
| **Incident Commander (IC)** | Lidera a resposta, define prioridades, comunica status. | @ic-oncall |
| **Tech Lead** | Coordena diagnóstico técnico e execução de runbooks. | @techlead |
| **Comms Manager** | Atualiza stakeholders internos e externos. | @comms |
| **SRE / DevOps** | Executa ações corretivas e monitora impacto. | @sre-oncall |
| **Observability Lead** | Coleta métricas, logs e evidências. | @metrics-team |

💡 *Um único incidente, uma única voz: o IC tem autoridade final.*

---

## 🔁 Fluxo de Ação
### 1️⃣ Detecção
- Alerta é recebido via [ferramenta de monitoramento].  
- Incident Commander é designado automaticamente.

### 2️⃣ Diagnóstico Inicial
- Identificar o escopo e serviços afetados.  
- Acionar Runbooks correspondentes.  
- Atualizar canal de incidentes (ex: Slack #incident-room).

### 3️⃣ Mitigação
- Aplicar ações de contenção (rollback, failover, scale-up).  
- Validar se impacto está reduzindo.  
- Manter comunicação com stakeholders.

### 4️⃣ Resolução
- Confirmar restauração do serviço.  
- Validar SLOs e métricas principais.  
- Encerrar canal de incidente e registrar resumo.

### 5️⃣ Post-Mortem
- Criar documento inicial com causa, impacto e lições.  
- Marcar revisão com o time responsável.  

---

## 📡 Comunicação
Defina canais e frequência de atualização.

| Público | Canal | Frequência |
|----------|--------|------------|
| Time Técnico | Slack #incident-room | Contínuo |
| Gerência Técnica | Email / Chat | A cada 15 min |
| Stakeholders / Negócio | Status Page | A cada 30 min |
| Clientes (se aplicável) | Página de status pública | Após mitigação |

💬 *Transparência é parte da resposta — não apenas técnica, mas comunicacional.*

---

## 🧰 Recursos e Documentos Relacionados
- Runbook(s):  
  - [checkout-db-timeout.md](../runbooks/checkout-db-timeout.md)  
  - [network-connectivity-issue.md](../runbooks/network-connectivity-issue.md)
- Post-Mortem Template: [postmortem-template.md](../postmortems/postmortem-template.md)
- Lista de Contatos de Escalação: [contacts.yaml](../ops/contacts.yaml)
- Plano de Continuidade (BCP/DR): [bcp-dr.md](../bcp/bcp-dr.md)

---

## 🔒 Critérios de Encerramento
O incidente pode ser encerrado quando:
- Serviço restaurado e validado.  
- Comunicação final enviada.  
- Post-mortem aberto.  
- Ações preventivas registradas.

---

## 📊 Indicadores
| Indicador | Meta | Observação |
|------------|------|-------------|
| Tempo de reconhecimento (MTTA) | < 5 min | Tempo entre alerta e ação |
| Tempo de mitigação (MTTM) | < 15 min | Redução de impacto |
| Tempo total de recuperação (MTTR) | < 30 min | Serviço restabelecido |
| Taxa de reincidência | < 5% | Repetição do mesmo incidente |

---

## 🤖 Suporte de IA / Automação
- AIOps sugere runbook adequado baseado em padrão do alerta.  
- ChatOps (ex: Slack Bot) aciona automaticamente o IC e abre o canal do incidente.  
- IA gera minuta inicial do post-mortem após o encerramento.  
- Ferramentas correlacionam incidentes similares e notificam responsáveis.

---

## 📦 Metadados
```yaml
playbook_id: PB-001
version: 1.0
created_at: 2025-11-05
last_updated: 2025-11-05
owner: SRE Guild
related_services:
  - checkout
  - database
tags:
  - incident-response
  - blameless
  - sre
```

---

## 💬 Notas Finais
> Este playbook deve ser revisado trimestralmente e atualizado após cada incidente real ou simulado.  
> Mantê-lo vivo é o que garante uma resposta coordenada e eficaz.
