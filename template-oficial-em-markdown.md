# 🧭 Runbook: Falha de Comunicação com Banco de Dados (checkout-service)

## 📍 Contexto
Serviço checkout-service apresentando erros 5xx e latência acima de 2s.

## 🔍 Sintomas
- Logs: `SQLTimeoutException: timeout after 30s`
- Painel Grafana: aumento de `http_5xx_rate`
- Healthcheck falhando em `/checkout/health`

## 💥 Impacto
- Indisponibilidade parcial do checkout.
- Violação do SLO de latência (2s).
- Impacto direto em receita e experiência do usuário.

## 🧪 Diagnóstico
1. Validar conectividade com o banco:
   ```bash
   kubectl exec -it pod/checkout-xyz -- nc -zv db-service 5432
