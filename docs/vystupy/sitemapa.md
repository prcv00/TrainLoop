# TrainLoop — Sitemapa

**Stav:** podklad na hackathon 9. 10. 2026, sladěný s [wireframem ve Figmě](https://www.figma.com/design/IjEnmXXeJB8YBOWPjWiFu3/Trainloop-wireframe?node-id=0-1). Čísla `F-xx` odkazují na [feature-breakdown.xlsx](feature-breakdown.xlsx).

**Rozhodnuto:** pozvánku posílá **trenér klientovi**, protože aplikaci platí trenér (F-08). Klient se připojí přes „Mám pozvánku“ na úvodní obrazovce.

![Sitemapa TrainLoop](sitemapa.svg)

## Pojmy

| Pojem | Význam | Příklad |
| --- | --- | --- |
| **Disciplína** | Oblast, ve které pes trénuje | canicross, nosework, poslušnost |
| **Cvik** | Jeden konkrétní krok. V briefu se mu říká „úkol“ | „Běh v plném tahu 400 m“, „oční kontakt“ |
| **Sekvence cviků** | Několik cviků, které jdou vždy po sobě jako jeden blok | rozběh → 3× 400 m → vyklusání |
| **Plán** | Cviky a sekvence seřazené za sebou, případně rozvětvené. Trenér ho skládá pro psa v disciplíně na obrazovce *Tvorba tréninku* | „Trénink pro Rexe“ ve wireframu |
| **Trénink** | Jedno cvičení v konkrétní den v kalendáři. Psovod ho prochází cvik po cviku | „Alík Canicross Trénink“ v pátek |
| **Záznam** | Co psovod po tréninku odešle: video a komentář | |

## Jak vzniká a probíhá trénink

1. **Trenér pozve klienta** (Klienti → Pozvat klienta). Klient na úvodní obrazovce zvolí *Mám pozvánku*, zaregistruje se a založí psa. Pes se trenérovi objeví v *Klientech*.
2. **Trenér složí plán** (Pes → + → *Tvorba tréninku*). Přidává bloky dvou typů, *Jednotlivý cvik* a *Sekvenci cviků*, a spojuje je šipkami. Cesta se může rozdělit na dvě větve a ty se pak znovu spojí. Tlačítko + přidá blok, přetažením do koše se blok smaže.
3. **Trénink se objeví v kalendáři psovoda** (*Týden*). Den má barevné proužky podle psa, po kliknutí na den se zobrazí karta tréninku se seznamem cviků.
4. **Psovod trénuje.** Otevře trénink a prochází cviky jeden po druhém („Aktuální cvik 3/20“, šipky vlevo a vpravo).
5. **Psovod odešle záznam.** Na obrazovce *Konec* nahraje video, napíše komentář a odešle.
6. **Trenér reaguje.** U klienta v *Klientech* svítí štítek „čeká na reakci“. Trenér si záznam prohlédne, odpoví a podle výsledku upraví plán v *Tvorbě tréninku*. Obrazovka pro odpověď ve wireframu zatím chybí.

## Co znamená nelinearita a větvení

**Lineární plán** je jako sešit: cvik 1 → 2 → 3 → 4, vždy ve stejném pořadí.

**Nelineární plán** podle briefu reaguje na to, jak psovi trénink jde. Mění se **v čase, napříč tréninky a týdny**, podle zapsaných výsledků. Na příkladu z briefu (plán „pozornost v silně rušivém prostředí“: oční kontakt → delší podržení → mírné rušivky → silné rušivky):

| Situace | Co se v plánu stane | Feature |
| --- | --- | --- |
| Mírné rušivky psovi nejdou | **Návrat** o krok zpět na delší podržení | F-14 |
| Delší podržení pes už umí | **Přeskočení** rovnou na mírné rušivky | F-14 |
| Skok mezi mírnými a silnými rušivkami je moc velký | **Vložení mezikroku** | F-13 |
| Pes se při rušivkách přetěžuje | **Rozvětvení:** cesta se rozdělí na dvě větve, které se trénují souběžně (např. „pozornost venku“ a „práce s klidem“). Až pes obě zvládne, cesty se znovu spojí | F-15 |

Wireframe kreslí větvení na obrazovce *Tvorba tréninku*. Není ale jasné, jestli tato obrazovka znázorňuje **plán na několik týdnů** (význam z briefu), nebo **jeden trénink** (pak by větev znamenala, že si psovod během tréninku vybere jednu cestu). Na tom závisí datový model, proto je to otázka č. 1.

## Obrazovky

Sloupec *Wireframe* uvádí název rámce ve Figmě, nebo „chybí“, pokud obrazovku je ještě potřeba nakreslit.

| Obrazovka | Wireframe | Co na ní je | Features |
| --- | --- | --- | --- |
| **Úvodní stránka** | Uvodní stránka | Co je TrainLoop, tlačítka *Mám pozvánku*, *Přihlásit se*, *Registrace* | — |
| ↳ Mám pozvánku | chybí | Zadání kódu od trenéra (nebo otevření odkazu z e-mailu), pak registrace a propojení s trenérem | F-08, F-09 |
| ↳ Registrace, Přihlášení, Obnova hesla | chybí | Standardní formuláře | F-01, F-02 |
| **Psi** | Psi | Seznam psů s fotkou, jménem a plemenem. Barevný proužek = barva psa v kalendáři. Tlačítko + přidá psa | F-04, F-06 |
| ↳ Nový pes | chybí | Jméno, plemeno, fotka, disciplíny | F-04, F-05 |
| ↳ **Pes** (detail) | Pes | Fotka, jméno, plemeno a *Aktivity*, tedy tréninky psa po dnech. Tlačítko + vede na *Tvorbu tréninku* | F-07, F-26 |
| ↳ ↳ **Tvorba tréninku** | Tvorba tréninku | Plán z bloků *Jednotlivý cvik* a *Sekvence cviků*, větvení a spojení, + přidat blok, koš smazat | F-12 – F-16 |
| **Týden** | Týden | Výběr týdne, dny Po–Ne s barevnými proužky podle psů. Po kliknutí na den karta tréninku („Alík Canicross Trénink“ a seznam cviků) | F-19 – F-22 |
| ↳ Trénink (průchod) | Trénink | „Aktuální cvik 3/20“, název cviku, šipkami na předchozí a další cvik | F-43 |
| ↳ Trénink (konec) | Trénink | *Nahrát video*, *Komentář*, *Odeslat* | F-24, F-25, F-30 |
| **Klienti** (jen trenér) | Klienti | Karty klientů (jméno, e-mail), štítek „čeká na reakci“ | F-31, F-32 |
| ↳ Pozvat klienta | chybí | E-mail klienta nebo kód / odkaz k předání na lekci | F-08, F-09 |
| ↳ Detail klienta | chybí | Psi klienta (vedou na *Pes*) a záznamy čekající na reakci | F-31, F-32 |
| ↳ Reakce trenéra | chybí | Odeslaný záznam (video, komentář) a odpověď trenéra | F-30 |
| **Profil** | Účet | Jméno, e-mail, změna hesla, odhlásit se, smazat účet | F-01, F-39 |

**Navigace** (spodní lišta ve wireframu): Psi · Týden · Klienti · Profil.

## Hlavní cesty

1. **Trenér začíná:** Registrace → Klienti → Pozvat klienta.
2. **Klient se připojí:** Úvodní stránka → Mám pozvánku → Registrace → Nový pes → pes se trenérovi objeví v Klientech.
3. **Trenér připraví trénink:** Klienti → Detail klienta → Pes → + → Tvorba tréninku.
4. **Psovod trénuje:** Týden → den → Trénink (cvik po cviku) → Konec → video, komentář → Odeslat.
5. **Trenér reaguje:** Klienti („čeká na reakci“) → Detail klienta → Reakce trenéra → případně úprava v Tvorbě tréninku.

## Systémové obrazovky a stavy

| Situace | Co uživatel uvidí |
| --- | --- |
| Prázdné stavy (bez psa, prázdný týden, trenér bez klientů) | Výzva k dalšímu kroku: přidat psa, počkat na trénink od trenéra, pozvat klienta |
| Neplatná nebo vypršelá pozvánka / kód | Vysvětlení a co dělat dál |
| Trenér ukončil spolupráci | „K tomuto psovi už nemáte přístup“ |
| Nevratná akce (smazání bloku, psa, účtu) | Potvrzovací dialog |
| Neexistující stránka, chyba serveru | 404 / chybová obrazovka s možností zkusit znovu |

## Otázky pro PO

Seřazené podle dopadu na datový model a wireframe. U každé je návrh týmu. Další otázky jsou v [otazky-na-klienta.md](otazky-na-klienta.md), odkazy uvádíme.

1. **Co je větvení: plán na několik týdnů, nebo jeden trénink?** Ukažte prosím na příkladu se Zoe, kdy jste naposledy cestu rozdělila. Trénují se pak obě větve souběžně, nebo se podle psa vybere jedna? Spojí se zase? → F-15, viz také otázka 1 v otazky-na-klienta.
   *Návrh:* *Tvorba tréninku* zobrazuje plán na několik týdnů. Obě větve se trénují souběžně a každá má vlastní aktuální cvik.
2. **Chcete u plánu i cíl** (např. „5 km pod 5 min/km“), nebo stačí plán v disciplíně s názvem? → F-12.
   *Návrh:* v MVP stačí název a disciplína, cíl s termínem a kritériem až později.
3. **Stačí po tréninku video a komentář, nebo chcete i % úspěšnosti?** Pokud ano, za každý cvik, nebo za celý trénink? → F-24, F-27, viz také otázka 3.
   *Návrh:* pokud ano, přidat na obrazovku *Konec* jedno pole za celý trénink (% nebo Splněno / Částečně / Nesplněno).
4. **Co udělá tlačítko *Nahrát video*:** nahraje soubor, nebo stačí vložit odkaz (YouTube, Disk)? → F-25, F-28, viz také otázka 5.
   *Návrh:* v MVP odkaz. Nahrávání souborů na náš server je dražší a je mimo rozsah (F-28).
5. **Jak se trénink dostane do kalendáře?** Ve wireframu je „vygenerovaný popis tréninku“. Rozvrhne aplikace cviky z plánu do dnů sama, nebo trenér či psovod zařadí trénink na konkrétní den ručně? → F-20, viz také otázka 4.
   *Návrh:* ručně, trenér nebo psovod vybere den. Automatický rozvrh nechat jako Nice to have.
6. **Má plán upravovat i psovod?** A může psovod aplikaci používat i bez trenéra? → F-16, F-01, viz také otázka 2.
   *Návrh:* plán sestavuje a upravuje trenér, psovod trénuje a posílá záznamy. Psovod bez trenéra je mimo MVP.
7. **Pozvánka od trenéra:** zve trenér člověka, nebo rovnou konkrétního psa? Co když klient už účet má (např. kvůli jinému trenérovi)? Jak dlouho platí kód? → F-08, F-09.
   *Návrh:* trenér zve člověka. Klient po přijetí vybere nebo založí psa. Kód platí 7 dní.
8. **Jak trenér odpovídá a kde odpověď psovod uvidí?** Obrazovku *Reakce trenéra* je potřeba dokreslit. → F-30, viz také otázka 8.
   *Návrh:* vlákno komentářů u odeslaného tréninku. Psovodovi se u tréninku v Týdnu ukáže štítek „nová odpověď“.
9. **Navigace podle role:** vidí psovod záložku *Klienti*? Má trenér i vlastní psy v záložce *Psi*? Která obrazovka je výchozí? → F-01.
   *Návrh:* psovod má Psi · Týden · Profil, trenér navíc Klienti. Trenér začíná na Klientech, psovod na Týdnu.
