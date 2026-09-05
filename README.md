# VPNfriend

A small **VPN watcher** for Windows and macOS. It is **not** a VPN: it does not connect, route, or encrypt traffic.

VPN clients sometimes keep showing вЂњconnectedвЂќ while the tunnel is already dead, the adapter is gone, or traffic is leaving on the ordinary WiвЂ‘Fi. VPNfriend watches what the OS and this process actually see, shows it on a compact status card, and can warn you if marked programs are open while protection looks off.

**The program is still early / unfinished and is in active development.** Expect bugs, rough edges, and incomplete behaviour.

**Current version: 1.0.1** В· Windows 7+ (.NET Framework 4.x) В· macOS 12+

Author: [Denis Wolkow](mailto:denniesw2@gmail.com) В· Questions: [Discussions](https://github.com/Denny-Wolkow/VPNfriend-releases/discussions)

---

## Download

Official builds (public): [**Releases**](https://github.com/Denny-Wolkow/VPNfriend-releases/releases). This repository is **downloads only** (no source). Source is not published. You may **not** build or publish your own copies without the authorвЂ™s permission (see [LICENSE](LICENSE)).

| Platform | File |
|----------|------|
| Windows | [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.exe) |
| macOS (preferred) | [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg) вЂ” drag the app onto **Applications** |
| macOS (zip) | [`VPNfriend-macOS.zip`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend-macOS.zip) |

Release notes: [RELEASE_NOTES.md](RELEASE_NOTES.md).

---

## Why it exists

Typical failure modes VPNfriend is meant to catch:

1. The client UI still says вЂњconnectedвЂќ, but the virtual adapter is gone.
2. The adapter is still there, but this machineвЂ™s public IPv4 did not change (dead / broken tunnel).
3. Marked apps (browser, Telegram, Discord, torrent, Tor, custom names) are open while VPN is off.
4. Extra honesty checks: this appвЂ™s traffic not via the VPN adapter, system DNS still on ordinary WiвЂ‘Fi, system proxy set, IPv6 path around an IPv4-only VPN.

It does **not** replace a proper browser leak test (DNS-over-HTTPS, WebRTC). For that, open [ipleak.net](https://ipleak.net) from the tray / menu-bar menu.

---

## Status card (what you see)

| Line | Meaning |
|------|---------|
| Title + colour | **On** (green) вЂ” selected client adapter is up. **Off** (red) вЂ” no such adapter. **Dead tunnel** (orange) вЂ” adapter up, but public IPv4 matched the non-VPN address twice (IP check must be on). |
| IP country | Geolocation of the public IPv4 **this program** fetched. Not the node name from Happ/subscription. `вЂ”` until IP + geo succeed. |
| IP / IPv6 | Public addresses of the VPNfriend process (if the interval is enabled). вЂњUnchangedвЂќ means same as remembered without VPN. |
| Apps | Watched programs currently running (browsers, Telegram, Discord, torrent, Tor, custom list). |
| Reason | Short measured issues (adapter missing, SOCKS-only, path/DNS/proxy notes, dead tunnel, вЂ¦). Long text wraps on the card. |

Buttons on the card: copy status, **Links** window, quiet mode, settings, open the VPN client.

---

## Checks (honest scope)

**Always (no checkbox):**

- Is the selected clientвЂ™s adapter visible? (Windows: virtual NIC; Mac: usually `utun` / related, with process checks for shared tunnels.)
- Which watched apps are open?
- Does **this appвЂ™s** IPv4 / IPv6 path go via that adapter (separate from вЂњthe whole Mac/PC is in VPNвЂќ)?
- Is system DNS still configured on ordinary WiвЂ‘Fi/Ethernet beside VPN?
- Are system proxies enabled?

**If вЂњpublic IP checkвЂќ is on:**

- Public IPv4 of VPNfriend (ipify and fallbacks; system proxy ignored for the request).
- Optional public IPv6 of VPNfriend.
- Dead tunnel: two samples with adapter up matching the remembered home address.
- Country = geo of that IPv4.

Local Happ SOCKS without an adapter is **not** counted as VPN On.

---

## Settings overview

Tabs (same idea on Windows and Mac):

1. **Settings** вЂ” VPN client, language, watched apps, grace periods, toasts/warnings, IP interval, window size/font/opacity, autostart (desktop shortcut on Windows).
2. **Mine** вЂ” personal data behind an optional password:
   - **Links** вЂ” useful third-party links (outages, DNS, maps, вЂ¦); tick which appear in the Links window.
   - **VPN apps** вЂ” your collection of clients to switch from the tray / menu bar.
   - **Data** вЂ” VPN providers (site, Telegram, Discord, email, optional secrets) and Mine lock password.
3. **Help** / **Concepts** вЂ” built-in topics (RU/EN/ZH for long bodies where available).

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

**Uninstall:** tray в†’ вЂњUninstall VPNfriendвЂ¦вЂќ. If you delete the exe by hand, turn off autostart first (`HKCU\Software\Microsoft\Windows\CurrentVersion\Run` в†’ `VPNfriend`).

Log: `vpnfriend.log` next to the program (trimmed automatically).

Local build (author / with permission): `Build-VPNfriend.bat`.

---

## macOS

macOS 12+. Prefer the DMG:

1. Open [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg).
2. **Drag `VPNfriend.app` onto the Applications folder** in that window.
3. Eject the disk. Open VPNfriend from Applications (not from the USB/DMG).

If you launch from a USB/disk first, the app asks to copy into Applications (or to open the copy already there). After install, use the Applications copy.

Gatekeeper: right-click в†’ Open if needed.

On Mac, VPNfriend lives in the **menu bar** (green/red circle), not in the Dock. Left-click в†’ card; right-click в†’ menu. Shared `utun` counts only if the selected client process is running. Safari counts as a browser.

Sources: [`mac/`](mac/). Build: see [`mac/README.txt`](mac/README.txt).

---

## What it is not

- Not a VPN, not a client, not a kill switch that blocks traffic.
- Not a full DNS / IPv6 / WebRTC browser audit (use ipleak.net).
- Not proof that вЂњevery app on the machine is inside the VPNвЂќ.

---

## Security notes

- Provider login/password/key under **Mine** are stored with OS protection (Windows DPAPI / macOS Keychain).
- Mine tab can be locked with a password.
- The program does not send your data to ipleak.net; the menu only opens the site in the browser.

---

## Legal Notice & Terms of Use

В© 2026 **Denny-Wolkow**. All rights reserved.

Full proprietary license: [LICENSE](LICENSE).

Publishing this project on GitHub does **not** waive copyright. Access is for viewing / educational transparency. Copying, modifying, redistributing, or using the code in other products without written permission is prohibited. Software is provided **AS IS**, without warranty.

---
---

# VPNfriend

РќРµР±РѕР»СЊС€РѕР№ **РЅР°Р±Р»СЋРґР°С‚РµР»СЊ Р·Р° VPN** РґР»СЏ Windows Рё macOS. Р­С‚Рѕ **РЅРµ** VPN: РїСЂРѕРіСЂР°РјРјР° РЅРёС‡РµРіРѕ РЅРµ РїРѕРґРєР»СЋС‡Р°РµС‚ Рё РЅРµ С€РёС„СЂСѓРµС‚.

РљР»РёРµРЅС‚ РёРЅРѕРіРґР° РїРѕРєР°Р·С‹РІР°РµС‚ В«РїРѕРґРєР»СЋС‡РµРЅРѕВ», Р° Р°РґР°РїС‚РµСЂР° СѓР¶Рµ РЅРµС‚, С‚СѓРЅРЅРµР»СЊ РјС‘СЂС‚РІ, РёР»Рё С‚СЂР°С„РёРє СѓС…РѕРґРёС‚ РІ РѕР±С‹С‡РЅС‹Р№ WiвЂ‘Fi. VPNfriend СЃРјРѕС‚СЂРёС‚, С‡С‚Рѕ СЂРµР°Р»СЊРЅРѕ РІРёРґРЅРѕ СЃРёСЃС‚РµРјРµ Рё СЃР°РјРѕРјСѓ РїСЂРѕС†РµСЃСЃСѓ, РїРѕРєР°Р·С‹РІР°РµС‚ СЌС‚Рѕ РЅР° РєР°СЂС‚РѕС‡РєРµ Рё РјРѕР¶РµС‚ РїСЂРµРґСѓРїСЂРµРґРёС‚СЊ, РµСЃР»Рё РѕС‚РєСЂС‹С‚С‹ РѕС‚РјРµС‡РµРЅРЅС‹Рµ РїСЂРѕРіСЂР°РјРјС‹, Р° Р·Р°С‰РёС‚С‹ РЅРµС‚.

**РџСЂРѕРіСЂР°РјРјР° РµС‰С‘ СЃС‹СЂР°СЏ Рё РЅР°С…РѕРґРёС‚СЃСЏ РІ РїСЂРѕС†РµСЃСЃРµ СЂР°Р·СЂР°Р±РѕС‚РєРё.** Р’РѕР·РјРѕР¶РЅС‹ РѕС€РёР±РєРё, С€РµСЂРѕС…РѕРІР°С‚РѕСЃС‚Рё Рё РЅРµР·Р°РІРµСЂС€С‘РЅРЅРѕРµ РїРѕРІРµРґРµРЅРёРµ.

**РўРµРєСѓС‰Р°СЏ РІРµСЂСЃРёСЏ: 1.0.1** В· Windows 7+ (.NET Framework 4.x) В· macOS 12+

РђРІС‚РѕСЂ: [Denis Wolkow](mailto:denniesw2@gmail.com) В· Р’РѕРїСЂРѕСЃС‹: [Discussions](https://github.com/Denny-Wolkow/VPNfriend-releases/discussions)

---

## РЎРєР°С‡Р°С‚СЊ

РћС„РёС†РёР°Р»СЊРЅС‹Рµ СЃР±РѕСЂРєРё (РїСѓР±Р»РёС‡РЅС‹Рµ): [**Releases**](https://github.com/Denny-Wolkow/VPNfriend-releases/releases). Р­С‚РѕС‚ СЂРµРїРѕР·РёС‚РѕСЂРёР№ **Р·Р°РєСЂС‹С‚С‹Р№** (РёСЃС…РѕРґРЅРёРєРё). РЎРѕР±РёСЂР°С‚СЊ Рё РІС‹РєР»Р°РґС‹РІР°С‚СЊ СЃРІРѕРё РєРѕРїРёРё **РЅРµР»СЊР·СЏ** Р±РµР· СЂР°Р·СЂРµС€РµРЅРёСЏ Р°РІС‚РѕСЂР° ([LICENSE](LICENSE)).

| РџР»Р°С‚С„РѕСЂРјР° | Р¤Р°Р№Р» |
|-----------|------|
| Windows | [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.exe) |
| macOS (СѓРґРѕР±РЅРµРµ) | [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg) вЂ” РїРµСЂРµС‚Р°С‰РёС‚Рµ РїСЂРёР»РѕР¶РµРЅРёРµ РЅР° **В«РџСЂРѕРіСЂР°РјРјС‹В»** |
| macOS (zip) | [`VPNfriend-macOS.zip`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend-macOS.zip) |

Р—Р°РјРµС‚РєРё Рє РІС‹РїСѓСЃРєР°Рј: [RELEASE_NOTES.md](RELEASE_NOTES.md).

---

## Р—Р°С‡РµРј СЌС‚Рѕ РЅСѓР¶РЅРѕ

РўРёРїРёС‡РЅС‹Рµ СЃР»СѓС‡Р°Рё:

1. Р’ РєР»РёРµРЅС‚Рµ В«РїРѕРґРєР»СЋС‡РµРЅРѕВ», Р° РІРёСЂС‚СѓР°Р»СЊРЅРѕР№ РєР°СЂС‚С‹ СѓР¶Рµ РЅРµС‚.
2. РљР°СЂС‚Р° РµСЃС‚СЊ, РЅРѕ РїСѓР±Р»РёС‡РЅС‹Р№ IPv4 РєР°Рє Р±РµР· VPN (РјС‘СЂС‚РІС‹Р№ С‚СѓРЅРЅРµР»СЊ).
3. РћС‚РєСЂС‹С‚С‹ Р±СЂР°СѓР·РµСЂ / Telegram / Discord / С‚РѕСЂСЂРµРЅС‚ / Tor (Рё СЃРІРѕРё РёРјРµРЅР°), Р° VPN РІС‹РєР».
4. Р”РѕРїРѕР»РЅРёС‚РµР»СЊРЅРѕ: РїСѓС‚СЊ СЌС‚РѕР№ РїСЂРѕРіСЂР°РјРјС‹ РјРёРјРѕ VPN-Р°РґР°РїС‚РµСЂР°, СЃРёСЃС‚РµРјРЅС‹Р№ DNS РЅР° РѕР±С‹С‡РЅРѕР№ СЃРµС‚Рё, СЃРёСЃС‚РµРјРЅС‹Рµ РїСЂРѕРєСЃРё, IPv6 РјРёРјРѕ IPv4-only VPN.

Р­С‚Рѕ **РЅРµ** Р·Р°РјРµРЅР° РїСЂРѕРІРµСЂРєРё В«РіР»Р°Р·Р°РјРё СЃР°Р№С‚Р°В» (DoH, WebRTC). Р”Р»СЏ СЌС‚РѕРіРѕ вЂ” [ipleak.net](https://ipleak.net) РёР· РјРµРЅСЋ С‚СЂРµСЏ / РєСЂСѓР¶РєР°.

---

## РљР°СЂС‚РѕС‡РєР° СЃС‚Р°С‚СѓСЃР°

| РЎС‚СЂРѕРєР° | РЎРјС‹СЃР» |
|--------|--------|
| Р—Р°РіРѕР»РѕРІРѕРє Рё С†РІРµС‚ | **Р’РєР»** (Р·РµР»С‘РЅС‹Р№) вЂ” РІРёРґРµРЅ Р°РґР°РїС‚РµСЂ РІС‹Р±СЂР°РЅРЅРѕРіРѕ РєР»РёРµРЅС‚Р°. **Р’С‹РєР»** (РєСЂР°СЃРЅС‹Р№) вЂ” Р°РґР°РїС‚РµСЂР° РЅРµС‚. **РўСѓРЅРЅРµР»СЊ РјС‘СЂС‚РІ** (РѕСЂР°РЅР¶РµРІС‹Р№) вЂ” Р°РґР°РїС‚РµСЂ РµСЃС‚СЊ, Р° РїСѓР±Р»РёС‡РЅС‹Р№ IPv4 РґРІР° СЂР°Р·Р° СЃРѕРІРїР°Р» СЃ Р°РґСЂРµСЃРѕРј Р±РµР· VPN (РЅСѓР¶РЅР° РїСЂРѕРІРµСЂРєР° IP). |
| РЎС‚СЂР°РЅР° IP | Р“РµРѕ РїСѓР±Р»РёС‡РЅРѕРіРѕ IPv4, РєРѕС‚РѕСЂС‹Р№ РїРѕР»СѓС‡РёР»Р° **СЃР°РјР°** РїСЂРѕРіСЂР°РјРјР°. РќРµ РёРјСЏ СѓР·Р»Р° РёР· Happ. `вЂ”`, РїРѕРєР° РЅРµС‚ IP Рё РіРµРѕ. |
| IP / IPv6 | РџСѓР±Р»РёС‡РЅС‹Рµ Р°РґСЂРµСЃР° РїСЂРѕС†РµСЃСЃР° VPNfriend (РµСЃР»Рё РёРЅС‚РµСЂРІР°Р» РІРєР»СЋС‡С‘РЅ). В«РќРµ СЃРјРµРЅРёР»СЃСЏВ» вЂ” РєР°Рє Р·Р°РїРѕРјРЅРµРЅРЅС‹Р№ РґРѕРјР°С€РЅРёР№. |
| РџСЂРёР»РѕР¶РµРЅРёСЏ | РћС‚РјРµС‡РµРЅРЅС‹Рµ РїСЂРѕРіСЂР°РјРјС‹, РєРѕС‚РѕСЂС‹Рµ СЃРµР№С‡Р°СЃ РѕС‚РєСЂС‹С‚С‹. |
| РџСЂРёС‡РёРЅР° | РљСЂР°С‚РєРёРµ РёР·РјРµСЂРµРЅРёСЏ (РЅРµС‚ Р°РґР°РїС‚РµСЂР°, С‚РѕР»СЊРєРѕ SOCKS, РїСѓС‚СЊ/DNS/РїСЂРѕРєСЃРё, РјС‘СЂС‚РІС‹Р№ С‚СѓРЅРЅРµР»СЊвЂ¦). Р”Р»РёРЅРЅС‹Р№ С‚РµРєСЃС‚ РїРµСЂРµРЅРѕСЃРёС‚СЃСЏ. |

РљРЅРѕРїРєРё: РєРѕРїРёСЂРѕРІР°С‚СЊ СЃС‚Р°С‚СѓСЃ, РѕРєРЅРѕ **РЎСЃС‹Р»РєРё**, С‚РёС…РёР№ СЂРµР¶РёРј, РЅР°СЃС‚СЂРѕР№РєРё, РѕС‚РєСЂС‹С‚СЊ VPN-РєР»РёРµРЅС‚.

---

## Р§С‚Рѕ РїСЂРѕРІРµСЂСЏРµС‚ (С‡РµСЃС‚РЅС‹Рµ РіСЂР°РЅРёС†С‹)

**Р’СЃРµРіРґР°:**

- РІРёРґРµРЅ Р»Рё Р°РґР°РїС‚РµСЂ РІС‹Р±СЂР°РЅРЅРѕРіРѕ РєР»РёРµРЅС‚Р°;
- РєР°РєРёРµ РѕС‚РјРµС‡РµРЅРЅС‹Рµ РїСЂРѕРіСЂР°РјРјС‹ РѕС‚РєСЂС‹С‚С‹;
- РёРґС‘С‚ Р»Рё РёРЅС‚РµСЂРЅРµС‚ **СЌС‚РѕР№** РїСЂРѕРіСЂР°РјРјС‹ С‡РµСЂРµР· Р°РґР°РїС‚РµСЂ (СЌС‚Рѕ РЅРµ В«РІРµСЃСЊ РєРѕРјРїСЊСЋС‚РµСЂ РІ VPNВ»);
- РЅРµ РѕСЃС‚Р°Р»СЃСЏ Р»Рё СЃРёСЃС‚РµРјРЅС‹Р№ DNS РЅР° РѕР±С‹С‡РЅРѕРј WiвЂ‘Fi/РєР°Р±РµР»Рµ;
- РЅРµ РІРєР»СЋС‡РµРЅС‹ Р»Рё СЃРёСЃС‚РµРјРЅС‹Рµ РїСЂРѕРєСЃРё.

**Р•СЃР»Рё РІРєР»СЋС‡РµРЅР° РїСЂРѕРІРµСЂРєР° РІРЅРµС€РЅРµРіРѕ IP:**

- РїСѓР±Р»РёС‡РЅС‹Р№ IPv4 VPNfriend;
- РїСЂРё РЅР°Р»РёС‡РёРё вЂ” РїСѓР±Р»РёС‡РЅС‹Р№ IPv6;
- РјС‘СЂС‚РІС‹Р№ С‚СѓРЅРЅРµР»СЊ (РґРІР° СЃРѕРІРїР°РґРµРЅРёСЏ СЃ РґРѕРјР°С€РЅРёРј Р°РґСЂРµСЃРѕРј РїСЂРё РїРѕРґРЅСЏС‚РѕРј Р°РґР°РїС‚РµСЂРµ);
- СЃС‚СЂР°РЅР° РїРѕ РіРµРѕ СЌС‚РѕРіРѕ IPv4.

Р›РѕРєР°Р»СЊРЅС‹Р№ SOCKS Happ Р±РµР· Р°РґР°РїС‚РµСЂР° Р·РµР»С‘РЅС‹Рј **РЅРµ** СЃС‡РёС‚Р°РµС‚СЃСЏ.

---

## РќР°СЃС‚СЂРѕР№РєРё

1. **РќР°СЃС‚СЂРѕР№РєРё** вЂ” РєР»РёРµРЅС‚, СЏР·С‹Рє, РЅР°Р±Р»СЋРґРµРЅРёРµ Р·Р° РїСЂРѕРіСЂР°РјРјР°РјРё, РїР°СѓР·С‹, РїСЂРµРґСѓРїСЂРµР¶РґРµРЅРёСЏ, РёРЅС‚РµСЂРІР°Р» IP, СЂР°Р·РјРµСЂ/С€СЂРёС„С‚/РїСЂРѕР·СЂР°С‡РЅРѕСЃС‚СЊ, Р°РІС‚РѕР·Р°РїСѓСЃРє (СЏСЂР»С‹Рє РЅР° СЂР°Р±РѕС‡РёР№ СЃС‚РѕР» вЂ” РЅР° Windows).
2. **РњРѕС‘** (РјРѕР¶РЅРѕ Р·Р°РєСЂС‹С‚СЊ РїР°СЂРѕР»РµРј):
   - **РЎСЃС‹Р»РєРё** вЂ” РїРѕР»РµР·РЅС‹Рµ СЃС‚РѕСЂРѕРЅРЅРёРµ СЃР°Р№С‚С‹; РіР°Р»РѕС‡РєР° вЂ” РїРѕРєР°Р·С‹РІР°С‚СЊ РІ РѕРєРЅРµ В«РЎСЃС‹Р»РєРёВ»;
   - **VPN-РїСЂРёР»РѕР¶РµРЅРёСЏ** вЂ” РєРѕР»Р»РµРєС†РёСЏ РєР»РёРµРЅС‚РѕРІ РґР»СЏ РїРµСЂРµРєР»СЋС‡РµРЅРёСЏ РёР· С‚СЂРµСЏ / РјРµРЅСЋ РєСЂСѓР¶РєР°;
   - **Р”Р°РЅРЅС‹Рµ** вЂ” РїРѕСЃС‚Р°РІС‰РёРєРё (СЃР°Р№С‚, Telegram, Discord, РїРѕС‡С‚Р°, СЃРµРєСЂРµС‚С‹) Рё РїР°СЂРѕР»СЊ РЅР° РІРєР»Р°РґРєСѓ.
3. **РЎРїСЂР°РІРєР°** / **РџРѕРЅСЏС‚РёСЏ** вЂ” РІСЃС‚СЂРѕРµРЅРЅС‹Рµ С‚РµРєСЃС‚С‹ (РґР»РёРЅРЅС‹Рµ С‚РµР»Р° вЂ” RU / EN / ZH).

РћРєРЅРѕ **РЎСЃС‹Р»РєРё** (РєРЅРѕРїРєР° СЃ С†РµРїСЊСЋ): РїРѕРёСЃРє РїРѕ РѕС‚РјРµС‡РµРЅРЅС‹Рј РїРѕР»РµР·РЅС‹Рј СЃСЃС‹Р»РєР°Рј Рё РєРѕРЅС‚Р°РєС‚Р°Рј РїСЂРѕРІР°Р№РґРµСЂРѕРІ.

РЇР·С‹РєРё РёРЅС‚РµСЂС„РµР№СЃР°: 14. Р”Р»РёРЅРЅР°СЏ СЃРїСЂР°РІРєР° вЂ” РІ РѕСЃРЅРѕРІРЅРѕРј RU / EN / ZH.

---

## РљР»РёРµРЅС‚С‹

Happ, AmneziaVPN, WireGuard, OpenVPN, ProtonVPN, Mullvad, Windscribe, Outline, Cloudflare WARP, Psiphon, Lantern, Hiddify, v2rayN, Nekoray РёР»Рё **В«Р”СЂСѓРіРѕРµВ»** (РёРјСЏ РїСЂРѕС†РµСЃСЃР° Р±РµР· `.exe`).

Psiphon/Lantern С‚РѕР»СЊРєРѕ РєР°Рє РїСЂРѕРєСЃРё (Р±РµР· Р°РґР°РїС‚РµСЂР°) РїСЂРѕРіСЂР°РјРјР° РЅРµ СѓРІРёРґРёС‚ РєР°Рє В«Р’РєР»В».

---

## Windows

РќСѓР¶РµРЅ .NET Framework 4.x.

1. РЎРєР°С‡Р°Р№С‚Рµ [`VPNfriend.exe`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.exe).
2. Р—Р°РїСѓСЃС‚РёС‚Рµ. РћРґРёРЅ СЌРєР·РµРјРїР»СЏСЂ; РЅРѕРІР°СЏ РєРѕРїРёСЏ РёР· РґСЂСѓРіРѕР№ РїР°РїРєРё РјРѕР¶РµС‚ Р·Р°РјРµРЅРёС‚СЊ СЃС‚Р°СЂСѓСЋ.
3. Р—РЅР°С‡РѕРє РІ С‚СЂРµРµ Рё РєР°СЂС‚РѕС‡РєР°. РќР°СЃС‚СЂРѕР№РєРё вЂ” С€РµСЃС‚РµСЂС‘РЅРєР° РёР»Рё РјРµРЅСЋ С‚СЂРµСЏ.

**РЈРґР°Р»РµРЅРёРµ:** С‚СЂРµР№ в†’ В«РЈРґР°Р»РёС‚СЊ VPNfriendвЂ¦В». Р•СЃР»Рё СЃС‚РёСЂР°РµС‚Рµ exe СЂСѓРєР°РјРё вЂ” СЃРЅР°С‡Р°Р»Р° СЃРЅРёРјРёС‚Рµ Р°РІС‚РѕР·Р°РїСѓСЃРє.

Р›РѕРі: `vpnfriend.log` СЂСЏРґРѕРј СЃ РїСЂРѕРіСЂР°РјРјРѕР№.

РЎР±РѕСЂРєР°: `Build-VPNfriend.bat` (РґР»СЏ Р°РІС‚РѕСЂР° / СЃ СЂР°Р·СЂРµС€РµРЅРёРµРј).

---

## macOS

macOS 12+. РЈРґРѕР±РЅРµРµ DMG:

1. РћС‚РєСЂРѕР№С‚Рµ [`VPNfriend.dmg`](https://github.com/Denny-Wolkow/VPNfriend-releases/releases/latest/download/VPNfriend.dmg).
2. **РџРµСЂРµС‚Р°С‰РёС‚Рµ `VPNfriend.app` РЅР° РїР°РїРєСѓ В«РџСЂРѕРіСЂР°РјРјС‹В»** РІ РѕРєРЅРµ РґРёСЃРєР°.
3. РР·РІР»РµРєРёС‚Рµ РґРёСЃРє. Р—Р°РїСѓСЃРєР°Р№С‚Рµ РёР· В«РџСЂРѕРіСЂР°РјРјС‹В», РЅРµ СЃ С„Р»РµС€РєРё/DMG.

Р•СЃР»Рё РѕС‚РєСЂС‹Р»Рё СЃ С„Р»РµС€РєРё вЂ” РїСЂРѕРіСЂР°РјРјР° РїСЂРµРґР»РѕР¶РёС‚ СЃРєРѕРїРёСЂРѕРІР°С‚СЊ РІ В«РџСЂРѕРіСЂР°РјРјС‹В» РёР»Рё РѕС‚РєСЂС‹С‚СЊ СѓР¶Рµ СѓСЃС‚Р°РЅРѕРІР»РµРЅРЅСѓСЋ РєРѕРїРёСЋ.

Gatekeeper: РїСЂР°РІС‹Р№ РєР»РёРє в†’ В«РћС‚РєСЂС‹С‚СЊВ».

РќР° Mac вЂ” **РєСЂСѓР¶РѕРє РІ СЃС‚СЂРѕРєРµ РјРµРЅСЋ** (РЅРµ Dock). Р›РµРІС‹Р№ РєР»РёРє вЂ” РєР°СЂС‚РѕС‡РєР°, РїСЂР°РІС‹Р№ вЂ” РјРµРЅСЋ. РћР±С‰РёР№ `utun` Р·Р°СЃС‡РёС‚С‹РІР°РµС‚СЃСЏ С‚РѕР»СЊРєРѕ РїСЂРё Р·Р°РїСѓС‰РµРЅРЅРѕРј РїСЂРѕС†РµСЃСЃРµ РІС‹Р±СЂР°РЅРЅРѕРіРѕ РєР»РёРµРЅС‚Р°. Safari РІС…РѕРґРёС‚ РІ Р±СЂР°СѓР·РµСЂС‹.

РСЃС…РѕРґРЅРёРєРё: [`mac/`](mac/). РЎР±РѕСЂРєР°: [`mac/README.txt`](mac/README.txt).

---

## Р§РµРіРѕ РЅРµС‚

- Р­С‚Рѕ РЅРµ VPN, РЅРµ РєР»РёРµРЅС‚ Рё РЅРµ kill switch.
- Р­С‚Рѕ РЅРµ РїРѕР»РЅС‹Р№ Р°СѓРґРёС‚ DNS / IPv6 / WebRTC РІ Р±СЂР°СѓР·РµСЂРµ (ipleak.net).
- Р­С‚Рѕ РЅРµ РґРѕРєР°Р·Р°С‚РµР»СЊСЃС‚РІРѕ, С‡С‚Рѕ В«РІСЃРµ РїСЂРѕРіСЂР°РјРјС‹ СЃРёСЃС‚РµРјС‹ РІ VPNВ».

---

## Р‘РµР·РѕРїР°СЃРЅРѕСЃС‚СЊ

- Р›РѕРіРёРЅ/РїР°СЂРѕР»СЊ/РєР»СЋС‡ РїСЂРѕРІР°Р№РґРµСЂРѕРІ РІ **РњРѕС‘** вЂ” С‡РµСЂРµР· Р·Р°С‰РёС‚Сѓ РћРЎ (DPAPI / Keychain).
- Р’РєР»Р°РґРєСѓ В«РњРѕС‘В» РјРѕР¶РЅРѕ Р·Р°РєСЂС‹С‚СЊ РїР°СЂРѕР»РµРј.
- РќР° ipleak.net РґР°РЅРЅС‹Рµ РЅРµ РѕС‚РїСЂР°РІР»СЏСЋС‚СЃСЏ вЂ” С‚РѕР»СЊРєРѕ РѕС‚РєСЂС‹РІР°РµС‚СЃСЏ СЃС‚СЂР°РЅРёС†Р° РІ Р±СЂР°СѓР·РµСЂРµ.

---

## РџСЂР°РІРѕРІРѕР№ СЃС‚Р°С‚СѓСЃ

В© 2026 **Denny-Wolkow**. Р’СЃРµ РїСЂР°РІР° Р·Р°С‰РёС‰РµРЅС‹.

РџРѕР»РЅС‹Р№ С‚РµРєСЃС‚: [LICENSE](LICENSE). РџСѓР±Р»РёРєР°С†РёСЏ РЅР° GitHub **РЅРµ** РѕС‚РјРµРЅСЏРµС‚ Р°РІС‚РѕСЂСЃРєРёРµ РїСЂР°РІР°. РљРѕРїРёСЂРѕРІР°РЅРёРµ, РёР·РјРµРЅРµРЅРёРµ Рё СЂР°СЃРїСЂРѕСЃС‚СЂР°РЅРµРЅРёРµ Р±РµР· РїРёСЃСЊРјРµРЅРЅРѕРіРѕ СЂР°Р·СЂРµС€РµРЅРёСЏ Р·Р°РїСЂРµС‰РµРЅС‹. РџРћ РїСЂРµРґРѕСЃС‚Р°РІР»СЏРµС‚СЃСЏ **РєР°Рє РµСЃС‚СЊ**, Р±РµР· РіР°СЂР°РЅС‚РёР№.
