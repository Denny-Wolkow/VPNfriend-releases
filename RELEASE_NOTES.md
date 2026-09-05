# VPNfriend 1.0.1

Bugfix and polish over 1.0.

## Fixes
- Settings schema migrations persist size/catalog together (no skipped upgrades).
- Mine secrets: DPAPI / Keychain failures no longer wipe stored login/password/key on Save.
- Mine lock: decrypt / Keychain read failure no longer unlocks the tab.
- Status card wraps long “Reason” text (Mac grows the window for 2–3 lines).
- Help/Concepts titles update when language changes before first open.
- Useful-links Hidden flag kept across merge/replace/export/import.
- Tray / menu-bar VPN client switcher (“My apps”); resets dead-tunnel state on switch.
- Safer self-replace: only kill exact VPNfriend builds; Mac no longer deletes a quiet Applications copy.
- Mac: SOCKS probe off the UI thread; Links wrap width; broadcast NIC no longer fake uplink.
- Mac: IP/geo refreshes on network change (server/country updates faster after VPN switch).
- Mac settings aligned with Windows: **Settings | Mine | Help | Concepts**; links/providers live under Mine.
- Mac install: DMG drag-to-Applications; launch from USB/disk offers copy or opens the Applications install.
- mailto: / email links allowed in support/useful lists.
- Path vs system default route reasons split (Windows).
- Guides: offline internet checklist RU/EN/ZH; useful catalog (incl. Kiwix).
- Mine tab: Links / VPN apps / Data subtabs; 14 UI languages; help bodies ru/en/zh.

## Windows
Download: [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.exe) (.NET Framework 4.x).

## macOS
Download: [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg) — drag `VPNfriend.app` onto Applications. Zip: [`VPNfriend-macOS.zip`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend-macOS.zip). macOS 12+.

## License
Proprietary — see [LICENSE](LICENSE).

---

# VPNfriend 1.0.1 (RU)

Исправления поверх 1.0: миграции настроек, «Моё»/секреты, перенос причины, быстрое обновление страны на Mac, настройки как на Windows (Моё + ссылки), установка через DMG / вопрос про «Программы», трей-переключатель VPN, офлайн-гайды RU/EN/ZH.

Скачать: Windows [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.exe) · Mac [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg).

---

# VPNfriend 1.0

First public release of the VPN watcher (not a VPN itself).

## Windows

- Status card and tray icon.
- Clients: Happ, AmneziaVPN, WireGuard, OpenVPN, ProtonVPN, Mullvad, Windscribe, Outline, Cloudflare WARP, Psiphon, Lantern, Hiddify, v2rayN, Nekoray, “Other”.
- Adapter and public IPv4 check; “dead tunnel” if the address looks like no VPN.
- Exit country from IPv4 geolocation.
- Warnings if marked programs are open without VPN.
- ipleak.net from the tray (the program itself does not test DNS/IPv6).
- UI languages: ru, en, de, fr, es, zh, uk. Help — Russian or English.

Download: [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/tag/v1.0) (.NET Framework 4.x required).

## macOS

Download: [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/tag/v1.0) — open the disk image and drag `VPNfriend.app` onto Applications. macOS 12+. Zip: [`VPNfriend-macOS.zip`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/tag/v1.0).

## License

Proprietary License: source is for viewing only. Copying, modifying, and distributing without permission is not allowed. Full text: [LICENSE](LICENSE).
