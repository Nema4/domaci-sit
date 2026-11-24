# Dokumentace domácí počítačové sítě

**Home Network Infrastructure – analýza, inventarizace a diagnostika**

**Stav:** Verze 1.0 – dokončená základní analýza a dokumentace  
**Datum měření:** 23. 11. 2026  
**Prostředí:** Skutečná domácí síť, Windows a O2 Smart Box 1

## 1. O projektu

Cílem projektu bylo zmapovat a zdokumentovat existující domácí síť, zjistit základní IP konfiguraci a ověřit síťovou konektivitu. Jde o praktický projekt do IT portfolia zaměřený na TCP/IP, DHCP, DNS, diagnostiku a tvorbu technické dokumentace.

**Rozsah verze 1.0:** identifikace hardwaru, inventarizační snímek klientů z routeru, ověřená část logické topologie a čtyři základní diagnostické testy. Detailní fyzická kabeláž a bezpečnostní audit nejsou součástí dokončeného rozsahu.

## 2. Použitá infrastruktura

| Označení | Zařízení | Úloha | Ověření |
|---|---|---|---|
| R01 | O2 Smart Box 1 | Výchozí brána, DHCP, DNS a Wi-Fi | Administrace a nastavení Windows |
| SW01 | D-Link DGS-108 | Neřízený 8portový gigabitový ethernetový switch | Fotografie zařízení |
| PC01 | Počítač s Windows | Testovací zařízení připojené přes Wi-Fi | `ipconfig /all` |

Router má v lokální IPv4 síti adresu `10.0.1.138`. Switch D-Link DGS-108 nemá běžné webové administrační rozhraní ani vlastní správní IP adresu. Přesné kabelové zapojení switche nebylo ověřeno.

## 3. Inventarizace klientů

V administrační části **Device List** bylo zachyceno **9 klientských záznamů**: 5 ve skupině Wi-Fi a 4 ve skupině Ethernet. Jde o stav zobrazený routerem, nikoli zaručeně úplný seznam všech zařízení v domácnosti.

| ID | Typ / popis podle routeru | Skupina | IPv4 |
|---|---|---|---|
| MOB01 | Android telefon | Wi-Fi | Nezjištěna |
| MOB02 | Android telefon | Wi-Fi | Nezjištěna |
| MOB03 | Android zařízení | Wi-Fi | Nezjištěna |
| MOB04 | Android / Motorola | Wi-Fi | Nezjištěna |
| PC01 | Testovací počítač Windows | Wi-Fi | `10.0.1.77` |
| TV01 | Android TV | Ethernet | Nezjištěna |
| PC02 | Počítač | Ethernet | Nezjištěna |
| PC03 | Počítač | Ethernet | Nezjištěna |
| DEV01 | Klient označený Android-2 | Ethernet | Nezjištěna |

V mapě routeru byly navíc zobrazeny telefonní porty **FXS1** a **FXS2**; ty se nepočítají jako klientská zařízení. Dřívější mapa obsahovala i iPhone, který v následném seznamu chyběl. Není potvrzeno, zda byl odpojený, evidovaný pod jiným názvem, nebo šlo o historický záznam.

## 4. Logická topologie

![Logická topologie domácí sítě](obrazky/topologie.png)

Diagram zobrazuje **ověřenou část logické topologie**. Přerušovaná vazba u D-Link switche vyjadřuje neověřené fyzické zapojení, nikoli potvrzený kabelový spoj. Internetová přípojka a skutečné zapojení portů nebyly podrobně mapovány.

## 5. IP adresace a síťové služby

Konfigurace PC01 byla získána příkazem `ipconfig /all`.

| Parametr | Zjištěná hodnota |
|---|---|
| IPv4 adresa PC01 | `10.0.1.77` |
| Maska | `255.255.255.0` |
| Podsíť | `10.0.1.0/24` |
| Adresa sítě | `10.0.1.0` |
| Broadcast | `10.0.1.255` |
| Rozsah použitelných adres | `10.0.1.1–10.0.1.254` |
| Výchozí IPv4 brána | `10.0.1.138` |
| DHCP server | `10.0.1.138` |
| IPv4 DNS server | `10.0.1.138` |
| DNS suffix | `home` |
| Typ připojení | Wi-Fi |
| Bezdrátový adaptér | Realtek 8852BE Wi-Fi 6 |

**DHCP:** Počítač má automatické přidělování IPv4 konfigurace zapnuté a používá DHCP server routeru. Skutečný DHCP pool (rozsah pronajímaných adres) nebyl ověřen.

**DNS:** Router je nastaven jako IPv4 DNS server počítače. Při testu `nslookup` počítač komunikoval s DNS serverem `internet.o2` přes IPv6 a získal IPv4 i IPv6 odpovědi.

**IPv6:** Na PC jsou aktivní globální, dočasné i link-local IPv6 adresy. Konkrétní globální adresy v dokumentaci nejsou uvedeny.

## 6. Diagnostika a výsledky

Testy byly provedeny z PC01 v příkazovém řádku Windows dne 23. 11. 2026.

| Test | Příkaz | Naměřený výsledek | Hodnocení |
|---|---|---|---|
| Spojení s routerem | `ping 10.0.1.138` | 4/4 odpovědí, 0 % ztráta, průměr 4 ms | PASS |
| Spojení s veřejnou IPv4 | `ping -4 1.1.1.1` | 4/4 odpovědí, 0 % ztráta, průměr 17 ms | PASS |
| Překlad DNS | `nslookup seznam.cz` | Vráceny záznamy A i AAAA | PASS |
| Trasa k cíli | `tracert -4 1.1.1.1` | Cíl dosažen na 11. skoku | PASS |

### 6.1 Ping na router

![Výsledek ping na router](obrazky/ping-router.png)

Rozsah odezvy byl 3–6 ms. Test potvrdil funkční komunikaci s výchozí bránou v době měření.

### 6.2 Ping na veřejnou IPv4 adresu

![Výsledek ping na internet](obrazky/ping-internet.png)

Rozsah odezvy byl 17–18 ms. Test potvrdil dostupnost cíle `1.1.1.1`, nikoli kvalitu nebo dostupnost celého internetu.

### 6.3 DNS překlad

![Výsledek DNS testu](obrazky/dns-test.png)

Doména `seznam.cz` byla úspěšně přeložena. Adresa domácího IPv6 DNS resolveru je na veřejném snímku anonymizována.

### 6.4 Traceroute

![Výsledek traceroute](obrazky/traceroute.png)

První skok byl domácí router `10.0.1.138`, druhý skok privátní adresa `10.10.10.1` a jedenáctý skok cílová adresa `1.1.1.1`. Některé mezilehlé uzly neodpovídaly na diagnostické pakety; vzhledem k dosažení cíle to samo o sobě neprokazuje poruchu.

**Omezení měření:** Čtyři pakety při ping testu představují pouze krátký orientační test. Nebyla měřena dlouhodobá stabilita, propustnost, rychlost Wi-Fi ani bezpečnost celé sítě.

## 7. Bezpečnost a omezení analýzy

V rámci této verze nebyly prováděny změny v routeru, audit firewallu ani ověření konfigurace zabezpečení Wi-Fi. Proto nelze tvrdit, že je síť bezpečnostně prověřená.

Při zveřejnění byly z dokumentace vynechány přístupové údaje, MAC adresy, identifikátory rodinných příslušníků a globální IPv6 adresy domácích zařízení. Privátní IPv4 adresy jsou uvedeny pro vysvětlení sítě.

Další omezení: neověřené fyzické vedení kabelů, neznámý DHCP pool, neúplná inventarizace všech zařízení a neověřený typ internetové přípojky.

## 8. Doporučení pro další rozvoj

1. Ověřit skutečné kabelové propojení Smart Boxu, D-Link switche a ethernetových zásuvek.
2. Zkontrolovat zabezpečení Wi-Fi, aktualizace routeru, vzdálenou administraci a hostovskou síť.
3. Zjistit rozsah DHCP a případné rezervace IP adres.
4. Průběžně aktualizovat seznam aktivních klientů.
5. V samostatné laboratoři vyzkoušet monitoring, firewall a segmentaci pomocí VLAN na zařízení, které tyto funkce podporuje.

Tyto body představují **návrhy**, nikoli realizované změny.

## 9. Stav projektu

**Verze 1.0 – dokončeno:**

- [x] Identifikace hlavního routeru a switche
- [x] Inventarizační snímek klientů z Device List
- [x] Analýza IPv4 konfigurace a základních síťových služeb
- [x] Ověření komunikace s routerem a externím cílem
- [x] Test DNS a analýza trasy paketů
- [x] Dokumentace výsledků včetně screenshotů
- [x] Diagram ověřené části logické topologie

**Možná navazující verze 2.0:**

- [ ] Kompletní fyzická topologie a identifikace portů
- [ ] Kompletní přehled aktivních zařízení a jejich adres
- [ ] Bezpečnostní kontrola Wi-Fi a routeru
- [ ] Monitoring, případně samostatná VLAN laboratoř

## 10. Závěr

Podařilo se zdokumentovat základní infrastrukturu domácí sítě, určit IP konfiguraci testovacího počítače a úspěšně provést čtyři základní diagnostické testy. Práce ukázala význam ověřování informací z více zdrojů: seznam zařízení v routeru nemusí být úplný a dosažení cíle při traceroute nevylučuje chybějící odpovědi mezilehlých uzlů.

Prakticky jsem si procvičil práci s webovou administrací routeru, IPv4 adresací, DHCP, DNS, příkazy `ipconfig`, `ping`, `nslookup`, `tracert` a dokumentováním technických výsledků na GitHubu.

**Základní analýza a diagnostika (verze 1.0) jsou dokončeny.** Pokročilé zabezpečení a úplné fyzické mapování jsou vymezeny jako další fáze, nikoli jako již provedené činnosti.
