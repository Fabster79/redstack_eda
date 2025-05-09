
>Prompt: Bitte lies das Dataset. Trennzeichen ist ;


Das Dataset wurde erfolgreich eingelesen. Es enthält 29 Spalten, darunter Informationen wie:

 
- `ID`, `Year_Birth`, `Education`, `Marital_Status`, `Income`, `Kidhome`, `Teenhome`
 
- `Dt_Customer` (Datum des ersten Kaufs), `Recency` (Tage seit letztem Kauf)
 
- Ausgaben in verschiedenen Kategorien (`MntWines`, `MntFruits`, etc.)
 
- Kanalnutzung (`NumDealsPurchases`, `NumWebVisitsMonth`, etc.)
 
- Kampagnenreaktionen (`AcceptedCmp1` bis `AcceptedCmp5`, `Response`)
 
- `Complain`, `Z_CostContact`, `Z_Revenue`

Möchtest du eine bestimmte Analyse oder Visualisierung basierend auf diesem Datensatz?

>Prompt: Wie beurteilst Du die Qualität des Datasets?


**Datenqualitätsübersicht**

| |Datentyp | Fehlende Werte | Anzahl eindeutiger Werte |
| --- | --- | --- | --- |
| ID | int64 | 0 | 2240 |
| Year_Birth | int64 | 0 | 59 |
| Education | object | 0 | 5 |
| Marital_Status | object | 0 | 8 |
| Income | float64 | 24 | 1974 |
| Kidhome | int64 | 0 | 3 |


Hier siehst du eine Übersicht über die Datenqualität. Die Tabelle zeigt dir die Datentypen, die Anzahl fehlender Werte sowie die Anzahl eindeutiger Werte pro Spalte. So kannst du schnell erkennen, welche Spalten auffällig sind – zum Beispiel hat die Spalte `Income` fehlende Werte. Möchtest du eine genauere Bewertung oder Vorschläge zur Bereinigung?

>Prompt: Gibt es ungewöhnliche Ausprägungen oder Ausreißer? Beachte die Spalten 1-5.


<img src="https://raw.githubusercontent.com/Fabster79/redstack_eda/refs/heads/main/Images/1.0%20Ausrei%C3%9Fer.png" alt="Bild ausgeben" width="1200">


Ja, es gibt einige ungewöhnliche Ausprägungen und mögliche Ausreißer in den Spalten 1 bis 5:

 
1. **ID** : Werte reichen von 0 bis 11191. Der Wert 0 könnte ein Fehler sein, falls IDs bei 1 beginnen sollten.
 
2. **Year_Birth** :
 
  - Der früheste Jahrgang ist 1893, was sehr alt wäre (über 100 Jahre alt).
 
  - Möglicher Ausreißer: Geburtsjahre < 1920 sollten geprüft werden.
 
3. **Income** :
 
  - Es gibt einen extremen Ausreißer mit 666.666, der stark vom Median (~51.000) abweicht.
 
  - Dieser Wert ist wahrscheinlich ein fehlerhaft eingetragener oder künstlicher Extremwert.
 
  - Zudem fehlen 24 Werte (NaNs).
 
4. **Education** :
 
  - Die Kategorien sind grundsätzlich plausibel.
 
  - Möglicherweise Redundanz zwischen "2n Cycle" und anderen Stufen wie Master.
 
5. **Marital_Status** :
 
  - Es tauchen ungewöhnliche Einträge wie „YOLO“, „Absurd“ und „Alone“ auf – vermutlich Testeinträge oder Eingabefehler.
 
  - Diese sollten bereinigt oder gruppiert werden.

Möchtest du eine Empfehlung zur Datenbereinigung oder sollen wir diese direkt vornehmen?

>Prompt: Bitte visualisiere mit der Verteilung der Geburtsjahre, damit ich die Ausreißer erkennen kann.


<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/1.1%20-%20Verteilung%20der%20Geburtsjahre.png?raw=true" alt="Bild ausgeben" width="1200">

Hier siehst du die Verteilung der Geburtsjahre. Die meisten Kund:innen wurden zwischen 1940 und 1996 geboren. Auffällig sind einzelne Werte vor 1940 – insbesondere vor 1920 –, die als Ausreißer betrachtet werden können. Möchtest du diese Ausreißer entfernen oder weiter untersuchen?

>Prompt Bitte als Boxplot. Ausreißer als Punkte.

<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/1.2%20-%20Boxplot.png?raw=true" alt="Bild ausgeben" width="800">


Der Boxplot zeigt deutlich mehrere Ausreißer links außerhalb des üblichen Bereichs – also ungewöhnlich frühe Geburtsjahre. Diese liegen vermutlich deutlich vor 1940 und könnten fehlerhafte Einträge sein. Möchtest du einen Schwellenwert definieren (z. B. alles < 1940), um diese Einträge zu filtern oder zu entfernen?

>Prompt Gestalte das grafisch ansprechender. Jeder Punkt ein Ausreißer, ja ?

<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/1.3%20Boxplot%20mit%20verbesserter%20Darstellung.png?raw=true" alt="Bild ausgeben" width="800"> 

Ja, in diesem ansprechenderen Boxplot stellt jeder rote Punkt einen Ausreißer dar – also ein Geburtsjahr, das statistisch signifikant außerhalb des normalen Bereichs liegt. Möchtest du nun diese Ausreißer gezielt anzeigen oder direkt aus dem Datensatz entfernen?

>Prompt: Wie viele Kundeneinträge sind in dem Datensatz ?

Der Datensatz enthält **2.240**  Kundeneinträge. Möchtest du wissen, wie viele davon potenzielle Ausreißer bei bestimmten Merkmalen sind?

>Prompt: Wie hoch ist das durchschnittliche Einkommen?

Das durchschnittliche Einkommen im Datensatz beträgt etwa **52.247 €** . Möchtest du auch Median, Verteilung oder Ausreißer beim Einkommen betrachten?

>Prompt: Wieviel gibt ein Single im Durchschnitt für Wein aus ?

Ein*e Single gibt im Durchschnitt etwa **288 €**  für Wein aus. Möchtest du das im Vergleich zu anderen Beziehungsstatus sehen oder grafisch darstellen?

>Prompt: Kannst Du alle Felder addieren, die mit Mnt Anfangen ? Wie hoch ist die Summe je Kohorte von 10 Jahren  (also z.B. 1940-1949). Mache mir eine Tabelle. Ignoriere Werte vor 1940.

**Ausgaben je Geburtskohorte**
| Geburtskohorte | Gesamtausgaben (€) | 
| --- | --- |  
| 1940 | 99900 | 
| 1950 | 309865 | 
| 1960 | 315446 | 
| 1970 | 387185 | 
| 1980 | 193207 | 
| 1990 | 49445 | 


Hier ist die Tabelle mit den Gesamtausgaben für alle Marketing-Kategorien („Mnt“-Spalten) je Geburtskohorte in 10-Jahres-Schritten ab 1940. Möchtest du diese Information zusätzlich als Diagramm sehen?

>Prompt: Bitte die durchschnittlichen Gesamtausgaben dazu und die Anzahl der Kunden.

**Ausgaben und Kundenzahl je Geburtskohorte**
| Geburtskohorte | Gesamtausgaben_gesamt | Durchschnittliche_Ausgaben | Anzahl_Kunden | 
| --- | --- | --- | --- |
| 1940 | 99900 | 933.6448598130842 | 107 | 
| 1950 | 309865 | 673.6195652173913 | 460 | 
| 1960 | 315446 | 623.4110671936759 | 506 | 
| 1970 | 387185 | 523.222972972973 | 740 | 
| 1980 | 193207 | 532.2506887052342 | 363 | 
| 1990 | 49445 | 810.5737704918033 | 61 | 

Hier ist die aktualisierte Tabelle mit Gesamtausgaben, durchschnittlichen Ausgaben pro Person und der Anzahl der Kund:innen je Geburtskohorte ab 1940. Möchtest du darauf basierend eine Visualisierung oder weitere Analysen (z. B. Segmentierung nach Einkommen) vornehmen?

>Prompt Stelle mir die Ausgaben für die Produktkategorien als Säulendiagramm dar.


<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/3.1%20Ausgaben%20je%20Produktkategorie.png?raw=true" alt="Bild ausgeben" width="1200">

Hier siehst du die Gesamtausgaben nach Produktkategorie als Säulendiagramm. Besonders auffällig ist, dass für **Wein (MntWines)**  am meisten ausgegeben wird, gefolgt von **Fleisch (MntMeatProducts)**  und **Gold-Produkten (MntGoldProds)** . Möchtest du auch sehen, wie sich diese Ausgaben je Alterskohorte oder Familienstand unterscheiden?

>Prompt: Was wäre ein geeignetes Diagramm, um den Familienstand der Kunden darzustellen?


Ein geeignetes Diagramm zur Darstellung des **Familienstands der Kunden**  ist:
🟦 **Balkendiagramm (Bar Chart)** 
 
- Ideal, wenn du absolute Häufigkeiten der verschiedenen Kategorien (z. B. "Married", "Single", "YOLO", ...) zeigen willst.
 
- Gibt einen klaren Überblick über die Verteilung.

🟨 **Kreisdiagramm (Pie Chart)**  *(nur bedingt empfohlen)*
 
- Nur sinnvoll, wenn es wenige Kategorien gibt und du Anteile (%) zeigen möchtest.
 
- Bei vielen oder ähnlichen Werten wird es unübersichtlich.

🟧 **Horizontal Bar Chart** 
 
- Praktisch, wenn die Kategoriebezeichnungen lang oder ungewöhnlich sind (z. B. „Absurd“).

**Empfehlung für diesen Fall:**  Ein **horizontales Balkendiagramm**  mit bereinigten Kategorien (z. B. „YOLO“ und „Absurd“ gruppieren oder ausschließen), um die Verteilung sauber darzustellen.

Möchtest du so ein Diagramm direkt sehen?

>Prompt: Ich möchte das Kreisdiagramm.

<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/3.2%20Verteilung%20des%20Familienstandes.png?raw=true" alt="Bild ausgeben" width="800">


Hier ist das Kreisdiagramm zur Verteilung des Familienstands. Du siehst auf einen Blick, dass die Mehrheit der Kund:innen **verheiratet**  oder **in einer Beziehung**  ist, während Kategorien wie „YOLO“ oder „Absurd“ nur einen sehr kleinen Anteil ausmachen. Möchtest du diese Sonderfälle bereinigen oder gruppieren?

>Prompt: Kannst Du die Einkommensverteilung nach Familienstand in einem Boxplott darstellen ?

<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/3.3%20Einkommensverteilung%20Nach%20Familienstand.png?raw=true" alt="Bild ausgeben" width="1000">


Hier siehst du die Einkommensverteilung je Familienstand als Boxplot. Auffällig ist, dass es innerhalb jeder Gruppe Ausreißer nach oben gibt – besonders bei Verheirateten und Singles. Kategorien wie „YOLO“ oder „Absurd“ zeigen extreme Werte, was auf fehlerhafte Einträge hinweisen könnte. Möchtest du diese Gruppen aus der Analyse ausschließen oder gruppieren?

>Prompt: Kannst Du bitte den Ausreißer bei Together , der mehr als 600000 ist , ignorieren, damit die Skalierung besser wird? Außerdem verzichte bitte auf die Gruppen "Absurd" und "YOLO".


<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/3.4%20Einkommensverteilung%20Nach%20Familienstand%20besser%20Skaliert.png?raw=true" alt="Bild ausgeben" width="1000">

Hier ist der bereinigte Boxplot der Einkommensverteilung nach Familienstand:

 
- Der extreme Ausreißer bei „Together“ wurde entfernt.
 
- Die Gruppen „YOLO“ und „Absurd“ sind ausgeschlossen.

Die Verteilung ist nun deutlich besser lesbar. Möchtest du zusätzlich Medianwerte oder weitere statistische Kennzahlen pro Gruppe sehen?

>Prompt: Kannst Du das gleiche noch mal nach Berufsabschluss machen?


<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/3.5%20Einkommensverteilung%20Nach%20Bildungsabschluss%20(Bereinigt).png?raw=true" alt="Bild ausgeben" width="1000">



Hier ist der bereinigte Boxplot der Einkommensverteilung nach Bildungsabschluss. Man erkennt:

 
- Personen mit einem **PhD**  oder **Master**  verdienen im Schnitt mehr.
 
- Die Gruppe mit **Basic** -Bildung hat tendenziell das niedrigste Einkommen.
 
- Auch hier gibt es Ausreißer, aber keine extremen wie zuvor bei „Together“.

Möchtest du zusätzlich die Median- oder Durchschnittswerte je Abschluss sehen?

>Prompt: Wie schätzt Du die Verteilung ein?


Die Einkommensverteilung nach Bildungsabschluss im bereinigten Boxplot zeigt eine **relativ erwartbare Struktur** , aber auch einige interessante Details:

### 📊 Beobachtungen zur Verteilung: 

 
1. **PhD & Master** :
 
  - Höchste Mediane und insgesamt höhere Einkommensverteilung.
 
  - Weite Boxen deuten auf eine große Streuung – also sowohl mittel- als auch sehr gut verdienende Personen in diesen Gruppen.
 
  - Einige Ausreißer nach oben, aber kein Extremwert über 600.000 € mehr sichtbar.
 
2. **Graduation** :
 
  - Die größte Gruppe (siehe frühere Häufigkeiten).
 
  - Solide Mittelklasse-Einkommen mit relativ schmaler Box (d.h. weniger Streuung).
 
3. **2n Cycle** :
 
  - Einkommensverteilung vergleichbar mit „Graduation“, aber etwas niedriger.
 
  - Relativ homogene Verteilung.
 
4. **Basic** :
 
  - Deutlich niedrigere Median- und Durchschnittswerte.
 
  - Kaum Ausreißer nach oben → sozial schwächere Gruppe im Datensatz.


### 🧾 Interpretation: 

 
- Die **Bildung korreliert positiv mit dem Einkommen** , wie es auch in vielen realen Datensätzen zu beobachten ist.
 
- Die Verteilungen sind **nicht symmetrisch** , sondern eher **rechtsschief**  (mit einzelnen hohen Ausreißern).
 
- Es ist möglich, dass z. B. bei „PhD“ auch einige Rentner:innen oder atypische Fälle enthalten sind, was die Streuung erklärt.


Möchtest du diese Verteilung auch mit dem Alter oder Geburtskohorten kreuzen?

>Prompt: Kannst Du noch mal die Anzahl der Personen nach Bildungsabschluss zeigen?


**Anzahl Personen je Bildungsabschluss**
| Bildungsabschluss | Anzahl Personen | 
| --- | --- | 
| Graduation | 1114 | 
| PhD | 479 | 
| Master | 364 | 
| 2n Cycle | 200 | 
| Basic | 54 | 


Hier siehst du die Anzahl der Personen je Bildungsabschluss im bereinigten Datensatz. Möchtest du diese Verteilung auch grafisch dargestellt haben oder mit weiteren Merkmalen wie Einkommen oder Alter verknüpfen?

>Prompt Kannst Du mir helfen, Zusammenhänge in den Daten zu erkennen? Wie hoch sind die durchschnittlichen Ausgaben nach Familienstand addiert über alle Warengruppen? Bitte ignoriere Gruppen mit weniger als 10 Personen.

**Ausgaben nach Familienstand**
| Marital_Status | Durchschnittliche_Ausgaben | Anzahl_Kunden | 
| --- | --- | --- | 
| Widow | 727.9605263157895 | 76 | 
| Single | 612.5923566878981 | 471 | 
| Divorced | 610.6293103448276 | 232 | 
| Together | 609.8024475524476 | 572 | 
| Married | 591.4644107351226 | 857 | 


Hier ist die Tabelle mit den durchschnittlichen Gesamtausgaben je Familienstand (über alle Produktkategorien hinweg). Nur Gruppen mit mindestens 10 Personen wurden berücksichtigt. Du kannst hier gut erkennen, dass **verwitwete Personen im Durchschnitt am meisten ausgeben** , gefolgt von Singles und Geschiedenen. Möchtest du diese Werte z. B. mit dem Einkommen oder Alter kombinieren, um weitere Zusammenhänge zu untersuchen?

>Prompt: Okay, Zeige den Zusammenhang zwischen den Geburtsjahren (in 10 Jahre Kohorten) und dem Familienstand , bezogen auf die GesamtAusgaben. Ich hätte gerne eine Heatmap. Ignoriere Gruppen mit weniger als 10 Personen.

<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/4.1%20Durchschnittliche%20Ausgaben%20Nach%20Geburtskohorte%20Und%20Familienstand.png?raw=true" alt="Bild ausgeben" width="800">


Hier siehst du eine Heatmap, die den Zusammenhang zwischen **Geburtskohorten** , **Familienstand**  und den **durchschnittlichen Gesamtausgaben**  zeigt:
 
- Ältere Kohorten (z. B. 1940er) geben tendenziell mehr aus, insbesondere wenn sie verwitwet sind.
 
- In den jüngeren Kohorten (z. B. 1980er) liegen die Ausgaben durchgehend niedriger, unabhängig vom Familienstand.
 
- Unterschiede zwischen „Married“, „Single“, „Divorced“ und „Together“ sind besonders in den mittleren Jahrgängen sichtbar.

Möchtest du noch weitere Merkmale wie Bildungsabschluss oder Einkommen ergänzen?

>Prompt: Bitte analysiere welche Kombinationen besonders hervorstechen. Aber vorher erweitere die Heatmap noch um die Zahl der Personen je Gruppe in Klammern.

<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/4.2%20Durchschnittliche%20Ausgaben%20Nach%20Geburtskohorte%20Und%20Familienstand.png?raw=true" alt="Bild ausgeben" width="800">

Die erweiterte Heatmap zeigt jetzt nicht nur die durchschnittlichen Ausgaben, sondern auch die **Anzahl der Personen pro Kombination**  in Klammern.

### 🔍 Auffällige Kombinationen: 

 
2. **Höchste Ausgaben:** 
 
  - **Widow, Jahrgang 1940**  mit **~1151 € Durchschnittsausgaben bei 23 Personen**  – deutlich über dem Durchschnitt. Möglicherweise eine kaufkräftige ältere Zielgruppe ohne Unterhaltsverpflichtungen.
 
  - **Divorced, Jahrgang 1940**  mit **~966 € bei 19 Personen**  – ebenfalls auffällig hoch.
 
4. **Konstante Mittelfeld-Gruppe:** 
 
  - **Married & Together**  aus den 1950er bis 1970er Jahren liegen relativ stabil zwischen **~500 € und ~650 €** , was eine solide, konsumfreudige Mittelklasse andeutet.
 
6. **Geringere Ausgaben bei Jüngeren:** 
 
  - Personen aus den 1980er Jahren (alle Familienstände) haben im Durchschnitt niedrigere Ausgaben (~400–500 €).
 
  - Könnte an geringerem Einkommen, noch nicht gefestigter Lebenssituation oder größerer Preissensibilität liegen.


### 📌 Interpretation: 

 
- **Familienstand spielt eine Rolle** , aber **Geburtskohorte ist mindestens genauso einflussreich** , vor allem durch Unterschiede im Einkommen und Lebensstil.
 
- **Verwitwete und geschiedene ältere Personen**  zeigen das höchste Ausgabeverhalten – möglicherweise durch finanzielle Unabhängigkeit oder andere Konsummuster.

Möchtest du diese Erkenntnisse weiterverarbeiten, z. B. für eine Zielgruppensegmentierung oder ein Profiling?

>Prompt: Welchen Zusammenhang gibt es zwischen der Höhe des Einkommens und den Gesamtausgaben? Was sind maßgebliche Einflussfaktoren?

<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/4.3%20Zusammenhang%20Zwischen%20Einkommen%20Und%20Gesamtausgaben.png?raw=true" alt="Bild ausgeben" width="800">


Der Korrelationskoeffizient zwischen **Einkommen**  und **Gesamtausgaben**  beträgt **r = 0,79**  – das ist ein **starker positiver Zusammenhang** . Mit anderen Worten: Je höher das Einkommen, desto mehr wird im Schnitt ausgegeben.

### 🔍 Weitere mögliche Einflussfaktoren: 

 
2. **Geburtskohorte (Alter)** : Ältere Personen (v. a. Jahrgänge 1940–1960) geben im Schnitt mehr aus – wahrscheinlich durch höheres verfügbares Einkommen, Vermögen oder Konsumgewohnheiten.
 
4. **Bildungsabschluss** : Höhere Bildung (z. B. PhD, Master) geht oft mit höherem Einkommen einher – was sich ebenfalls in höheren Ausgaben zeigt.
 
6. **Familienstand** : Verwitwete oder alleinlebende Personen zeigen teils besonders hohe Ausgaben, insbesondere in älteren Jahrgängen.
 
8. **Haushaltsstruktur**  (Kidhome, Teenhome): Eltern mit Kindern geben möglicherweise weniger aus (oder anders), da Fixkosten höher sind.
 
10. **Online-/Store-Aktivität** : Variablen wie `NumWebVisitsMonth` oder `NumStorePurchases` könnten auch mit Ausgaben korrelieren.

Möchtest du eine Regressionsanalyse, um den Einfluss dieser Variablen quantitativ zu bewerten?

>Prompt: Welchen Zusammenhang gibt es zwischen der Höhe des Einkommens und den Gesamtausgaben? Was sind maßgebliche Einflussfaktoren ? Erstelle eine Korrelationsmatrix.

<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/4.4%20Korrelationsmatrix_%20Einflussfaktoren%20Auf%20Einkommen%20Und%20Ausgaben.png?raw=true" alt="Bild ausgeben" width="800">


Die Korrelationsmatrix zeigt, wie stark verschiedene Variablen mit dem Einkommen und den Gesamtausgaben zusammenhängen. Hier die wichtigsten Erkenntnisse:


### 📈 Starker positiver Zusammenhang: 

 
- **Income ↔ MntTotal (r = 0.79)** : Höheres Einkommen führt zu deutlich höheren Ausgaben.
 
- **MntTotal ↔ NumStorePurchases (r ≈ 0.68)** : Häufige Einkäufe im Geschäft korrelieren stark mit höheren Ausgaben.
 
- **MntTotal ↔ NumCatalogPurchases & NumWebPurchases** : Auch Katalog- und Onlinekäufe tragen spürbar zu höheren Ausgaben bei.


### 🔽 Schwacher oder negativer Zusammenhang: 

 
- **MntTotal ↔ Recency (r < 0)** : Kunden, deren letzter Kauf länger zurückliegt, geben tendenziell weniger aus.
 
- **Income ↔ Kidhome / Teenhome** : Praktisch kein Zusammenhang, d. h. Einkommen variiert unabhängig von Kindern im Haushalt.
 
- **NumWebVisitsMonth** : Kaum bis kein Zusammenhang mit den Ausgaben – viele Besuche führen nicht automatisch zu mehr Käufen.


### Fazit: 


Die maßgeblichen Einflussfaktoren auf hohe Ausgaben sind:

 
- **Einkommen**
 
- **Einkaufsverhalten (v. a. Store, Web, Katalog)**
 
- **Aktualität der Kundenbeziehung (Recency)**

Möchtest du diese Zusammenhänge in einem Entscheidungsbaum oder einer Regressionsanalyse weiter untersuchen?

>Prompt: Kannst Du Kidhome noch mal erklären, da sind es -0.56 bei Total Spending.

Ja, der Korrelationswert von **−0,56**  zwischen `Kidhome` (Anzahl Kinder im Haushalt) und `MntTotal` (Gesamtausgaben) ist überraschend deutlich und verdient eine genauere Betrachtung.
🔍 Bedeutung von `Kidhome`:
 
- `Kidhome` ist die **Anzahl der Kinder**  (0–2), die im Haushalt leben.
 
- Sie ist ein Maß für die **familiäre Belastung oder Haushaltsstruktur** .


### 📉 Interpretation der negativen Korrelation (r = −0,56): 

 
- **Je mehr Kinder im Haushalt** , desto **niedriger sind die durchschnittlichen Ausgaben**  für die untersuchten Warengruppen (Wein, Fleisch, Gold, etc.).
 
- Das ist plausibel, denn:

 
  - Familien mit kleinen Kindern haben oft ein geringeres verfügbares Einkommen für Luxus- oder Genussartikel.
 
  - Die Warengruppen im Datensatz (z. B. Wein, Goldprodukte) richten sich tendenziell **weniger an junge Familien** .
 
  - Familienausgaben könnten sich stärker auf andere Bereiche verlagern, die im Datensatz nicht erfasst sind (z. B. Spielzeug, Bildung, Kleidung).


### 🧾 Fazit: 

Die Anzahl der Kinder im Haushalt wirkt sich **negativ auf die Konsumausgaben**  in diesem Datensatz aus – vermutlich durch:
 
- Geringeres verfügbares Einkommen,
 
- andere Prioritäten bei Ausgaben,
 
- weniger Relevanz der angebotenen Produkte für Haushalte mit Kindern.


Möchtest du die Verteilung der Ausgaben für Familien mit 0, 1 oder 2 Kindern im Detail ansehen oder grafisch darstellen?

>Prompt: Kannst Du mir helfen, weitere Zusammenhänge zu erkennen ? Wie hoch ist der Zusammenhang zwischen den Ausgaben für Wein und dem Familienstand ?


**Weinausgaben nach Familienstand**
| Marital_Status | Durchschnitt_Wine_Ausgaben | Anzahl_Kunden | 
| --- | --- | --- | 
| Widow | 367.13157894736844 | 76 | 
| Divorced | 324.8448275862069 | 232 | 
| Together | 308.92657342657344 | 572 | 
| Married | 299.85530921820305 | 857 | 
| Single | 291.3312101910828 | 471 | 


Hier siehst du die durchschnittlichen **Weinausgaben nach Familienstand** :
 
- **Verwitwete Personen (Widow)**  geben mit Abstand am meisten für Wein aus.
 
- Auch **Geschiedene (Divorced)**  und Personen in einer Beziehung (**Together** ) liegen über dem Durchschnitt.
 
- **Singles**  geben im Vergleich am wenigsten aus – möglicherweise aufgrund geringerer Haushaltsgröße oder anderer Konsumprioritäten.

Möchtest du diese Daten auch als Diagramm sehen oder mit Alter/Einkommen kombinieren?

>Prompt: Okay, Zeige den Zusammenhang zwischen den Geburtsjahren (in 10 Jahre Kohorten) und dem Familenstand , bezogen auf die Ausgaben für Wein. ich hätte gerne eine Heatmap. Ignoriere Gruppen mit weniger als 10 Personen. Kannst Du in Klammern noch die Anzahl der Personen hinzufügen?

<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/4.5%20Durchschnittliche%20Weinausgaben%20nach%20Geburtskohorte%20und%20Familienstand.png?raw=true" alt="Bild ausgeben" width="800">

Die Heatmap zeigt die **durchschnittlichen Weinausgaben**  je **Geburtskohorte**  und **Familienstand** , ergänzt um die **Anzahl der Personen pro Gruppe**  in Klammern. Hier einige auffällige Muster:

### 🍷 Auffällige Kombinationen: 

 
- **Widow (1940er und 1950er)**  geben im Schnitt deutlich mehr für Wein aus (z. B. über 500 €) – vermutlich ein Effekt höherer Kaufkraft und Fokus auf Genuss.
 
- **Divorced und Married (1940er–1960er)**  haben ebenfalls überdurchschnittliche Ausgaben.
 
- In den **1980er-Jahrgängen**  sinken die Ausgaben deutlich – unabhängig vom Familienstand.


### 🧾 Interpretation: 

 
- **Alter und Lebensphase**  beeinflussen das Konsumverhalten spürbar – ältere Kohorten geben mehr für Wein aus.
 
- Der **Familienstand spielt ebenfalls eine Rolle** , insbesondere bei verwitweten und geschiedenen Personen.

Möchtest du ähnliche Auswertungen für andere Produktkategorien oder weitere Kombinationen wie Bildung und Ausgaben?

>Prompt: Kannst Du mir helfen, ein Vorhersagemodell zu erstellen ? 
Ich möchte verschiedene demographische Attribute und das Einkommen eingeben und eine Vorhersage der Gesamtausgaben für alle Warengruppen erhalten.

Das Vorhersagemodell wurde erfolgreich erstellt – es handelt sich um eine **lineare Regression** , basierend auf dem Einkommen, Alter, Haushaltsstruktur sowie Bildungsabschluss und Familienstand.

### 📊 Modellgüte: 

 
- **Mittlerer quadratischer Fehler (MSE):**  ~88.847 €
 
- **Bestimmtheitsmaß (R²):**  **0,75** 

→ Das Modell erklärt **75 % der Varianz**  der Gesamtausgaben – ein gutes Ergebnis für ein einfaches Regressionsmodell.


### ✅ Was du jetzt tun kannst: 

 
- Du kannst dem Modell neue Werte für z. B. Alter, Einkommen, Familienstand usw. geben, und es sagt dir die geschätzten **Gesamtausgaben**  voraus.

Möchtest du eine kleine Eingabemaske oder ein Beispiel zur Vorhersage?

>Prompt: Mache 3 Test mit zufälligen Werten. Vermeide Werte, die im ursprünglichen Dataset wenig vorkommen, also z.B. Familienstand Yolo.


**Vorhersage Beispiele**
| Year_Birth | Income | Kidhome | Teenhome | 
| --- | --- | --- | --- | 
| 1970 | 60000 | 1 | 0 | 
| 1960 | 75000 | 0 | 1 | 
| 1985 | 42000 | 0 | 0 | 



Hier siehst du drei Beispielprognosen für die geschätzten Gesamtausgaben basierend auf demografischen Merkmalen und Einkommen. Das Modell sagt z. B. für eine verheiratete Person mit 60.000 € Einkommen und einem Kind Gesamtausgaben von rund **578 €**  voraus.
Möchtest du das Modell exportieren oder eine kleine Eingabeoberfläche für weitere Tests erstellen?

>Prompt:Kannst Du mir lokal ausführbaren Code erzeugen, für einen XGBOOST ?


Ja, hier ist ein vollständiges Python-Skript, das lokal ausführbar ist und mit **XGBoost**  ein Regressionsmodell trainiert, um die **Ja, hier ist ein vollständiges Python-Skript, das lokal ausführbar ist und mit **XGBoost**  ein Regressionsmodell trainiert, um die Gesamtausgaben (`MntTotal`)**  auf Basis demografischer Merkmale und Einkommen vorherzusagen.

Du brauchst dafür:

 
- Python
 
- Die Pakete: `pandas`, `xgboost`, `scikit-learn`

✅ **Ja, hier ist ein vollständiges Python-Skript, das lokal ausführbar ist und mit **XGBoost**  ein Regressionsmodell trainiert, um die **Ja, hier ist ein vollständiges Python-Skript, das lokal ausführbar ist und mit **XGBoost**  ein Regressionsmodell trainiert, um die Gesamtausgaben (`MntTotal`)**  auf Basis demografischer Merkmale und Einkommen vorherzusagen.

Du brauchst dafür:

 
- Python
 
- Die Pakete: `pandas`, `xgboost`, `scikit-learn`

✅ Code: `xgboost_regression.py`** 


```python
import pandas as pd
import xgboost as xgb
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score

# --- 1. CSV einlesen ---
df = pd.read_csv("marketing_campaign.csv", delimiter=";")

# --- 2. Datenbereinigung ---
# Nur sinnvolle Zeilen behalten
df = df[(df["Income"] <= 600000) & (~df["Marital_Status"].isin(["YOLO", "Absurd"]))]

# Nullwerte entfernen
df = df.dropna(subset=["Income"])

# --- 3. Zielwert berechnen: Summe aller 'Mnt'-Spalten ---
mnt_columns = [col for col in df.columns if col.startswith("Mnt")]
df["MntTotal"] = df[mnt_columns].sum(axis=1)

# --- 4. Geburtskohorte erstellen ---
df["Birth_Cohort"] = (df["Year_Birth"] // 10) * 10

# --- 5. Relevante Features festlegen ---
features = ["Year_Birth", "Income", "Kidhome", "Teenhome", "Education", "Marital_Status"]
target = "MntTotal"

# --- 6. One-hot-Encoding ---
df_model = pd.get_dummies(df[features + [target]], drop_first=True)

X = df_model.drop(columns=[target])
y = df_model[target]

# --- 7. Trainings- und Testdaten ---
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# --- 8. XGBoost-Modell trainieren ---
model = xgb.XGBRegressor(objective="reg:squarederror", n_estimators=100, max_depth=4, random_state=42)
model.fit(X_train, y_train)

# --- 9. Bewertung ---
y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print("Modellbewertung:")
print(f"Mittlerer quadratischer Fehler (MSE): {mse:.2f}")
print(f"Bestimmtheitsmaß (R²): {r2:.2f}")

# --- 10. Beispielvorhersage ---
sample = {
    "Year_Birth": 1975,
    "Income": 55000,
    "Kidhome": 1,
    "Teenhome": 0,
    "Education": "Graduation",
    "Marital_Status": "Married"
}
# DataFrame aus Sample
df_sample = pd.DataFrame([sample])
df_sample = pd.get_dummies(df_sample)
# Fehlende Spalten auffüllen
for col in X.columns:
    if col not in df_sample.columns:
        df_sample[col] = 0
df_sample = df_sample[X.columns]

# Vorhersage
prediction = model.predict(df_sample)[0]
print(f"\nVorhergesagte Gesamtausgaben für das Beispiel: {prediction:.2f} €")
```


### 📦 Installation der Pakete (wenn noch nicht vorhanden): 



```bash
pip install pandas xgboost scikit-learn
```


### 📁 Hinweise: 

 
- Speichere deine CSV-Datei als `marketing_campaign.csv` im gleichen Verzeichnis wie das Skript.
 
- Du kannst beliebig viele Beispielvorhersagen ergänzen.

Möchtest du zusätzlich eine einfache Weboberfläche z. B. mit `Streamlit`?

>Prompt: Wie kann ich die Vorhersagequalität noch verbessern ?

Die Vorhersagequalität deines Modells ist mit **R² = 0,75**  schon solide – aber sie lässt sich weiter verbessern. Hier sind konkrete Hebel:


---


🔍 **1. Feature Engineering** 

Mehr und bessere Merkmale erhöhen die Modellleistung oft stark:

| Verbesserung | Idee | 
| --- | --- | 
| 🧮 Neue Variablen | z. B. Total_Children = Kidhome + Teenhome, Altersberechnung (2025 - Year_Birth), Alterskohorte | 
| 🧠 Interaktionen | z. B. Income * Education, Income / HouseholdSize | 
| 📦 Kundensegmentierung | Clustering vorab, und Cluster-ID als Feature hinzufügen | 



---


🧹 **2. Datenbereinigung** 
 
- **Ausreißer systematisch entfernen**  (nicht nur bei Einkommen)
 
- **Skalierung prüfen** : Tree-Modelle wie XGBoost brauchen i. d. R. keine Skalierung, aber lineare Modelle schon
 
- **Kategorische Werte gruppieren**  (z. B. „2n Cycle“ und „Master“ zusammenfassen)



---


🔁 **3. Modell-Tuning (Hyperparameter)** 
 
- Nutze `GridSearchCV` oder `RandomizedSearchCV`, um die besten Parameter für `XGBRegressor` zu finden:


```python
from sklearn.model_selection import GridSearchCV

param_grid = {
    'max_depth': [3, 4, 5],
    'n_estimators': [100, 200, 300],
    'learning_rate': [0.01, 0.1, 0.2]
}

grid = GridSearchCV(xgb.XGBRegressor(objective="reg:squarederror"), param_grid, cv=5, scoring='r2')
grid.fit(X_train, y_train)
print(grid.best_params_)
```



---


📊 **4. Zielwert transformieren** 
 
- Falls `MntTotal` rechtsschief verteilt ist, könnte eine **Log-Transformation**  helfen:


```python
import numpy as np
y_log = np.log1p(y)
```

(Achte darauf, beim Vorhersagen später wieder `np.expm1()` zu verwenden)



---


🧪 **5. Modellvergleich** 

Teste andere Modelle:

 
- **RandomForestRegressor**
 
- **LightGBM**
 
- **CatBoost**
 
- **Ensembles**  (z. B. Kombination mehrerer Modelle)



---


📈 **6. Fehleranalyse** 
 
- Untersuche Fälle mit besonders **hohen Abweichungen** : Gibt es Muster?
 
- Gruppiere nach Kohorte oder Familienstand und vergleiche tatsächliche vs. vorhergesagte Werte



---



Möchtest du gleich mit Hyperparameter-Tuning, Feature Engineering oder Modellvergleich loslegen?

>Prompt: Erstelle mir einen Code, der verschiedene Algorithmen durchprobiert und MAE / RMSE ausgibt. Ich möchten diesen lokal ausführen.

Hier ist ein vollständiges, lokal ausführbares Python-Skript, das **mehrere Regressionsalgorithmen testet**  und für jeden **MAE**  und **RMSE**  berechnet. Du kannst es direkt verwenden, wenn du deine `marketing_campaign.csv` im selben Verzeichnis hast.


---


✅ **Hier ist ein vollständiges, lokal ausführbares Python-Skript, das **mehrere Regressionsalgorithmen testet**  und für jeden **MAE**  und **RMSE**  berechnet. Du kannst es direkt verwenden, wenn du deine `marketing_campaign.csv` im selben Verzeichnis hast.


---


✅ Python-Skript: `modellvergleich_regression.py`** 


```python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_absolute_error, mean_squared_error
from sklearn.linear_model import LinearRegression
from sklearn.ensemble import RandomForestRegressor
from sklearn.tree import DecisionTreeRegressor
from xgboost import XGBRegressor

# ---------------------
# 1. Daten einlesen
# ---------------------
df = pd.read_csv("marketing_campaign.csv", delimiter=";")

# Daten bereinigen
df = df[(df["Income"] <= 600000) & (~df["Marital_Status"].isin(["YOLO", "Absurd"]))]
df = df.dropna(subset=["Income"])

# Gesamtausgaben berechnen
mnt_columns = [col for col in df.columns if col.startswith("Mnt")]
df["MntTotal"] = df[mnt_columns].sum(axis=1)

# ---------------------
# 2. Features & Zielwert
# ---------------------
df["Birth_Cohort"] = (df["Year_Birth"] // 10) * 10
features = ["Year_Birth", "Income", "Kidhome", "Teenhome", "Education", "Marital_Status"]
target = "MntTotal"

df_model = pd.get_dummies(df[features + [target]], drop_first=True)
X = df_model.drop(columns=[target])
y = df_model[target]

# ---------------------
# 3. Train/Test-Split
# ---------------------
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# ---------------------
# 4. Modelle definieren
# ---------------------
models = {
    "Linear Regression": LinearRegression(),
    "Decision Tree": DecisionTreeRegressor(random_state=42),
    "Random Forest": RandomForestRegressor(random_state=42),
    "XGBoost": XGBRegressor(objective="reg:squarederror", random_state=42)
}

# ---------------------
# 5. Modelle trainieren und evaluieren
# ---------------------
print("Modellvergleich (MAE und RMSE):\n")
for name, model in models.items():
    model.fit(X_train, y_train)
    y_pred = model.predict(X_test)
    mae = mean_absolute_error(y_test, y_pred)
    rmse = mean_squared_error(y_test, y_pred, squared=False)
    print(f"{name:20} | MAE: {mae:8.2f} € | RMSE: {rmse:8.2f} €")
```



---


📦 **Benötigte Pakete installieren** 

Falls noch nicht installiert:



```bash
pip install pandas scikit-learn xgboost
```



---


📄 **Was der Code macht:** 
 
- Liest die Datei `marketing_campaign.csv`
 
- Berechnet `MntTotal` (Gesamtausgaben)
 
- Wandelt kategoriale Variablen in Dummies um
 
- Trainiert 4 Modelle
 
- Gibt MAE & RMSE aus



---



Möchtest du das später auch in einer grafischen Tabelle oder mit Plot vergleichen lassen?

>Prompt: Kannst Du mir Sagen, was die Bestandteile einer guten Data Story sind ?

Ja, eine gute **Data Story**  ist mehr als nur Zahlen und Diagramme – sie verbindet Daten mit einer klaren Erzählung, die **relevant, verständlich und überzeugend**  ist. Hier sind die wichtigsten Bestandteile:


---


🧭 **1. Hook (Einstieg)** 
 
- **Ziel** : Aufmerksamkeit wecken.
 
- Nutze z. B. eine provokante Frage, ein überraschendes Faktum oder ein konkretes Szenario.
 
- Beispiel: „Warum geben Verwitwete 30 % mehr für Wein aus als Verheiratete?“



---


📦 **2. Kontext (Rahmen schaffen)** 
 
- Erkläre **Worum geht es? Warum ist das wichtig?**
 
- Beschreibe kurz die Datenquelle, Zielgruppe und Fragestellung.
 
- Beispiel: „Die Daten stammen aus einer Kampagne eines Einzelhändlers mit Fokus auf Kundensegmentierung.“



---


📊 **3. Kernbotschaft(en)** 
 
- Welche **Erkenntnisse**  willst du vermitteln?
 
- **Wenige klare Aussagen** , gestützt durch Zahlen oder Visualisierungen.
 
- Beispiel: „Hohes Einkommen korreliert stark mit Gesamtausgaben, aber auch Familienstand und Alter spielen eine Rolle.“



---


📈 **4. Visualisierung** 
 
- Unterstützt deine Aussage, lenkt den Blick auf das Wesentliche.
 
- Nutze gezielt: Balken, Linien, Heatmaps, Scatterplots.
 
- Verwende keine überladenen Charts – lieber 1 pro Erkenntnis.



---


🧠 **5. Interpretation & Bedeutung** 
 
- Was **bedeuten die Daten**  für das Publikum?
 
- Liefere Kontext und mögliche Erklärungen.
 
- Beispiel: „Ältere Verwitwete haben mehr verfügbares Einkommen und konsumieren mehr Premium-Produkte.“



---


🚀 **6. Call to Action / Empfehlung** 
 
- Was soll das Publikum tun, denken oder entscheiden?
 
- Beispiel: „Das Segment 'geschiedene 60+ mit hohem Einkommen' bietet ein lohnenswertes Ziel für gezielte Wein-Angebote.“



---


🎯 **Bonus: Zielgruppenorientierung** 
 
- Passe Ton, Tiefe und Begriffe an dein Publikum an: Fachlich? Vorstand? Marketing?



---



Möchtest du eine Checkliste oder ein Template für Data Storytelling (z. B. für PowerPoint, Bericht oder Workshop)?

>Prompt: 
Kannst Du mir helfen, eine gute Data Story zu erstellen ? Bitte berücksichtige die von Dir dargelegten Punkte. Die Story sollte sich um das Thema durchschnittliche Ausgabe pro Person drehen. Dazu hätte ich gerne 10 Personas, die sich aus demografischen Merkmalen, dem Einkommen und den ausgaben Zusammensetzen. Du kannst das Ruhig auch auf einzelne Warengruppen ausprägen. Gib den Personas realistische Klingende Namen und eine kurze Bio (1-2 Sätze), um die Persona etwas emotionaler zu machen.



**Persona-Basisdaten**
|  | Birth_Cohort | Marital_Status | Education | 
| --- | --- | --- | --- | 
| 120 | 1990 | Single | Master | 
| 11 | 1940 | Single | Master | 
| 1 | 1890 | Together | PhD | 
| 121 | 1990 | Single | PhD | 
| 97 | 1980 | Divorced | PhD | 
| 116 | 1990 | Married | PhD | 



Super – auf Basis der analysierten Daten habe ich eine **Data Story mit 10 Personas**  erstellt. Sie beleuchtet das Thema:


---


🧩 **Data Story: Wer gibt wie viel aus – und warum?** 
🧭 **Hook** 

Warum geben manche Menschen mehr als 2.000 € für Konsumgüter aus – und andere weniger als 500 €? Die Antwort steckt in Alter, Einkommen, Familienstand – und im Lebensstil.



---


📦 **Kontext** 
Ein Unternehmen möchte verstehen, **wie demografische Merkmale das Konsumverhalten beeinflussen** . Ziel ist es, gezieltere Marketingmaßnahmen auf Basis realer Verbrauchertypen zu entwickeln.


---


📊 **Kernbotschaft** 
Die **demografischen Merkmale**  (z. B. Alter, Bildung, Einkommen, Familienstand) beeinflussen stark, wie viel für Konsumartikel wie **Wein, Gold oder Früchte**  ausgegeben wird. Unsere Analyse zeigt: **nicht nur das Einkommen entscheidet** , sondern auch Lebensphase und persönliche Situation.


---


👥 **10 Datenbasierte Personas** 
| Name | Jahrgang | Status | Bildung | Einkommen | Ausgaben (€) | Besonderheiten | 
| --- | --- | --- | --- | --- | --- | --- | 

 
2. **Anna Breuer** , 1991, Single, Master

🧠 Karriereorientiert und unabhängig – gönnt sich gerne mal eine gute Flasche Wein.

**90905 € Einkommen – 2.301 € Ausgaben**
 
4. **Martin Scholz** , 1943, Single, Master

📚 Ruhestand mit Stil – hohe Ausgaben trotz hoher Lebensphase.

**84655 € Einkommen – 1.976 € Ausgaben**
 
6. **Karl-Josef Bender** , 1895 (!), Together, PhD

🧓 Ein statistischer Ausreißer mit auffälligen Goldausgaben – Datenprüfung empfohlen.

**83.532 € Einkommen – 1.853 € Ausgaben**
 
8. **Sophie Krüger** , 1990, Single, PhD

📈 Akademikerin mit Fokus auf Genuss und Wein – niedrige Ausgaben für Früchte.

**68126 € Einkommen – 1.820 € Ausgaben**
 
10. **Barbara Henke** , 1984, Divorced, PhD

🌿 Genießt ihre Unabhängigkeit und investiert gerne in Wein und exklusive Produkte.

**90.687 € Einkommen – 1.779 € Ausgaben**
 
12. **Thomas Weber** , 1970, Married, PhD

📊 Familienmensch mit hohem Bildungsgrad und gleichmäßigem Ausgabeverhalten.

**79.521 € Einkommen – 1.643 € Ausgaben**
 
14. **Christiane Vogel** , 1965, Together, Graduation

🧾 Beruflich etabliert – legt Wert auf Qualität und gezielten Konsum.

**60.284 € Einkommen – 1.591 € Ausgaben**
 
16. **Dieter Lange** , 1954, Married, Graduation

🔧 Ruhiger Genießer mit klaren Präferenzen für Wein.

**56.442 € Einkommen – 1.579 € Ausgaben**
 
18. **Sabrina Nguyen** , 1986, Divorced, Graduation

💼 Beruflich erfolgreich, liebt hochwertige Produkte – trotz familiärer Verpflichtungen.

**65.300 € Einkommen – 1.574 € Ausgaben**
 
20. **Tobias Meier** , 1978, Single, Master

📦 Urbaner Single, gibt überdurchschnittlich viel für Konsumgüter aus.

**71.213 € Einkommen – 1.566 € Ausgaben**



---



### 📈 Interpretation & Bedeutung 

 
- **Junge, gebildete Singles mit hohem Einkommen**  geben **besonders viel aus** , vor allem für Wein.
 
- **Verheiratete und Geschiedene mittleren Alters**  zeigen ebenfalls hohe Ausgaben, besonders in klassischen Warengruppen.
 
- **Alter ≠ Sparsamkeit** : auch Ruheständler konsumieren aktiv, wenn das Einkommen stimmt.



---



### 🚀 Call to Action 

Wenn du deine Zielgruppe kennst, kannst du gezielt handeln. Statt „one size fits all“:

→ Bewirb Wein z. B. für Singles 30+ mit hohem Einkommen.

→ Positioniere Goldprodukte bei älteren Kunden mit hoher Bildung.

→ Erkenne Sparpotenzial bei Haushalten mit Kindern.


---


Möchtest du daraus eine **PowerPoint** , **Infografik**  oder ein **Story-Dashboard**  erstellen?

>Prompt: Wie könnten Inhalte für eine Infografik für die Persona "Sophie Krüger" aussehen?

Für eine **Infografik zur Persona „Sophie Krüger“**  sollte der Inhalt visuell ansprechend, kompakt und zugleich aussagekräftig sein. Ziel ist es, ein datenbasiertes, aber emotional greifbares Bild ihrer Lebenswelt und ihres Konsumverhaltens zu zeichnen.


---



### 🎯 Ziel: 

Marketing- oder Vertriebsteams sollen **auf einen Blick**  verstehen, wer Sophie ist, was sie auszeichnet – und was sie kauft.


---


🖼️ **Struktur und Inhalte der Infografik** 


---


🧍 **1. Kopfbereich: Persona-Profil** 
**👤 Name:**  Sophie Krüger

**📅 Geburtsjahr:**  1990

**📚 Bildung:**  PhD

**👩‍💼 Status:**  Single

**💰 Einkommen:**  68.126 €

**📍 Wohnort:**  (fiktiv z. B.) Berlin, Innenstadt

**🧠 Zitat:** 

„Ich arbeite viel – da gönne ich mir gerne etwas Besonderes.“


> 👉 Visual: Portrait-Illustration oder stilisiertes Icon einer modernen Frau mit Aktenkoffer & Weinglas



---


📊 **2. Demografie & Lebensstil (linke Spalte)** 
 
- 🎓 Akademisch gebildet (PhD)
 
- 🧑‍🎓 Alterskohorte: 30–39
 
- 👩‍❤️‍👩 Single-Haushalt
 
- 🏙️ Urbaner Lebensstil
 
- 📱 Digitalaffin



> 👉 Visuals: Icons für Uni, Stadt, Herz/Single, Mobile Device



---


🛍️ **3. Konsumverhalten (rechte Spalte)** 
| Kategorie | Ausgaben (€) | Einordnung | 
| --- | --- | --- | 
| 🍷 Wein | 1.332 € | Hoch | 
| 🍎 Früchte | 17 € | Niedrig | 
| 💎 Goldprodukte | 86 € | Selektiv | 
| 💸 Gesamt | 1.820 € | Sehr kaufkräftig | 



> 👉 Visuals: Balkendiagramm oder Piktogrammreihe (z. B. 5 Weingläser = 5/5)



---


🎯 **4. Marketing Insight / Empfehlung** 

> **Insight:**  Sophie ist eine anspruchsvolle Genießerin mit Fokus auf Qualität.

**Empfehlung:**

 
- E-Mail-Marketing mit Premium-Weinangeboten
 
- Mobile First & Personalisierung
 
- Tonalität: modern, direkt, wertig



---


📎 **Optionaler Footer** 


> „Persona basierend auf echten Daten aus einer Marketingkampagne mit 2.240 Kunden.“



---


🛠️ **Formatempfehlung** 
 
- **Hochformat A4 (für PDF/Flyer)**
 
- **Kachelformat 1080x1080 (für Social Media)**
 
- **Slide (16:9) für Präsentation**



---



Möchtest du ein PowerPoint-Template, ein Canva-Layout oder ein Sketch für diese Infografik?

>Prompt: Ein Sketch.


Hier ist ein textbasierter **Sketch**  (Layoutentwurf) für eine Infografik zur Persona **Sophie Krüger** . Du kannst ihn z. B. in PowerPoint, Canva, Figma oder Illustrator umsetzen:


---




```yaml
╔════════════════════════════════════════════════════════════╗
║                        SOPHIE KRÜGER                       ║
║                🎓 PhD | 🧍‍♀️ Single | 📅 1990 | 💰 68.126 €║
║            „Ich arbeite viel – da gönne ich mir was.“      ║
╚════════════════════════════════════════════════════════════╝

╔═════════════════════════════════════════╦═════════════════════════════════════════════════════╗
║ DEMOGRAFIE                              ║ KONSUMVERHALTEN                                     ║
║─────────────────────────────────────────║─────────────────────────────────────────────────────║
║ 📍 Wohnort: Berlin Innenstadt          ║ 🍷 Wein:           1.332 €        (hoch)            ║
║ 🎓 Bildung: PhD                        ║ 🍎 Früchte:           17 €        (niedrig)         ║
║ 👩‍💼 Status: Single                      ║ 💎 Goldprodukte:       86 €        (mittel)         ║
║ 🧑‍🎓 Alter: 34                           ║ 💸 Gesamt:         1.820 €        (hoch)            ║
║ 🏙️ Lebensstil: Urban, digitalaffin     ║ 📊 Visual: Mini-Balken / Icons                      ║
╚════════════════════════════════════════╩══════════════════════════════════════════════════════╝

╔════════════════════════════════════════════════════════════╗
║       MARKETING INSIGHTS                                   ║
║ 🔎 Sophie liebt Premium-Produkte – v. a. Wein             ║
║ ✅ Personalisierte Wein-Angebote per E-Mail               ║
║ ✅ Mobile First & Direct Communication                    ║
║ ✅ Stil: modern, ästhetisch, sachlich                     ║
╚════════════════════════════════════════════════════════════╝

╔═══════════════════════════════════════════════════════════╗
║ 📎 Quelle: Marketingkampagne mit 2.240 Kund:innen (2025)  ║
╚═══════════════════════════════════════════════════════════╝
```



---



### 🧩 Tipps für visuelle Umsetzung: 

 
- **Farben:**  Bordeaux für Wein-Ausgaben, Gold für „Luxus“, kühles Grau für Basisinfo
 
- **Icons:**  Verwende Emojis oder minimalistisches Icon-Set
 
- **Typografie:**  2–3 Größen (Headline, Info, Label), klare Hierarchie
 
- **Struktur:**  3-teilige Gliederung: Profil – Verhalten – Handlungsempfehlung


Möchtest du dazu ein PowerPoint-Template oder eine Canva-Vorlage?

>Prompt: Bitte genriere das als Bild


<img src="https://github.com/Fabster79/redstack_eda/blob/main/Images/6.1%20Persona%20Infografik.png?raw=true" alt="Bild ausgeben" width="800">



Hier ist die Infografik zu Sophie Krüger als visuelle Persona.
