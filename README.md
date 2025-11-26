# Observabilidade com Banco de Dados e Carga Real

Este conjunto adiciona PostgreSQL + postgres-exporter + load generator + Prometheus + Grafana + nginx (HTTPS + basic auth) ao seu ambiente.

Portas publicadas no host:
- 3300 -> nginx HTTPS (proxy para Grafana)
- 22   -> container SSH (opcional)

Credenciais padrão (troque em ambiente real):
- Postgres: pguser / pgpass (DB: appdb)
- nginx basic auth: observer / pass123
- Grafana admin: admin / admin

Como rodar
1. Coloque os arquivos do projeto nas pastas indicadas.
2. docker compose up -d
3. Verifique containers: docker compose ps

Acessos
- Grafana (via HTTPS + basic auth): https://localhost:3300
  - HTTP Basic Auth: observer / pass123
  - Grafana login: admin / admin

Validar exporter do Postgres
- No host:
  docker compose exec postgres-exporter wget -qO- http://localhost:9187/metrics | head

Validar targets no Prometheus
- docker compose exec prometheus wget -qO- http://localhost:9090/api/v1/targets | jq '.'

Logs load generator
- docker compose logs -f load-generator