# 🧭 Runbook: [Título descritivo do incidente ou rotina]
> **Objetivo:** Explique em uma linha o que este runbook resolve ou executa.  
> Exemplo: “Restabelecer o serviço de checkout quando a API retorna erro 503.”

---

## 📍 Contexto
Descreva o cenário em que este runbook deve ser usado:
- Serviço ou sistema afetado.
- Condições típicas do incidente.
- Relação com SLOs ou dependências críticas.

> Exemplo:  
> Este runbook trata falhas intermitentes no `checkout-service` causadas por saturação de conexões com o banco de dados.

---

## 🔍 Sintomas
Liste os sinais observáveis que indicam a necessidade deste runbook:
- Alertas específicos (ex: “HTTP 5xx > 5%”)
- Logs de erro.
- Métricas anormais.

**Exemplo:**
- `SQLTimeoutException` no log do serviço.
- Métrica `http_request_duration_seconds > 2s`.
- Latência elevada em dashboard Grafana.

---

## 💥 Impacto
Descreva o impacto operacional e de negócio:
- Serviços degradados.
- SLOs violados.
- Possível perda de receita ou experiência do usuário.

**Exemplo:**  
Indisponibilidade parcial do fluxo de pagamentos, afetando checkout e histórico de pedidos.

---

## 🧠 Causa Provável
Liste hipóteses conhecidas ou causas mais comuns observadas em incidentes anteriores.

**Exemplo:**
- Exaustão do pool de conexões JDBC.  
- Falha no serviço de banco de dados.  
- Aumento repentino de tráfego.

---

## 🧪 Diagnóstico (Passo a passo)
Passos para confirmar a causa do problema.  
Cada passo deve ser reproduzível por qualquer operador.

1. **Verificar status do pod:**
   ```bash
   kubectl get pods -n payments | grep checkout
   ```
2. **Consultar logs recentes:**
   ```bash
   kubectl logs deployment/checkout-service --tail=100
   ```
3. **Validar conexão com o banco:**
   ```bash
   kubectl exec -it pod/checkout-xyz -- nc -zv db-service 5432
   ```
4. **Checar métricas:**
   - Prometheus: `rate(http_requests_total{status="5xx"}[5m])`
   - Grafana Dashboard: *Checkout Performance*

> 💡 *Se falha de rede for detectada → seguir para Runbook “network-connectivity-issue.md”.*

---

## 🛠️ Correção (Passo a passo)
Ações para resolver ou mitigar o problema.  
Inclua comandos, scripts ou automações possíveis.

1. Reiniciar o serviço:
   ```bash
   kubectl rollout restart deployment checkout-service
   ```
2. Confirmar estabilização:
   ```bash
   kubectl get pods -n payments | grep checkout
   ```
3. Validar que o novo pod está pronto:
   ```bash
   kubectl describe pod checkout-service | grep "State"
   ```
4. Verificar logs:
   ```bash
   kubectl logs deployment/checkout-service --tail=20
   ```
5. Validar no Grafana se latência < 300ms e erro 5xx = 0.

> ⚠️ **Atenção:** nunca reiniciar mais de uma réplica simultaneamente em horário comercial.

---

## 🤖 Automação (Opcional)
Se houver script, pipeline ou ação automatizada associada ao runbook, documente aqui.

**Exemplo:**
```bash
# Script: restart-checkout.sh
kubectl rollout restart deployment checkout-service
kubectl rollout status deployment checkout-service
```

**Ferramentas integradas:**
- Ansible Playbook: `playbooks/restart_checkout.yml`
- Jenkins Pipeline: “Restart Checkout Deployment”
- Slack ChatOps Command: `/runbook checkout restart`

---

## ✅ Validação
Critérios para confirmar que a correção funcionou.

| Item | Métrica | Condição esperada | Ferramenta |
|------|----------|------------------|-------------|
| Latência média | P95 | < 300ms | Grafana |
| Erros 5xx | < 1% | Prometheus | |
| Healthcheck | HTTP 200 | curl /health | |
| Logs | Sem “SQLTimeoutException” | Kibana | |

---

## 📊 Evidências
Capture dados para auditoria ou aprendizado:
- Captura de logs antes e depois.  
- Screenshots de dashboards.  
- Tempo total de resolução (MTTR).  
- Responsável pela execução.

**Exemplo:**
```
Data/Hora Início: 2025-05-02 14:32
Data/Hora Fim: 2025-05-02 14:39
MTTR: 7 minutos
Executado por: @felipecavalieri
```

---

## 🔁 Follow-up e Melhorias
Liste ações preventivas, automações ou mudanças futuras:

- Reduzir tamanho do pool de conexões no `application.yaml`.
- Criar alerta para conexões ativas > 90%.
- Automatizar restart via pipeline GitOps.
- Adicionar teste de carga semanal no Grafana k6.

---

## 🧠 Lições Aprendidas
Preencha após o post-mortem:
- O que funcionou bem?  
- O que poderia ser automatizado?  
- Como melhorar a detecção precoce?

> “Runbooks são vivos — cada incidente deve aprimorar este documento.”

---

## 📚 Referências e Links
- Dashboard: [Checkout Performance](https://grafana.exemplo.com/d/checkout)
- Logs: [Kibana Checkout Logs](https://kibana.exemplo.com/)
- Repositório: [checkout-service GitHub](https://github.com/org/checkout-service)
- Post-Mortem Relacionado: [INC-1045](https://confluence.exemplo.com/incidents/1045)
- SLO: Latência < 300ms (P95) | Disponibilidade 99.9%

---

## 👥 Responsáveis
| Papel | Nome/Grupo | Contato |
|--------|--------------|----------|
| SRE On-Call | Squad Alpha | sre-oncall@empresa.com |
| Dono do Serviço | Checkout Team | @checkout-team |
| Escalonamento | Gerência SRE | +55 (11) 99999-9999 |

---

## 📦 Metadados (para automação)
```yaml
service: checkout-service
severity: P1
created_at: 2025-05-02
last_updated: 2025-11-05
linked_playbook: network-outage-playbook
ai_ready: true
tags:
  - sre
  - runbook
  - database
  - checkout
```

---

## 💬 Notas Finais
> Este runbook deve ser revisado a cada **três meses** ou após cada incidente P1 relacionado.  
> Versão 1.3 — Atualizado em **05/11/2025** por **Felipe Cavalieri**.
