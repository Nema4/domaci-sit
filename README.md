# Dokumentace domácí počítačové sítě

**Home Network Infrastructure – Analysis, Documentation & Troubleshooting**

## 1. Úvod projektu

Tento projekt se zaměřuje na analýzu, dokumentaci a diagnostiku existující domácí počítačové sítě využívající internetové připojení od poskytovatele O2.

Projekt vznikl za účelem získání praktických zkušeností v oblasti počítačových sítí a síťové administrace.

V průběhu projektu budu analyzovat síťovou infrastrukturu, identifikovat jednotlivá zařízení, dokumentovat IP adresaci, testovat konektivitu, kontrolovat zabezpečení a navrhovat možná vylepšení.

Projekt je součástí mého IT portfolia.

### Hlavní cíle

- Zmapovat existující domácí síťovou infrastrukturu.
- Identifikovat síťová a koncová zařízení.
- Vytvořit fyzickou a logickou topologii.
- Zdokumentovat IPv4 a IPv6 konfiguraci.
- Porozumět fungování DHCP a DNS.
- Provést základní diagnostiku sítě.
- Analyzovat zabezpečení síťové infrastruktury.
- Navrhnout případná zlepšení.

---

## 2. Popis současné domácí sítě

Domácí síť využívá router O2 Smart Box první generace, který zajišťuje základní síťové služby a připojení domácích zařízení k internetu.

Součástí infrastruktury je také osmipo rtový gigabitový ethernetový switch D-Link DGS-108.

Do domácí sítě jsou připojována zařízení prostřednictvím bezdrátové Wi-Fi a kabelového ethernetového připojení.

### Základní parametry

| Parametr | Hodnota |
|---|---|
| Poskytovatel internetu | O2 |
| Hlavní router | O2 Smart Box 1 |
| Switch | D-Link DGS-108 |
| IPv4 síť | 10.0.1.0/24 |
| Výchozí IPv4 brána | 10.0.1.138 |
| DHCP | Aktivní |
| IPv4 DNS server | 10.0.1.138 |
| IPv6 | Aktivní |
| Typ internetové přípojky | Bude ověřeno |

Přesné fyzické zapojení všech zařízení a kompletní seznam klientů budou doplněny během inventarizace.

---

## 3. Použitý síťový hardware

### 3.1 O2 Smart Box 1

O2 Smart Box 1 je hlavní síťové zařízení domácnosti.

V rámci současné konfigurace plní několik důležitých funkcí:

- Výchozí brána pro lokální síť
- Směrování komunikace do internetu
- DHCP server pro automatické přidělování IPv4 adres
- DNS resolver pro klientská zařízení
- Bezdrátový přístupový bod Wi-Fi
- Ethernetové připojení lokálních zařízení

**Zjištěná IP adresa routeru:** `10.0.1.138`

### 3.2 D-Link DGS-108

D-Link DGS-108 je osmipo rtový gigabitový neřízený ethernetový switch.

Jeho účelem je rozšíření počtu dostupných ethernetových portů v lokální síti.

Základní charakteristika:

- 8 ethernetových portů
- Přenosová rychlost až 1 Gbit/s na port
- Neřízený switch
- Automatické učení MAC adres
- Přepínání ethernetových rámců na 2. vrstvě modelu OSI

Přesná role switche v domácím zapojení bude ověřena při tvorbě fyzické topologie.

### 3.3 Testovací počítač

Pro diagnostiku sítě je využíván počítač s operačním systémem Windows.

**Síťový adaptér:** Realtek 8852BE Wireless LAN Wi-Fi 6 PCI-E NIC

**Aktuální typ připojení:** Wi-Fi

Testovací zařízení je využíváno pro analýzu TCP/IP konfigurace, DNS, dostupnosti zařízení a směrování paketů.

---

## 4. Síťová topologie

Cílem této části je vytvořit dva síťové diagramy.

### Fyzická topologie

Bude zobrazovat skutečné propojení síťových zařízení pomocí ethernetových kabelů a bezdrátového připojení.

### Logická topologie

Bude zobrazovat IP adresaci, síťové segmenty, výchozí bránu a základní komunikaci mezi zařízeními.

**Stav:** Probíhá mapování sítě.

---

## 5. IP adresace

### 5.1 IPv4 konfigurace

Konfigurace byla zjištěna pomocí příkazu:

`ipconfig /all`

| Parametr | Hodnota |
|---|---|
| IPv4 adresa PC | 10.0.1.77 |
| Maska podsítě | 255.255.255.0 |
| Prefix | /24 |
| Adresa sítě | 10.0.1.0 |
| Broadcast | 10.0.1.255 |
| Výchozí brána | 10.0.1.138 |
| DHCP server | 10.0.1.138 |
| IPv4 DNS server | 10.0.1.138 |

Podsíť `10.0.1.0/24` obsahuje 256 IPv4 adres, z nichž 254 je použitelných pro síťová rozhraní.

### 5.2 DHCP

Pro automatické přidělování IPv4 konfigurace je využíván DHCP server na routeru O2 Smart Box.

Testovací počítač má zapnuté automatické získávání IP adresy.

DHCP umožňuje klientským zařízením získat potřebné síťové parametry bez ruční konfigurace.

Přesný rozsah DHCP přidělování bude ještě ověřen v administraci routeru.

### 5.3 DNS

Testovací počítač využívá jako IPv4 DNS server adresu `10.0.1.138`.

DNS umožňuje překlad doménových jmen na IP adresy.

Funkčnost služby byla ověřena pomocí příkazu:

`nslookup seznam.cz`

Výsledkem byl úspěšný překlad doménového jména na IPv4 i IPv6 adresy.

### 5.4 IPv6

Testovací počítač má aktivní IPv6 konektivitu a přidělené globální i link-local IPv6 adresy.

Z bezpečnostních důvodů nejsou v dokumentaci zveřejněny konkrétní globální IPv6 adresy.

---

## 6. Diagnostika a testování sítě

Diagnostika byla provedena v prostředí Windows pomocí příkazového řádku.

### Test 1 – Dostupnost routeru

**Příkaz:** `ping 10.0.1.138`

Výsledek:

- Odesláno: 4 pakety
- Přijato: 4 pakety
- Ztráta: 0 %
- Průměrná odezva: 4 ms

**Stav: PASS**

### Test 2 – Dostupnost internetu

**Příkaz:** `ping -4 1.1.1.1`

Výsledek:

- Odesláno: 4 pakety
- Přijato: 4 pakety
- Ztráta: 0 %
- Průměrná odezva: 17 ms

**Stav: PASS**

### Test 3 – DNS překlad

**Příkaz:** `nslookup seznam.cz`

Výsledek:

- DNS server odpověděl.
- Překlad doménového jména proběhl úspěšně.
- Byly vráceny IPv4 i IPv6 adresy.

**Stav: PASS**

### Test 4 – Analýza trasy

**Příkaz:** `tracert -4 1.1.1.1`

Výsledek:

- První směrovač: 10.0.1.138
- Druhý směrovač: 10.10.10.1
- Cílová adresa: 1.1.1.1
- Cíl dosažen na 11. skoku

**Stav: PASS**

### Vyhodnocení diagnostiky

Všechny čtyři základní diagnostické testy byly úspěšné.

Byla potvrzena funkční komunikace s routerem, konektivita k externí IPv4 adrese a správná funkce DNS překladu.

Výsledky představují pouze stav v okamžiku testování, nikoliv dlouhodobé měření stability sítě.

---

## 7. Bezpečnost domácí sítě

V další fázi bude provedena základní bezpečnostní analýza.

Plánované oblasti kontroly:

- Zabezpečení bezdrátové sítě
- Používaný typ Wi-Fi šifrování
- Zabezpečení administrace routeru
- Nastavení firewallu
- Dostupnost aktualizací firmwaru
- Oddělení hostovských zařízení
- Kontrola nepotřebných služeb

**Stav:** Zatím neprovedeno.

---

## 8. Návrhy na optimalizaci

Po dokončení analýzy budou vyhodnoceny možnosti zlepšení infrastruktury.

Možné oblasti:

- Optimalizace rozmístění Wi-Fi zařízení
- Zlepšení zabezpečení
- Přehlednější správa síťových zařízení
- Oddělení hostovské sítě
- Zavedení monitoringu dostupnosti
- Možné rozšíření pomocí spravovatelného switche a VLAN

Tyto návrhy zatím nepředstavují provedené změny.

---

## 9. Postup projektu

- [x] Identifikace hlavního routeru
- [x] Identifikace síťového switche
- [x] Zjištění IPv4 konfigurace
- [x] Analýza základní DHCP konfigurace klienta
- [x] Ověření DNS
- [x] Test konektivity s routerem
- [x] Test internetové konektivity
- [x] Analýza trasy paketů
- [ ] Kompletní seznam síťových zařízení
- [ ] Fyzická topologie
- [ ] Logická topologie
- [ ] Kontrola Wi-Fi konfigurace
- [ ] Bezpečnostní analýza
- [ ] Návrh optimalizace
- [ ] Závěrečné vyhodnocení

---

## 10. Závěr

Projekt dokumentuje skutečnou domácí síť a její postupnou analýzu z pohledu začínajícího síťového administrátora.

Dosavadní práce zahrnuje identifikaci základního hardwaru, analýzu TCP/IP konfigurace a diagnostiku síťové komunikace.

Projekt bude postupně rozšiřován o kompletní topologii, inventarizaci zařízení, bezpečnostní kontrolu a návrhy zlepšení infrastruktury.

---

**Poznámka k bezpečnosti:** Identifikační údaje zařízení a citlivé informace o domácí síti nejsou zveřejněny nebo jsou anonymizovány.
