# TrainLoop — Sitemapa

**Stav:** nástřel na hackathon 9. 10. 2026. Čísla `F-xx` odkazují na [feature-breakdown.xlsx](feature-breakdown.xlsx).

![Sitemapa TrainLoop](sitemapa.svg)

## Obrazovky

| Obrazovka | Co na ní je | Features |
| --- | --- | --- |
| **Veřejná část** | Úvod, registrace, přihlášení, obnova hesla, přijetí pozvánky od psovoda | F-01, F-02, F-08 |
| **Týden** (výchozí) | Kalendář aktuálního týdne napříč psy a disciplínami, přepínání týdnů, přesun mezi dny. Z položky jde rovnou zapsat trénink | F-19 – F-24 |
| **Psi** | Seznam mých a nasdílených psů, založení psa | F-04 – F-07 |
| ↳ Detail psa | Aktivní cíle podle disciplín, archiv cílů, kdo má přístup | F-17 |
| ↳ Sdílení s trenéry | Pozvat e-mailem, ukázat kód, odebrat přístup | F-08 – F-10 |
| ↳ Detail cíle (plán) | Cesta úkolů s aktuálním krokem: přidat, vrátit, přeskočit, rozvětvit | F-12 – F-16 |
| **Detail úkolu** | Instrukce, historie tréninků (%, poznámka, video), komentáře psovod ↔ trenér | F-24 – F-26, F-30 |
| **Klienti** (jen trenér) | Psi klientů, připojení psa kódem | F-09, F-31 |
| ↳ Čeká na reakci | Nové záznamy od klientů, na které trenér ještě nereagoval | F-32 |
| **Účet** | Jméno, heslo, smazání účtu | F-01, F-39 |

## Systémové obrazovky a stavy

| Situace | Co uživatel uvidí |
| --- | --- |
| Prázdné stavy (bez psa, bez cílů, prázdný týden, trenér bez klientů) | Výzva k dalšímu kroku: založit psa, cíl, naplánovat trénink, připojit psa kódem |
| Neplatná nebo vypršelá pozvánka / kód | Vysvětlení a co dělat dál |
| Přístup ke psovi byl odebrán | „K tomuto psovi už nemáte přístup“ |
| Nevratná akce (smazání, odebrání přístupu) | Potvrzovací dialog |
| Neexistující stránka, chyba serveru | 404 / chybová obrazovka s možností zkusit znovu |

## Hlavní cesty

1. **Psovod začíná:** Registrace → Nový pes → Detail psa → nový cíl s úkoly → Týden → Naplánovat trénink.
2. **Po tréninku:** Týden → Zapsat trénink (%, poznámka, video).
3. **Propojení:** Detail psa → Sdílení → pozvánka → trenér ji přijme → Klienti.
4. **Trenér reaguje:** Klienti → Čeká na reakci → Detail úkolu → komentář → Detail cíle → upraví další krok.

## K probrání s PO

- Pokud je trenér zvláštní typ účtu (F-01), bude jeho výchozí obrazovkou *Klienti* místo *Týdne*.
- Podoba *Detailu cíle* (seznam, nebo strom) záleží na tom, jak vypadá větvení v praxi (F-15).
