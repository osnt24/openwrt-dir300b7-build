# OpenWRT DIR-300 B7 Custom Build

Этот репозиторий собирает с помощью GitHub Actions кастомный образ OpenWRT 22.03.5 для D-Link DIR-300 B7 (ramips/rt305x) с:

- Полным отключением IPv6 (sysctl, odhcpd, RA/SLAAC/ndp)
- TTL-спуфингом: TTL+1 для LAN, TTL=64 для WAN
- Встроенными пакетами: kmod-ipt-ttl, iptables-mod-ttl, odhcpd-ipv6only, dnsmasq-full

## Как работает

1. При пуше в `main` или вручную запускается workflow.
2. Скачивается ImageBuilder, в него копируются файлы из `files/`.
3. Собирается `factory.bin` и `sysupgrade.bin` с `.sha256` и `.config.buildinfo`.
4. Артефакты выкладываются в GitHub Actions → Artifacts.

## Установка

- **Web-upgrade**: заливаем `*-factory.bin` через OEM-интерфейс.
- **sysupgrade**: копируем `*-sysupgrade.bin` и выполняем `sysupgrade -n /tmp/…`.

---
