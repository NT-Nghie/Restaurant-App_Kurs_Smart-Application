# **Spec \- Restaurant Bella Vista (K1)** 

**Quelle: Meeting 1 & 2**

# **Entitäten**

| Entität | Attribute |
| :---- | :---- |
| Standort  | Standort\_ID(PK), Name, Adresse, Öffnungszeit, Küchenschluss |
| Mitarbeiter  | Mitarbeiter\_ID(PK), Name, Rolle(Manager, Norm\_Mitarbeiter), |
| Gast | Gast\_ID(PK), Name, Telefonnummer, Stammgaststatus, Bella\_Card\_Rabatt(Ja/Nein) |
| Reservierung | Reservierung\_ID(PK), Datum, Uhrzeit, Personenzahl, Quelle, Notiz, Standort\_ID(FK), Gast\_ID(FK),  |
| Tisch | Tisch\_ID(PK), Tischnummer, Sitzplätze, Status, Standort\_ID(FK),  |
| Reservierung\_Tisch | Reservierung\_Tisch\_ID(PK), Reservierung\_ID(FK), Tisch\_ID(FK) |
| Schichtdienst | Schichteinsatz\_ID(PK), Mitarbeiter\_ID(FK), Standort\_ID(FK), Datum, Beginn, Ende |
| Bestellung | Bestellung\_ID(PK), Zeitpunkt, Status, Bestellart (In Haus, Zum Mitnehmen, Vorbestellung, Catering), Zahlungsstatus, Tisch\_ID(FK), Gast\_ID(FK), Standort\_ID(FK) |
| Bestellungsschrittzuordnung | Zuordnung\_ID(PK), Mitarbeiter\_ID(FK), Bestellung\_ID(FK), Tätigkeit(Aufnehmen, Rausbringen, Abkassieren) |
| Bestellposition | Position\_ID(PK), Menge, Sonderwunsch, Einzelpreis, Rabatt, Bestellung\_ID(FK), Gericht\_ID(FK) |
| Gericht | Gericht\_ID(PK), Name, Preis, Standort(dropdown-\> Standort 1, Standort 2, Beide) |

# 

# **Beziehungen**

- Standort 1:n Tisch   
- Standort 1:n Reservierung   
- Gast 1:n Reservierung   
- Gast 1:n Reservierung   
- Gast 1:n Bestellung   
- Tisch 1:n Bestellung 

**n:m Beziehungen**

- Bestellung 1:n Bestellposition n:1 Gericht (Eine Bestellung kann mehrere Gerichte beinhalten und ein Gericht kann in mehreren Bestellungen vorkommen)

- Bestellung 1:n Bestellungsschrittzuordnung n:1 Mitarbeiter (Ein Mitarbeiter kann mehrere Bestellungen haben und an einer Bestellung können mehrere Mitarbeiter gearbeitet haben (Aufnahme, Rausbringen, Abkassieren))

- Mitarbeiter 1:n Schichtdienst n:1 Standort (Ein Mitarbeiter kann bei mehreren Standorten eingesetzt werden (über die Zeit) und ein Standort hat mehrere Mitarbeiter)

- Reservierung 1:n Reservierung\_Tisch n:1 Tisch (Eine Reservierung kann mehrere Tische beinhalten, wenn es eine große Gruppe ist und ein Tisch kann in mehreren Reservierungen vorkommen (über die Zeit))

Notiz: Mitarbeiter n:m Standort und Reservierung n:m Tisch sind unter der Annahme , dass ein Tisch/Mitarbeiter nicht doppelt zur gleichen Zeit gebucht werden darf.

# **Business Rules**

- **BR1** Ab einer Gruppengröße von min. 8 Personen ist grundsätzlich das Gruppenmenü verpflichtet ( Meeting 1, Antwort 4\)

- **BR2** Ausnahmen benötigen eine Freigabe durch einen Manager ( Meeting 1 & 2, Antwort 5 & 20\)

- **BR3** Bei einem Regulären Restaurant-Küchenschluss, werden ab 22:30 keine neuen Bestellungen mehr angenommen (Meeting 1, Antwort 12\)

- **BR4** Die beiden Standorte haben verschiedene Speisekarten und man kann nur die Gerichte bestellen die bei dem jeweiligen Standort verfügbar sind (Meeting 1, Antwort 12\)

- **BR5** Tisch automatisch blockiert wenn er reserviert ist, Reservierungen werden um die 15-20 Minuten gehalten, dann wird angerufen (Meeting 1, Antwort 8 & 9\)

# **Widersprüche**

**C1 – Reservierungsquellen**

**Erste Aussage (Meeting 1, Antwort 8):**  
Marco möchte Reservierungen ausschließlich telefonisch entgegennehmen und keine Online-Reservierungen anbieten.

**Widersprüchliche Aussage (Meeting 2, Antwort 18):**  
Es gehen bereits Reservierungen über Google ein. Einige davon werden von Giulia ausgedruckt, aber sie werden nicht zentral verwaltet.

**Auflösung:**  
Sowohl telefonische Reservierungen als auch Reservierungen über Google werden unterstützt. Alle Reservierungen werden zentral in der Anwendung zusammengeführt, wobei die ursprüngliche Quelle weiterhin erkennbar bleibt.  
\-\> Zentrale Verwaltung mehrerer Reservierungsquellen inklusive Kennzeichnung der jeweiligen Quelle.

**C2 – Richtlinie für Gruppenmenüs vs. tatsächliche Praxis**

**Erste Aussage (Meeting 1, Antworten 4 & 5):**  
Für Gruppen ab acht Personen gilt die Regel für Gruppenmenüs. Ausnahmen dürfen nur von Marco genehmigt werden.

**Widersprüchliche Praxis (Meeting 1, Frage 5 und Klarstellung in Frage 19):**  
Als die Gruppengröße kurzfristig von sieben auf neun Personen anstieg, entschied ein Kellner eigenmächtig und in Marcos Abwesenheit, dass die Gruppe à la carte bestellen durfte.

**Auflösung:**  
Die Richtlinie ist strikt einzuhalten. Ausnahmen dürfen nur von Marco oder Giulia genehmigt werden. Mitarbeiter sind nicht erlaubt, solche Entscheidungen selbst zu treffen. Ist keine Führungskraft anwesend, muss die Entscheidung warten. \-\> Automatisierte Überprüfung der Gruppengröße und zwingende Genehmigung durch einen Manager bei Ausnahmen.

# **Prioritäten**

**Hohe Priorität**

- Zentrale Reservierungsverwaltung inklusive Google und Telefon.

- Digitale Bestellannahme und eindeutige Tischzuordnung.

- Stammgastverwaltung und Bella-Card-Rabatt.

- Standortabhängige Speisekarten.

- Automatische Durchsetzung der Gruppenmenü-Regel.

- Küchenschluss und Reservierungsbenachrichtigungen.

- Mitarbeiteraktivitäten und einfache Schichtübersicht.

**niedrigere Priorität**

- Digitale Abrechnungsunterstützung und getrennte Zahlungen.

- Catering-Anfragen, Angebote und Auftragsübersicht.

- Erweiterte Catering-Verwaltung bei steigendem Auftragsvolumen.

- Weitere Standorte und deren Einbindung.

# **Neue Anforderung aus Meeting 2**

**Catering-Verwaltung:**

Die Anwendung soll zusätzlich Catering-Anfragen, Angebote und bestätigte Aufträge verwalten. Dabei sollen Kundeninformationen, Veranstaltungsdetails, Preisangaben, Änderungen und Zahlungsstatus zentral nachvollziehbar sein.

