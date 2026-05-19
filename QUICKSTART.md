# Quickstart

Guia rápido para subir o ambiente local do projeto **Postgres → NATS CDC**.

## Pré-requisitos

- Docker + Docker Compose
- Porta `5432` livre (Postgres)
- Porta `4222` livre (NATS)
- Porta `8222` livre (monitoramento NATS)

## 1) Subir serviços

```bash
docker compose up -d
```

Serviços iniciados:

- `postgres` em `localhost:5432`
- `nats` em `localhost:4222`
- monitoramento NATS em `http://localhost:8222`

## 2) Verificar status

```bash
docker compose ps
```

## 3) Testar conexão no Postgres

```bash
psql -h localhost -U postgres -d outboxx_test
```

Credenciais padrão:

- usuário: `postgres`
- senha: `password`
- database: `outboxx_test`

## 4) Rodar o CDC

Exemplo com binário Zig:

```bash
./zig-out/bin/outboxx --config dev/config.toml
```

## 5) Ver eventos no NATS

Com NATS CLI:

```bash
nats sub '>' -s nats://localhost:4222
```

> Dica: use `http://localhost:8222/healthz` para checar saúde do NATS.

## 6) Encerrar ambiente

```bash
docker compose down
```
