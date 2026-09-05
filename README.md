# VPNfriend

A small **VPN watcher** for Windows and macOS. It is **not** a VPN: it does not connect, route, or encrypt traffic.

VPN clients sometimes keep showing “connected” while the tunnel is already dead, the adapter is gone, or traffic is leaving on the ordinary Wi‑Fi. VPNfriend watches what the OS and this process actually see, shows it on a compact status card, and can warn you if marked programs are open while protection looks off.

**The program is still early / unfinished and is in active development.** Expect bugs, rough edges, and incomplete behaviour.

**Current version: 1.0.1** · Windows 7+ (.NET Framework 4.x) · macOS 12+

Author: [Denis Wolkow](mailto:denniesw2@gmail.com) · Questions: [Discussions](https://github.com/Denny-Wolkow/VPNfriend-releases/discussions)

---

## Download

Official builds (public): [**Releases**](https://github.com/Denny-Wolkow/VPNfriend-releases/releases). This repository is **downloads only** (no source). Source is not published. You may **not** build or publish your own copies without the author’s permission (see [LICENSE](LICENSE)).

| Platform | File |
|----------|------|
| Windows | [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.exe) |
| macOS (preferred) | [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg) — drag the app onto **Applications** |
| macOS (zip) | [`VPNfriend-macOS.zip`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend-macOS.zip) |

Same files are also in [`downloads/`](downloads/): [`VPNfriend.exe`](downloads/VPNfriend.exe), [`VPNfriend.dmg`](downloads/VPNfriend.dmg), [`VPNfriend-macOS.zip`](downloads/VPNfriend-macOS.zip).

Release notes: [RELEASE_NOTES.md](RELEASE_NOTES.md).

---

## Why it exists

Typical failure modes VPNfriend is meant to catch:

1. The client UI still says “connected”, but the virtual adapter is gone.
2. The adapter is still there, but this machine’s public IPv4 did not change (dead / broken tunnel).
3. Marked apps (browser, Telegram, Discord, torrent, Tor, custom names) are open while VPN is off.
4. Extra honesty checks: this app’s traffic not via the VPN adapter, system DNS still on ordinary Wi‑Fi, system proxy set, IPv6 path around an IPv4-only VPN.

It does **not** replace a proper browser leak test (DNS-over-HTTPS, WebRTC). For that, open [ipleak.net](https://ipleak.net) from the tray / menu-bar menu.

---

## Status card (what you see)

| Line | Meaning |
|------|---------|
| Title + colour | **On** (green) — selected client adapter is up. **Off** (red) — no such adapter. **Dead tunnel** (orange) — adapter up, but public IPv4 matched the non-VPN address twice (IP check must be on). |
| IP country | Geolocation of the public IPv4 **this program** fetched. Not the node name from Happ/subscription. `—` until IP + geo succeed. |
| IP / IPv6 | Public addresses of the VPNfriend process (if the interval is enabled). “Unchanged” means same as remembered without VPN. |
| Apps | Watched programs currently running (browsers, Telegram, Discord, torrent, Tor, custom list). |
| Reason | Short measured issues (adapter missing, SOCKS-only, path/DNS/proxy notes, dead tunnel, …). Long text wraps on the card. |

Buttons on the card: copy status, **Links** window, quiet mode, settings, open the VPN client.

---

## Checks (honest scope)

**Always (no checkbox):**

- Is the selected client’s adapter visible? (Windows: virtual NIC; Mac: usually `utun` / related, with process checks for shared tunnels.)
- Which watched apps are open?
- Does **this app’s** IPv4 / IPv6 path go via that adapter (separate from “the whole Mac/PC is in VPN”)?
- Is system DNS still configured on ordinary Wi‑Fi/Ethernet beside VPN?
- Are system proxies enabled?

**If “public IP check” is on:**

- Public IPv4 of VPNfriend (ipify and fallbacks; system proxy ignored for the request).
- Optional public IPv6 of VPNfriend.
- Dead tunnel: two samples with adapter up matching the remembered home address.
- Country = geo of that IPv4.

Local Happ SOCKS without an adapter is **not** counted as VPN On.

---

## Settings overview

Tabs (same idea on Windows and Mac):

1. **Settings** — VPN client, language, watched apps, grace periods, toasts/warnings, IP interval, window size/font/opacity, autostart (desktop shortcut on Windows).
2. **Mine** — personal data behind an optional password:
   - **Links** — useful third-party links (outages, DNS, maps, …); tick which appear in the Links window.
   - **VPN apps** — your collection of clients to switch from the tray / menu bar.
   - **Data** — VPN providers (site, Telegram, Discord, email, optional secrets) and Mine lock password.
3. **Help** / **Concepts** — built-in topics (RU/EN/ZH for long bodies where available).

**Links window** (chain button): searchable list of ticked useful links + provider contacts. Empty until you tick items under Mine.

UI languages: Russian, English, German, French, Spanish, Chinese, Ukrainian, Portuguese, Japanese, Korean, Arabic, Turkish, Vietnamese, Italian (14). Long help/concepts: primarily RU / EN / ZH.

---

## Supported clients

Happ, AmneziaVPN, WireGuard, OpenVPN, ProtonVPN, Mullvad, Windscribe, Outline, Cloudflare WARP, Psiphon, Lantern, Hiddify, v2rayN, Nekoray, or **Other** (process name without `.exe`).

Psiphon/Lantern in **proxy-only** mode (no adapter) will not show as On.

---

## Windows

.NET Framework 4.x (usually already installed).

1. Download [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.exe).
2. Run it. Only one instance; a newer copy from another folder can replace the old one.
3. Tray icon + floating card. Settings from the gear or tray menu.

**Uninstall:** tray → “Uninstall VPNfriend…”. If you delete the exe by hand, turn off autostart first (`HKCU\Software\Microsoft\Windows\CurrentVersion\Run` → `VPNfriend`).

Log: `vpnfriend.log` next to the program (trimmed automatically).

Local build (author / with permission): `Build-VPNfriend.bat`.

---

## macOS

macOS 12+. Prefer the DMG:

1. Open [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg).
2. **Drag `VPNfriend.app` onto the Applications folder** in that window.
3. Eject the disk. Open VPNfriend from Applications (not from the USB/DMG).

If you launch from a USB/disk first, the app asks to copy into Applications (or to open the copy already there). After install, use the Applications copy.

Gatekeeper: right-click → Open if needed.

On Mac, VPNfriend lives in the **menu bar** (green/red circle), not in the Dock. Left-click → card; right-click → menu. Shared `utun` counts only if the selected client process is running. Safari counts as a browser.

Sources: [`mac/`](mac/). Build: see [`mac/README.txt`](mac/README.txt).

---

## What it is not

- Not a VPN, not a client, not a kill switch that blocks traffic.
- Not a full DNS / IPv6 / WebRTC browser audit (use ipleak.net).
- Not proof that “every app on the machine is inside the VPN”.

---

## Security notes

- Provider login/password/key under **Mine** are stored with OS protection (Windows DPAPI / macOS Keychain).
- Mine tab can be locked with a password.
- The program does not send your data to ipleak.net; the menu only opens the site in the browser.

---

## Legal Notice & Terms of Use

© 2026 **Denny-Wolkow**. All rights reserved.

Full proprietary license: [LICENSE](LICENSE).

Publishing this project on GitHub does **not** waive copyright. Access is for viewing / educational transparency. Copying, modifying, redistributing, or using the code in other products without written permission is prohibited. Software is provided **AS IS**, without warranty.

---
---

# VPNfriend

Небольшой **наблюдатель за VPN** для Windows и macOS. Это **не** VPN: программа ничего не подключает и не шифрует.

Клиент иногда показывает «подключено», а адаптера уже нет, туннель мёртв, или трафик уходит в обычный Wi‑Fi. VPNfriend смотрит, что реально видно системе и самому процессу, показывает это на карточке и может предупредить, если открыты отмеченные программы, а защиты нет.

**Программа ещё сырая и находится в процессе разработки.** Возможны ошибки, шероховатости и незавершённое поведение.

**Текущая версия: 1.0.1** · Windows 7+ (.NET Framework 4.x) · macOS 12+

Автор: [Denis Wolkow](mailto:denniesw2@gmail.com) · Вопросы: [Discussions](https://github.com/Denny-Wolkow/VPNfriend-releases/discussions)

---

## Скачать

Официальные сборки (публичные): [**Releases**](https://github.com/Denny-Wolkow/VPNfriend-releases/releases). Этот репозиторий **закрытый** (исходники). Собирать и выкладывать свои копии **нельзя** без разрешения автора ([LICENSE](LICENSE)).

| Платформа | Файл |
|-----------|------|
| Windows | [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.exe) |
| macOS (удобнее) | [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg) — перетащите приложение на **«Программы»** |
| macOS (zip) | [`VPNfriend-macOS.zip`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend-macOS.zip) |

Те же файлы лежат в [`downloads/`](downloads/): [`VPNfriend.exe`](downloads/VPNfriend.exe), [`VPNfriend.dmg`](downloads/VPNfriend.dmg), [`VPNfriend-macOS.zip`](downloads/VPNfriend-macOS.zip).

Заметки к выпускам: [RELEASE_NOTES.md](RELEASE_NOTES.md).

---

## Зачем это нужно

Типичные случаи:

1. В клиенте «подключено», а виртуальной карты уже нет.
2. Карта есть, но публичный IPv4 как без VPN (мёртвый туннель).
3. Открыты браузер / Telegram / Discord / торрент / Tor (и свои имена), а VPN выкл.
4. Дополнительно: путь этой программы мимо VPN-адаптера, системный DNS на обычной сети, системные прокси, IPv6 мимо IPv4-only VPN.

Это **не** замена проверки «глазами сайта» (DoH, WebRTC). Для этого — [ipleak.net](https://ipleak.net) из меню трея / кружка.

---

## Карточка статуса

| Строка | Смысл |
|--------|--------|
| Заголовок и цвет | **Вкл** (зелёный) — виден адаптер выбранного клиента. **Выкл** (красный) — адаптера нет. **Туннель мёртв** (оранжевый) — адаптер есть, а публичный IPv4 два раза совпал с адресом без VPN (нужна проверка IP). |
| Страна IP | Гео публичного IPv4, который получила **сама** программа. Не имя узла из Happ. `—`, пока нет IP и гео. |
| IP / IPv6 | Публичные адреса процесса VPNfriend (если интервал включён). «Не сменился» — как запомненный домашний. |
| Приложения | Отмеченные программы, которые сейчас открыты. |
| Причина | Краткие измерения (нет адаптера, только SOCKS, путь/DNS/прокси, мёртвый туннель…). Длинный текст переносится. |

Кнопки: копировать статус, окно **Ссылки**, тихий режим, настройки, открыть VPN-клиент.

---

## Что проверяет (честные границы)

**Всегда:**

- виден ли адаптер выбранного клиента;
- какие отмеченные программы открыты;
- идёт ли интернет **этой** программы через адаптер (это не «весь компьютер в VPN»);
- не остался ли системный DNS на обычном Wi‑Fi/кабеле;
- не включены ли системные прокси.

**Если включена проверка внешнего IP:**

- публичный IPv4 VPNfriend;
- при наличии — публичный IPv6;
- мёртвый туннель (два совпадения с домашним адресом при поднятом адаптере);
- страна по гео этого IPv4.

Локальный SOCKS Happ без адаптера зелёным **не** считается.

---

## Настройки

1. **Настройки** — клиент, язык, наблюдение за программами, паузы, предупреждения, интервал IP, размер/шрифт/прозрачность, автозапуск (ярлык на рабочий стол — на Windows).
2. **Моё** (можно закрыть паролем):
   - **Ссылки** — полезные сторонние сайты; галочка — показывать в окне «Ссылки»;
   - **VPN-приложения** — коллекция клиентов для переключения из трея / меню кружка;
   - **Данные** — поставщики (сайт, Telegram, Discord, почта, секреты) и пароль на вкладку.
3. **Справка** / **Понятия** — встроенные тексты (длинные тела — RU / EN / ZH).

Окно **Ссылки** (кнопка с цепью): поиск по отмеченным полезным ссылкам и контактам провайдеров.

Языки интерфейса: 14. Длинная справка — в основном RU / EN / ZH.

---

## Клиенты

Happ, AmneziaVPN, WireGuard, OpenVPN, ProtonVPN, Mullvad, Windscribe, Outline, Cloudflare WARP, Psiphon, Lantern, Hiddify, v2rayN, Nekoray или **«Другое»** (имя процесса без `.exe`).

Psiphon/Lantern только как прокси (без адаптера) программа не увидит как «Вкл».

---

## Windows

Нужен .NET Framework 4.x.

1. Скачайте [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.exe).
2. Запустите. Один экземпляр; новая копия из другой папки может заменить старую.
3. Значок в трее и карточка. Настройки — шестерёнка или меню трея.

**Удаление:** трей → «Удалить VPNfriend…». Если стираете exe руками — сначала снимите автозапуск.

Лог: `vpnfriend.log` рядом с программой.

Сборка: `Build-VPNfriend.bat` (для автора / с разрешением).

---

## macOS

macOS 12+. Удобнее DMG:

1. Откройте [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg).
2. **Перетащите `VPNfriend.app` на папку «Программы»** в окне диска.
3. Извлеките диск. Запускайте из «Программы», не с флешки/DMG.

Если открыли с флешки — программа предложит скопировать в «Программы» или открыть уже установленную копию.

Gatekeeper: правый клик → «Открыть».

На Mac — **кружок в строке меню** (не Dock). Левый клик — карточка, правый — меню. Общий `utun` засчитывается только при запущенном процессе выбранного клиента. Safari входит в браузеры.

Исходники: [`mac/`](mac/). Сборка: [`mac/README.txt`](mac/README.txt).

---

## Чего нет

- Это не VPN, не клиент и не kill switch.
- Это не полный аудит DNS / IPv6 / WebRTC в браузере (ipleak.net).
- Это не доказательство, что «все программы системы в VPN».

---

## Безопасность

- Логин/пароль/ключ провайдеров в **Моё** — через защиту ОС (DPAPI / Keychain).
- Вкладку «Моё» можно закрыть паролем.
- На ipleak.net данные не отправляются — только открывается страница в браузере.

---

## Правовой статус

© 2026 **Denny-Wolkow**. Все права защищены.

Полный текст: [LICENSE](LICENSE). Публикация на GitHub **не** отменяет авторские права. Копирование, изменение и распространение без письменного разрешения запрещены. ПО предоставляется **как есть**, без гарантий.
