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

## Безопасность

Реальные локальные профили, подписки и provider-файлы намеренно не отслеживаются Git. В публичный репозиторий должны попадать только переносимые примеры без личных URL, ключей и подписок.

## Cisco / Enterprise DNS

Examples не содержат конкретные корпоративные Cisco AnyConnect DNS suffixes. Если вам нужно автоматизировать такую логику, updater может добавлять managed blocks в:

- `dns.fake-ip-filter` - чтобы внутренние корпоративные домены не попадали в fake-ip.
- `dns.nameserver-policy` - чтобы эти домены резолвились через `system`, то есть через DNS, который Cisco AnyConnect выдал системе.

Это опционально: во многих сценариях Cisco AnyConnect сам настраивает локальный DNS, и отдельная автоматизация нужна только если Clash перехватывает DNS раньше системы.
