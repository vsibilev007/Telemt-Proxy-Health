# Telemt Proxy Health

Prometheus exporter + Grafana dashboard для мониторинга MTProto-прокси Telemt.

**Совместимость:** Telemt 3.4.14 — 3.4.25

## Возможности

- Uptime MTProto-прокси
- Входящие/исходящие соединения
- Bad connections, handshake timeouts
- Upload / Download throughput
- Telegram DC upstream статус
- ME writers, активные сессии
- Security-события (desync, relay errors, force pool close)
- Per-user трафик и соединения
- Upstream success rate и latency
- ME pool drain и writer pick

## Панели Grafana

| Панель | Описание |
|--------|----------|
| Uptime | Время непрерывной работы прокси |
| Total Connections | Всего принятых подключений (counter) |
| Bad Connections | Ошибочные/отклонённые подключения |
| Handshake Timeouts | Таймауты handshake |
| Active ME Writers | Активные ME writers |
| Pool Drain Active | Draining ME writers |
| Upload / Download Rate | Текущая пропускная способность (bps) |
| Total Upload / Download | Кумулятивный объём трафика |
| Traffic Rate per User | Трафик по пользователям (bps) |
| DC→Client Data Rate | Поток данных DC → клиенты |
| Active Connections per User | Активные соединения по пользователям |
| Connection Rate | Новые соединения/сек |
| Upstream Success Rate | Доля успешных upstream-подключений |
| Upstream Attempts / Failures | Попытки и сбои upstream |
| ME Reconnect Attempts / Success | Попытки и успешные переподключения ME |
| Endpoint Quarantines | Карантин endpoints из-за rapid flaps |
| ME Writers Over Time | Динамика active/warm/draining writers |
| Upstream Connect Duration | Распределение времени подключения к upstream |
| Security & Error Events | Bad connections, handshake timeouts, desync, CRC/Seq mismatch |
| Relay Session Events | Idle soft/hard mark, pressure evict, protocol desync |
| DC→Client Flush Reasons | Причины flush DC→Client |
| ME Route Drops | Потери маршрутизации по причинам |
| Unique IPs per User | Уникальные IP по пользователям |
| Writer Pick Outcomes | Результаты выбора writer по режимам |
| Handshake Timeout Rate | Скорость handshake timeouts (anomaly detection) |
| Handshake Timeout Ratio | Доля таймаутов среди завершённых сессий |
| Relay Desync Rate | Desync-закрытия relay (признак DPI) |
| Pool Force Close Rate | Скорость принудительного закрытия пула |

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

### 3. Telemt

Убедись что метрики включены в `config.toml`:

```toml
[server]
metrics_port = 9090

[general]
telemetry_core_enabled = true
telemetry_user_enabled = true
telemetry_me_level = "normal"
```

## Структура

```
Telemt-Proxy-Health/
├── README.md
├── grafana-dashboard.json
└── prometheus.yml
```

## License

MIT
