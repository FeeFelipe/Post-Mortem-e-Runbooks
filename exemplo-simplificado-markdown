# Runbook: Falha no checkout-service

🔍 Sintomas:
Erros 5xx e latência > 2s

🧪 Diagnóstico:
kubectl logs deployment/checkout-service
kubectl get pods | grep checkout

🛠️ Correção:
kubectl rollout restart deployment checkout-service

✅ Validação:
Healthcheck OK, latência < 300ms

📎 Links:
Grafana dashboard, logs Kibana
👥 Responsável: SRE Squad Alpha
