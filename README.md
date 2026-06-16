# Clash Verge VPN Configs

Публичные example-конфиги для Clash Verge Rev / Mihomo с раздельной логикой Abroad и Russia.

## Что внутри

- `Abroad.example.yaml` - профиль для нахождения вне России: российские сервисы идут через `RU-SITES`, глобальные сервисы остаются `DIRECT` или идут через отдельную foreign proxy-группу.
- `Russia.example.yaml` - профиль для нахождения в России: российские сервисы идут `DIRECT`, а иностранные ограниченные сервисы идут через `PROXY` / `LOW-RESTRICT-FOREIGN`.

## Как использовать

1. Скопируйте нужный `*.example.yaml` в отдельный рабочий профиль, например `Abroad.yaml`.
2. Замените `https://YOUR_CLASH_SUBSCRIPTION_URL` на URL своего Clash/Mihomo provider.
3. Замените правило `DOMAIN,your-provider.example,DIRECT` на домен своего provider, чтобы подписка обновлялась напрямую.
4. Импортируйте профиль в Clash Verge Rev и проверьте его через встроенную проверку конфигурации.

## macOS DNS preflight

На macOS перед TUN-режимом проверьте, что legacy resolver file существует:

```sh
ls -l /etc/resolv.conf /var/run/resolv.conf
```

Если `/etc/resolv.conf` отсутствует, создайте стандартную ссылку:

```sh
sudo ln -sf /var/run/resolv.conf /etc/resolv.conf
```

Mihomo/Clash Verge может читать `/etc/resolv.conf` в TUN/DNS-сценариях. Если
файла нет, DNS может падать с ошибкой `failed to read /etc/resolv.conf`, хотя
обычные macOS-приложения продолжают резолвить домены через SystemConfiguration.

## Безопасность

Реальные локальные профили, подписки и provider-файлы намеренно не отслеживаются Git. В публичный репозиторий должны попадать только переносимые примеры без личных URL, ключей и подписок.

## Cisco / Enterprise VPN

Examples не содержат конкретные корпоративные Cisco AnyConnect DNS suffixes,
IP-адреса или process rules. Проверенный переносимый минимум для macOS - рабочий
`/etc/resolv.conf` из секции выше и обычные private network rules в профиле.
Корпоративные домены/IP лучше добавлять только локально и только после проверки
логов, потому что такие правила непереносимы между компаниями и пользователями.
