# Telemt Proxy Health

Prometheus exporter + Grafana dashboard для мониторинга MTProto-прокси Telemt.

## Возможности

- Uptime MTProto-прокси
- Входящие/исходящие соединения
- Bad connections, handshake timeouts
- Upload / Download throughput
- Telegram DC upstream статус
- ME writers, активные сессии
- Security-события (desync, relay errors, force pool close)

## Метрики

| Метрика | Описание |
|---------|----------|
| Uptime | Время непрерывной работы прокси |
| Connections | Входящие/исходящие подключения |
| Bad Connections | Ошибочные подключения |
| Handshake Timeouts | Таймауты handshake |
| Upload / Download | Пропускная способность |
| Telegram DC Status | Upstream-соединения к Telegram |
| ME Writers | Активность Writers |
| Sessions | Количество активных сессий |
| Security Events | Ошибки и подозрительные события |

## Установка

### 1. Prometheus

Добавь в `prometheus.yml`:

```yaml
- job_name: telemt
  static_configs:
    - targets: ['127.0.0.1:9090']
```

### 2. Grafana

Dashboards → Import → Upload JSON → `grafana-dashboard.json`

## Структура

```
Telemt-Proxy-Health/
├── README.md
├── grafana-dashboard.json
└── prometheus.yml
```

## License

MIT
