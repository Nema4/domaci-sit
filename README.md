# Dokumentace domácí počítačové sítě

**Home Network Infrastructure – Analysis, Documentation & Troubleshooting**

**Stav projektu:** Probíhá analýza a dokumentace  
**Datum zahájení:** 23. 11. 2026  
**Prostředí:** Reálná domácí síť

---

## 1. Úvod projektu

Tento projekt se zaměřuje na analýzu, dokumentaci, diagnostiku a vyhodnocení zabezpečení existující domácí počítačové sítě.

Domácí síť využívá internetové připojení od poskytovatele O2 a zahrnuje router, ethernetový switch, počítače, mobilní telefony, televizní zařízení a další síťové klienty.

Projekt vytvářím za účelem získání praktických zkušeností s počítačovými sítěmi a jejich správou. Je součástí mého IT portfolia pro budoucí uplatnění v oblasti IT infrastruktury, technické podpory a síťové administrace.

### 1.1 Cíle projektu

- Identifikovat používanou síťovou infrastrukturu.
- Zmapovat fyzické a logické uspořádání sítě.
- Provést inventarizaci síťových zařízení.
- Analyzovat IPv4 a IPv6 konfiguraci.
- Porozumět fungování DHCP a DNS v domácí síti.
- Ověřit dostupnost lokální sítě a internetu.
- Provést základní síťovou diagnostiku.
- Zkontrolovat zabezpečení domácí sítě.
- Navrhnout možná zlepšení infrastruktury.
- Vytvořit přehlednou technickou dokumentaci.

---

## 2. Popis současné domácí sítě

Domácí síť je postavena na routeru O2 Smart Box první generace.

Router zajišťuje přístup k internetu, směrování síťové komunikace, automatické přidělování IPv4 konfigurace prostřednictvím DHCP a DNS služby pro koncová zařízení.

Součástí infrastruktury je také osmipo rtový gigabitový ethernetový switch D-Link DGS-108, který slouží k rozšíření počtu dostupných ethernetových portů.

Koncová zařízení využívají dva způsoby připojení:

- **Wi-Fi:** Mobilní telefony, počítače a další bezdrátová zařízení.
- **Ethernet:** Počítače, televizní zařízení a další kabeloví klienti.

Přesné fyzické propojení routeru, switche a jednotlivých zařízení bude ověřeno v další fázi projektu.

### 2.1 Základní informace o síti

| Parametr | Hodnota |
|---|---|
| Poskytovatel internetu | O2 |
| Hlavní router | O2 Smart Box 1 |
| Ethernetový switch | D-Link DGS-108 |
| Lokální IPv4 síť | 10.0.1.0/24 |
| Výchozí IPv4 brána | 10.0.1.138 |
| DHCP server | 10.0.1.138 |
| IPv4 DNS server | 10.0.1.138 |
| IPv6 | Aktivní na testovacím PC |
| Typ internetové přípojky | Zatím neověřeno |

---

## 3. Použitý síťový hardware

### 3.1 Router – O2 Smart Box 1

O2 Smart Box 1 představuje hlavní síťové zařízení domácnosti.

Zjištěné funkce:

- Výchozí IPv4 brána
- DHCP server
- DNS resolver pro klienty
- Směrování komunikace
- Bezdrátový přístupový bod
- Ethernetové připojení zařízení
- Webové administrační rozhraní

**IPv4 adresa routeru:** `10.0.1.138`

Router poskytuje webovou administraci, ve které lze zobrazit mapu sítě, seznam zařízení a další konfigurační informace.

### 3.2 Ethernetový switch – D-Link DGS-108

Součástí domácí infrastruktury je switch D-Link DGS-108.

Základní vlastnosti:

- 8 ethernetových portů
- Podpora rychlostí 10/100/1000 Mb/s
- Neřízený switch
- Přepínání ethernetových rámců na 2. vrstvě OSI modelu
- Rozšíření kabelové konektivity domácí sítě

Tento model nemá běžné webové administrační rozhraní a nevyžaduje vlastní správní IP adresu.

Přesné zapojení jeho portů bude zdokumentováno při mapování fyzické topologie.

### 3.3 Testovací počítač

K diagnostice je používán počítač s operačním systémem Windows.

| Parametr | Hodnota |
|---|---|
| Identifikátor | PC01 |
| Operační systém | Windows |
| Síťový adaptér | Realtek 8852BE Wireless LAN Wi-Fi 6 PCI-E NIC |
| Způsob připojení | Wi-Fi |
| IPv4 adresa | 10.0.1.77 |
| DHCP | Povoleno |

Pro testování byly využity příkazy `ipconfig`, `ping`, `nslookup` a `tracert`.

---

## 4. Inventarizace síťových zařízení

### 4.1 Cíl inventarizace

Cílem inventarizace je identifikovat zařízení připojená do domácí sítě, určit jejich funkci, způsob připojení a dostupnou IP konfiguraci.

Data byla získána pomocí:

- Webové administrace O2 Smart Boxu
- Funkce Device Map
- Funkce Device List
- Fyzické kontroly síťového hardwaru
- Diagnostických nástrojů Windows

### 4.2 Síťová infrastruktura

| ID | Zařízení | IPv4 adresa | Funkce |
|---|---|---|---|
| R01 | O2 Smart Box 1 | 10.0.1.138 | Router, DHCP, DNS |
| SW01 | D-Link DGS-108 | Bez správní IP | Ethernetový switch |
| PC01 | Testovací Windows PC | 10.0.1.77 | Diagnostika sítě |

### 4.3 Klientská zařízení podle O2 Smart Boxu

V okamžiku kontroly zobrazovalo rozhraní Device List celkem 9 klientských záznamů.

#### Wi-Fi klienti

| ID | Typ zařízení | Připojení | IPv4 |
|---|---|---|---|
| MOB01 | Android telefon | Wi-Fi | Nezjištěno |
| MOB02 | Android telefon | Wi-Fi | Nezjištěno |
| MOB03 | Android telefon | Wi-Fi | Nezjištěno |
| MOB04 | Android / Motorola | Wi-Fi | Nezjištěno |
| PC01 | Windows PC | Wi-Fi | 10.0.1.77 |

**Počet zobrazených Wi-Fi klientů: 5**

#### Ethernet klienti

| ID | Typ zařízení | Připojení | IPv4 |
|---|---|---|---|
| TV01 | Android TV | Ethernet | Nezjištěno |
| PC02 | Počítač | Ethernet | Nezjištěno |
| PC03 | Počítač | Ethernet | Nezjištěno |
| DEV01 | Neidentifikovaný Android klient | Ethernet | Nezjištěno |

**Počet zobrazených ethernetových klientů: 4**

### 4.4 Telefonní rozhraní

Router dále zobrazuje rozhraní:

- FXS1
- FXS2

Tato rozhraní slouží pro telefonní služby a nejsou započítána mezi běžné síťové klienty.

### 4.5 Zjištěné nesrovnalosti

Při porovnání funkcí Device Map a Device List bylo zjištěno, že seznamy zařízení se nemusí zcela shodovat.

Například zařízení typu iPhone bylo viditelné ve starším zobrazení mapy, ale v následném seznamu Device List nebylo uvedeno.

Možné příčiny:

- Zařízení nebylo aktuálně připojené.
- Router zobrazoval historický záznam.
- Zařízení používá privátní Wi-Fi MAC adresu.
- Zařízení je evidováno pod jiným názvem.

Přesná příčina zatím nebyla ověřena.

### 4.6 Závěr inventarizace

Byla identifikována základní síťová infrastruktura a získán seznam devíti klientských záznamů.

Inventarizace však zatím není úplná.

Zbývá ověřit lokální IPv4 adresy klientů, jejich aktuální stav a případná další zařízení nezobrazená v seznamu.

---

## 5. IP adresace a síťová konfigurace

### 5.1 IPv4 konfigurace

Konfigurace testovacího počítače byla získána příkazem:

`ipconfig /all`

| Parametr | Hodnota |
|---|---|
| IPv4 adresa PC | 10.0.1.77 |
| Maska podsítě | 255.255.255.0 |
| Prefix sítě | /24 |
| Síťová adresa | 10.0.1.0 |
| Broadcast adresa | 10.0.1.255 |
| Výchozí brána | 10.0.1.138 |
| DHCP server | 10.0.1.138 |
| IPv4 DNS server | 10.0.1.138 |
| DNS suffix | home |

Podsíť `10.0.1.0/24` obsahuje 256 IPv4 adres.

Z tohoto počtu je 254 adres použitelných pro síťová rozhraní.

Rozsah použitelných adres:

`10.0.1.1 – 10.0.1.254`

Tento rozsah neznamená, že jsou všechny adresy zahrnuty do DHCP poolu.

### 5.2 DHCP

Testovací počítač má aktivní automatické získávání IP adresy.

DHCP server na adrese `10.0.1.138` klientovi poskytl IPv4 konfiguraci.

DHCP umožňuje automatické přidělování síťových parametrů bez nutnosti ruční konfigurace každého zařízení.

Přesný DHCP pool a případné rezervace adres zatím nebyly ověřeny.

### 5.3 DNS

Testovací počítač využívá router jako IPv4 DNS server.

Funkčnost DNS byla ověřena příkazem:

`nslookup seznam.cz`

Výsledek potvrdil úspěšný překlad doménového jména na IPv4 a IPv6 adresy.

### 5.4 IPv6

Na testovacím počítači je aktivní IPv6.

Byly identifikovány:

- Globální IPv6 adresa
- Dočasné IPv6 adresy
- Link-local IPv6 adresa
- IPv6 výchozí brána
- IPv6 DNS server

Konkrétní veřejně směrovatelné IPv6 adresy nejsou z bezpečnostních důvodů zveřejněny.

---

## 6. Diagnostika a testování sítě

**Datum testování:** 23. 11. 2026  
**Testovací zařízení:** PC01  
**Prostředí:** Windows CMD

### 6.1 Test komunikace s routerem

**Příkaz:** `ping 10.0.1.138`

Výsledky:

- Odesláno: 4 pakety
- Přijato: 4 pakety
- Ztráta paketů: 0 %
- Minimální odezva: 3 ms
- Maximální odezva: 6 ms
- Průměrná odezva: 4 ms

**Výsledek: PASS**

Počítač úspěšně komunikuje s výchozí bránou.

### 6.2 Test internetové konektivity

**Příkaz:** `ping -4 1.1.1.1`

Výsledky:

- Odesláno: 4 pakety
- Přijato: 4 pakety
- Ztráta paketů: 0 %
- Minimální odezva: 17 ms
- Maximální odezva: 18 ms
- Průměrná odezva: 17 ms

**Výsledek: PASS**

Byla potvrzena dostupnost externí IPv4 adresy.

### 6.3 DNS test

**Příkaz:** `nslookup seznam.cz`

Výsledky:

- DNS server odpověděl.
- Byly vráceny IPv4 adresy.
- Byly vráceny IPv6 adresy.
- DNS překlad proběhl úspěšně.

**Výsledek: PASS**

### 6.4 Analýza trasy

**Příkaz:** `tracert -4 1.1.1.1`

Výsledky:

| Skok | Adresa | Poznámka |
|---|---|---|
| 1 | 10.0.1.138 | O2 Smart Box |
| 2 | 10.10.10.1 | Privátní síťový uzel |
| 3 | Bez odpovědi | Timeout |
| 4 | 90.183.197.126 | Síťový uzel |
| 8 | 154.54.78.65 | Mezilehlý směrovač |
| 11 | 1.1.1.1 | Cílová adresa |

Některé mezilehlé uzly neodpověděly na testovací pakety.

Cílová adresa však byla úspěšně dosažena.

**Výsledek: PASS**

### 6.5 Souhrn diagnostiky

| Test | Výsledek |
|---|---|
| Ping na router | PASS |
| Ping na externí IPv4 adresu | PASS |
| DNS překlad | PASS |
| Traceroute | PASS |

Všechny čtyři základní diagnostické testy proběhly úspěšně.

Testování potvrzuje funkčnost vybraných síťových služeb v okamžiku měření. Nejedná se o dlouhodobou analýzu stability ani bezpečnosti.

---

## 7. Síťová topologie

### 7.1 Logická topologie

Dosud potvrzená část sítě:

```text
Internet
   |
O2 Smart Box 1
10.0.1.138
   |
Wi-Fi
   |
Testovací Windows PC
10.0.1.77/24
```

Další známé komponenty:

- D-Link DGS-108
- Další ethernetoví klienti
- Další Wi-Fi klienti
- Telefonní rozhraní FXS1 a FXS2

### 7.2 Fyzická topologie

Fyzická topologie zatím nebyla kompletně ověřena.

Bude doplněna po identifikaci propojení mezi routerem, switchem, ethernetovými zásuvkami a klientskými zařízeními.

---

## 8. Zabezpečení domácí sítě

Bezpečnostní analýza je plánována jako samostatná část projektu.

Kontrolované oblasti:

- Zabezpečení Wi-Fi
- Použité šifrování
- Administrátorský přístup
- Firewall
- Aktualizace firmwaru
- Hostovská Wi-Fi
- Nepotřebné síťové služby
- Oddělení zařízení
- Bezpečnost přístupových údajů

**Stav:** Zatím neprovedeno.

---

## 9. Návrhy na optimalizaci

Po dokončení analýzy budou vyhodnoceny možnosti zlepšení domácí sítě.

Předběžně zvažované oblasti:

- Zlepšení pokrytí Wi-Fi
- Oddělení hostovských zařízení
- Monitoring dostupnosti
- Přehlednější inventarizace zařízení
- Zlepšení zabezpečení administrace
- Případné využití spravovatelného switche
- Možné rozšíření o VLAN

Žádné z těchto vylepšení zatím nebylo realizováno.

---

## 10. Stav projektu

### Dokončené úkoly

- [x] Identifikace hlavního routeru
- [x] Identifikace ethernetového switche
- [x] Zjištění IPv4 konfigurace testovacího PC
- [x] Ověření DHCP konfigurace klienta
- [x] Test DNS
- [x] Ping na router
- [x] Ping na externí IPv4 adresu
- [x] Traceroute do internetu
- [x] První záznam klientů z Device List

### Rozpracované úkoly

- [ ] Kompletní inventarizace všech zařízení
- [ ] Ověření IP adres dalších klientů
- [ ] Fyzická topologie
- [ ] Kompletní logická topologie
- [ ] Kontrola DHCP poolu
- [ ] Analýza Wi-Fi konfigurace
- [ ] Bezpečnostní analýza
- [ ] Návrh optimalizace
- [ ] Závěrečné vyhodnocení

---

## 11. Závěr

V první fázi projektu byla identifikována základní síťová infrastruktura, provedena analýza IP konfigurace a úspěšně dokončeny základní diagnostické testy.

Dále byl získán první přehled klientských zařízení připojených přes Wi-Fi a Ethernet.

Následující fáze projektu budou zaměřeny na dokončení inventarizace, vytvoření topologie a kontrolu zabezpečení domácí sítě.

---

## 12. Bezpečnost dokumentace

Z důvodu ochrany soukromí a bezpečnosti domácí infrastruktury nejsou zveřejňovány:

- Hesla a přístupové údaje
- MAC adresy
- Globální IPv6 adresy domácích zařízení
- Osobní názvy klientských zařízení
- Úplné zálohy konfigurace routeru

Dokumentace používá anonymizované identifikátory zařízení a obsahuje pouze informace relevantní pro technickou analýzu.
