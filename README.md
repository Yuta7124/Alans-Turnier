# Darkime

**Live:** https://yuta7124.github.io/Alans-Turnier/

Firebase ist bereits eingerichtet (Projekt `alans-turnier-dc34c`, Firestore in Frankfurt, Regeln aus `firestore.rules` veröffentlicht, Anmeldung mit E-Mail/Passwort aktiv). Die Zugangsdaten stehen in `config.js`.

Die Anleitung unten beschreibt die Einrichtung von Grund auf, falls du sie einmal neu machen musst.

---

## Anleitung für GitHub Pages

Die Seite läuft kostenlos auf **GitHub Pages**. Die Daten (Spieler, Punkte, Quiz, Zufallsrad, Ankündigungen) liegen in einer kostenlosen **Firebase-Datenbank** von Google. So sehen alle Geräte live dasselbe, und deine Freunde können ohne Konto eigene Spieler anlegen und im Quiz selbst antworten.

Dauer: etwa 15 Minuten, am besten am PC.

## Dateien

| Datei | Wofür |
|---|---|
| `index.html` | Die komplette Seite |
| `en.js` | Die englischen Texte (wird nur geladen, wenn jemand English wählt) |
| `config.js` | Deine Firebase-Daten (trägst du in Schritt 1.5 ein) |
| `firestore.rules` | Die Sicherheitsregeln für die Datenbank (Schritt 1.4) |
| `.nojekyll` | Kleine Hilfsdatei für GitHub Pages (optional) |

---

## 1. Firebase einrichten

1. **Projekt anlegen:** Öffne [console.firebase.google.com](https://console.firebase.google.com), melde dich mit deinem Google-Konto an und klicke auf **Projekt erstellen**. Name zum Beispiel `alans-turnier`. Google Analytics brauchst du nicht.
2. **Datenbank anlegen:** Links unter **Build** auf **Firestore Database** → **Datenbank erstellen**. Standort `europe-west3 (Frankfurt)` wählen und **im Produktionsmodus** starten.
3. **Anmeldung aktivieren:** Links **Build** → **Authentication** → **Jetzt starten**. Unter **Anmeldemethode** die Methode **E-Mail-Adresse/Passwort** aktivieren und speichern. Dein Spielleiter-Konto legst du später direkt auf der Seite an.
4. **Regeln eintragen:** **Firestore Database** → Tab **Regeln**. Alles löschen, den kompletten Inhalt von `firestore.rules` einfügen und auf **Veröffentlichen** klicken. Du musst darin nichts ändern.
5. **Web-App registrieren:** Oben links auf das Zahnrad → **Projekteinstellungen** → ganz unten bei **Meine Apps** das Web-Symbol `</>` anklicken. Einen Namen eingeben, Firebase Hosting **nicht** anhaken, **App registrieren**. Firebase zeigt dir jetzt einen Block `firebaseConfig`. Übertrage die Werte (`apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`) in die Datei `config.js`.
6. **Domain freigeben:** **Authentication** → **Einstellungen** → **Autorisierte Domains** → **Domain hinzufügen** → `DEINNAME.github.io` (dein GitHub-Benutzername).

Optional, erst **nachdem** du dein Spielleiter-Konto angelegt hast (Schritt 3.2): Unter **Authentication** → **Einstellungen** → **Nutzeraktionen** die Registrierung (sign-up) ausschalten. Dann kann niemand weitere Konten anlegen. Nötig ist das nicht, weitere Konten bleiben ohnehin Gäste.

## 2. Auf GitHub Pages hochladen

1. Auf [github.com](https://github.com) oben rechts **+** → **New repository**. Name zum Beispiel `alans-turnier`, Sichtbarkeit **Public**, **Create repository**.
2. Auf **uploading an existing file** klicken und `index.html` und die ausgefüllte `config.js` hineinziehen (`.nojekyll` darf mit, muss aber nicht). Unten **Commit changes**.
3. Im Repository **Settings** → **Pages**. Bei **Source** „Deploy from a branch“, bei **Branch** `main` und `/ (root)` wählen, **Save**.
4. Nach 1–2 Minuten ist die Seite erreichbar unter
   `https://DEINNAME.github.io/alans-turnier/`

Das Repository ist öffentlich, aber nur der Programmcode. Die Daten stecken in Firebase und sind durch das Turnier-Passwort geschützt. Die Werte in `config.js` sind nicht geheim, das ist bei Firebase so gedacht.

## 3. Erster Start

1. Öffne deinen Link. Du siehst die Passwort-Abfrage.
2. Tippe auf **Spielleiter-Login**, gib deine E-Mail und ein neues Passwort (mindestens 6 Zeichen) ein und tippe auf **Konto anlegen**. Das erste Konto wird automatisch der Spielleiter. Mach das also gleich, sobald die Seite online ist. Später meldest du dich mit denselben Daten über **Einloggen** an.
3. Leg das **Turnier-Passwort** fest. Das bekommen deine Freunde.
4. Fertig. Unter **Optionen** findest du den Link zum Kopieren, das Preisgeld, die Quiz-Musik und das Turnier-Passwort zum Ändern.

## So funktioniert es für deine Freunde

- Sie öffnen den Link, sehen ein kurzes Intro, geben einmal das Turnier-Passwort ein (ihr Gerät merkt es sich) und sind sofort auf der Seite.
- **Einladungslink:** Ganz oben in den Optionen kopiert jeder mit einem Klick einen Einladungslink. Damit kommt man ohne Passwort auf den Server. Der Link gilt 24 Stunden, danach geht er nicht mehr (wer schon drin ist, bleibt drin).
- Jeder legt **seinen eigenen Spieler mit Foto** an (genau einen pro Gerät) und ist auf seinem Gerät automatisch dieser Spieler. Spieler für andere anlegen oder sich als fremder Spieler eintragen geht nicht.
- Oben links steht neben dem Logo, wie viele gerade **online** sind.
- **Quiz, Malen, Golf und Kartenwahn gehen jederzeit, auch ohne dich:** Unter „Spiele“ gibt es 3 Räume mit je bis zu 8 Spielern. Wer als Erster beitritt, ist Host: Er wählt Quiz, Malen oder Golf, stellt alles ein und startet. Die anderen sehen live mit. Im Quiz wählt, wer dran ist, das Feld und die Antwort selbst.
- Das Host-Gerät steuert Zeit und Ablauf. Geht der Host raus, übernimmt automatisch der Nächste im Raum. Ist das Host-Gerät länger weg (Handy aus), kann jemand „Host übernehmen“ drücken, nach 90 Sekunden passiert das automatisch. Der Host kann Spieler aus dem Raum nehmen.
- Links steht, wer gerade dran ist und wer danach kommt, rechts die Punkteführung, die sich live neu sortiert. 5 Sekunden nach jeder Antwort geht es automatisch weiter; mit **Anhalten** stoppt der Host das.

## Gut zu wissen

- **Passwort ändern** (Optionen → Turnier-Passwort): Alle Daten ziehen mit um, Gäste müssen danach einmal das neue Passwort eingeben.
- **Quiz-Themen:** Videospiele, Flaggen (mit Flaggenbild), Geschichte, Allgemeinwissen und Schätzfragen, je 20 Fragen pro Schwierigkeit. Bei Schätzfragen schiebt man einen Regler; richtig ist alles innerhalb der angezeigten Abweichung. Eigene Schätzfragen legst du im Quiz-Bereich unter „Schätzfragen“ an.
- **Acht Themen:** Vor jedem Quiz wählst du 3 bis 6 Themen fürs Spielbrett (Videospiele, Flaggen, Geschichte, Allgemeinwissen, Schätzfragen, Filme, Serien, Animes).
- **Spieleliste:** Hier steht, welche Spiele im Turnier vorkommen können, mit Status (geplant, vielleicht, gespielt, fällt raus), Art, Plattform, Modus, Spielerzahl, Dauer, Notizen und Cover-Bild. Die geplanten Spiele haben eine Reihenfolge (mit ↑ ↓ ändern), oben siehst du die geschätzte Spielzeit. Mit 🎡 landen Spiele im Zufallsrad. Gäste sehen die Liste, geben ihren Favoriten 🔥 Hype und können Spiele vorschlagen. Bei gespielten Spielen trägst du den Sieger ein.
- **Aufbau:** Main-Menü, Turnier (Highscore, Zufallsrad, Spieleliste), Spiele (Quiz, Malen), Spieler und Optionen. Turnier hat oben eine Auswahl seiner Unterseiten; die Seite merkt sich, welche du zuletzt offen hattest.
- **Main-Menü:** Begrüßung mit Pixel-Figuren, darunter groß der Turnier-Status, die Spiele und die Ankündigungen (die haben keinen eigenen Tab mehr). Den Turnier-Status stellst du im Main-Menü mit „✎ Status ändern“ ein: kein Turnier, geplant (Datum, optional Uhrzeit mit Countdown) oder läuft gerade. Ist die Startzeit erreicht, steht dort von allein „Das Turnier läuft!“; am nächsten Morgen springt es auf „Aktuell ist kein Turnier geplant“. Neue Ankündigungen legst du dort mit „+ Neue Ankündigung“ an.
- **Name:** Die Seite heißt Darkime. Das Turnier selbst hat einen eigenen Namen (Optionen → Name des Turniers), Standard ist „Darkime Turnier“.
- **Spiele-Tab:** Zeigt die 3 Räume: wer drin ist, wer Host ist und was gerade läuft. Wer in einem Raum ist, sieht oben eine Leiste mit dem Raum und „Verlassen“. Du als Spielleiter kannst jedem Raum zuschauen und einen hängenden Raum zurücksetzen. Punkte übernehmen kannst nur du.
- **Eigene Begriffe und Fragen** (Malen-Wörter, Schätzfragen) legst nur du an, sie gelten dann in allen Räumen.
- **Malen** (wie skribbl.io): Wer dran ist, wählt eins von 3 Wörtern und malt es, alle anderen raten im Chat. Die Wörter sind nach Schwierigkeit sortiert und farbig umrandet: Leicht (grün), Mittel (orange), Schwer (rot). Schwere Wörter zählen mehr (Mittel ×1,5, Schwer ×2). Einstellbar sind Runden (1 bis 10), Zeit pro Bild (30 bis 240 Sekunden), welche Schwierigkeiten vorkommen, Buchstaben-Tipps und die Reihenfolge. 174 Begriffe sind dabei, eigene kannst du pro Schwierigkeit ergänzen. Zum Malen gibt es Stift, Radierer, Füllen, Formen (gerade Linie, Rechteck, Quadrat, Kreis) sowie Zurück und Vor (auch Strg+Z / Strg+Y); das Bild lässt sich als JPG speichern. Am Ende gibt es eine Galerie, jedes Bild darin auch als JPG; die Plätze 1 bis 3 bekommen automatisch 3, 2 und 1 Punkt im Raum-Highscore. Das Host-Gerät steuert die Zeit.
- **Auf dem Handy:** Hältst du das Handy während eines Spiels quer, zeigt die Seite nur noch das Spiel (beim Malen links die Leinwand, rechts Wort, Werkzeuge und Chat; beim Quiz Spielbrett und Frage groß). Mit ☰ kommst du an das Menü. Auf Android gibt es zusätzlich „Vollbild und quer“. Dreht sich der Bildschirm nicht, ist am Handy die automatische Drehung aus (iPhone: Ausrichtungssperre im Kontrollzentrum, Android: „Automatisch drehen“). Wer beim Malen dran ist, bekommt die drei Wörter als großes Fenster, egal wo er gerade auf der Seite ist.
- **Flaggenbilder** kommen von flagcdn.com, die Geräte brauchen also Internet (das brauchen sie für die Datenbank sowieso).
- **Sprache:** Beim allerersten Besuch wählt jeder zuerst Deutsch oder English, noch vor dem Intro. Das Gerät merkt sich die Wahl; ändern kann man sie jederzeit unter Optionen (die sehen jetzt alle, Gäste finden dort Sprache und Hintergrundmusik). Auf Englisch ist die ganze Seite übersetzt, auch alle eingebauten Quizfragen und Malbegriffe. Beim Malen zählt ein Begriff auf Deutsch und auf Englisch, so können gemischte Runden zusammen spielen. Was ihr selbst schreibt (Ankündigungen, Spieleliste, eigene Fragen und Begriffe), bleibt, wie es geschrieben wurde.
- **Turniersiege:** Im Tab Spieler steht statt Platz und Punkten, wie oft jemand schon ein Turnier gewonnen hat. Du zählst die Siege auf der Spielerkarte mit + und − hoch oder runter. Platz und Punkte stehen weiter im Highscore.
- **Vollbild:** Oben rechts neben „Live“ schaltet ein Knopf die Seite in den Vollbild-Modus und wieder zurück (oder Esc); dasselbe geht in den Optionen. Auf dem iPhone kann Safari das nicht, dort erklärt die Option den Weg über „Zum Home-Bildschirm“.
- **Im Spiel** stecken Kopfzeile und Raum-Leiste im ☰-Menü oben links (dasselbe ☰ schließt es wieder), damit das Spiel den ganzen Bildschirm hat. Golf passt komplett auf einen Bildschirm, ohne Scrollen; am Handy ist die Bahn bildschirmfüllend, oben links sitzen nur ☰ (Menü) und 🏆 (Punktetafel und Host-Knöpfe).
- **Event-Countdown:** In den letzten 5 Stunden eines Countdowns aus den Ankündigungen (und noch 1 Stunde danach) steht er riesig ganz oben im Main-Menü, und die ganze Seite bekommt einen Neon-Sonnenuntergang-Look mit Palmen. Beim Anlegen eines Countdowns kannst du stattdessen „Normal“ wählen, dann bleibt nur ein schlichtes, dunkles Banner (so ist es beim Attack-on-Titan-3-Countdown). Mit dem Neon-Look läuft für alle die Synthwave-Musik „🌴 Neon Nights“ (wer sie während des Events umstellt oder stumm schaltet, behält das bis zum Ende); danach kommt wieder die eigene Musik. „Neon Nights“ bleibt danach als Musikstil zur Auswahl.
- **Spieler-Profile (Steam-Stil):** Im Tab „Spieler“ öffnet ein Tipp auf einen Spieler sein Profil: Kopfbereich mit Foto, Spruch, Status (online, offline oder „Im Spiel“, wenn er gerade in einem Raum spielt), „Dabei seit“, Level mit XP-Balken (XP für eingetragene, durchgespielte und 100-%-Spiele, Spielzeit, Screenshots, Clips und Turniersiege) und dem neuesten Abzeichen. Unter dem Namen (und auf jeder Spielerkarte in der Übersicht) stehen die Top 3 Lieblingsspiele: Jeder Spieler wählt im Spiel „Platz 1, 2 oder 3“, freie Plätze füllen die bestbewerteten Spiele. Darunter das Lieblingsspiel groß, Screenshot-Showcase, kürzliche Aktivität mit Achievement-Fortschritt und die ganze Spielebibliothek mit Filtern; daneben Zahlen, 16 Abzeichen und die Mitspieler mit Status. Unter der Spielerübersicht stehen die Top-Spiele der Gruppe und die neueste Aktivität. Jeder Spieler trägt seine Spiele ein: Cover-Bild, Plattform (bis zu 4), Spielart (Story/Einzelspieler, Online-Multiplayer, Koop, lokal zusammen), Genres (bis zu 4, z. B. Action, Rollenspiel, Soulslike, Rennspiel), Altersfreigabe (FSK/USK 0, 6, 12, 16, 18, als farbiges Schild auf dem Cover), Status (durchgespielt, am Spielen, abgebrochen, endlos), Achievements (alle, ein paar mit „x von y“, keine, gibt es nicht), Spielzeit (auch als „5.000+“, wenn man es nicht genau weiß), Fazit und eine Gesamtbewertung von 0 bis 10. Dazu optional Einzelwertungen für Gameplay, Grafik, Sounddesign, Story, Atmosphäre und Spielspaß. Tippt man auf die Bewertung, klappen die Einzelwertungen als Balken auf. Beim Spiel selbst kann der Spieler bis zu 12 Screenshots (Großansicht mit Blättern) und bis zu 4 Clips hinzufügen: entweder als Link (YouTube, Twitch und Streamable spielen direkt auf der Seite) oder hochgeladen (höchstens 60 Sekunden; größere Clips werden im Browser verkleinert und in Teilen gespeichert, sie laden erst beim Abspielen). Im Profil kann man nach Status und Genre filtern, oben steht das Lieblingsgenre. Jeder kann alle Profile ansehen; eintragen, ändern und löschen kann nur der Spieler selbst auf seinem Gerät, auch der Spielleiter nicht die Spiele anderer. Die Datenbank-Regeln prüfen dafür den geheimen Schlüssel des Spielers; einen vorhandenen Schlüssel kann auch der Spielleiter nicht austauschen. Dafür braucht es die neuen Datenbank-Regeln (Abschnitt `vg` in firestore.rules).
- **Raum-Highscore:** Jeder der 3 Räume hat seinen eigenen Highscore. Am Ende jedes Spiels trägt das Host-Gerät die Punkte automatisch ein (Quiz: die Quizpunkte, Malen und Golf: 3, 2 und 1 Punkt für die Plätze 1 bis 3). In der Raum-Leiste öffnet „🏆 Highscore“ die Liste; du als Spielleiter kannst sie zurücksetzen. Der Highscore im Tab Turnier gehört nur zum Turnier, Spiele schreiben dort nichts mehr hinein.
- **Kartenwahn:** Das klassische Ablegespiel (Regeln wie beim bekannten Kartenspiel, eigenes Design im Pixel-Look der Seite) als viertes Spiel in den Räumen, für 2 bis 8 Spieler. 108 Karten in Rot, Gelb, Grün und Blau mit Aussetzen, Richtungswechsel, +2, Farbwahl und Farbwahl +4. Wer nur noch 2 Karten hat, drückt „Letzte Karte!“, sonst können die anderen „Erwischt!“ drücken (2 Karten ziehen). Der Host stellt Startkarten (5, 7, 10), Zeit pro Zug (15, 30, 60 Sekunden oder ohne) und zwei Hausregeln ein: +2/+4 stapeln und ziehen, bis eine Karte passt. Läuft die Zeit ab, zieht das Spiel automatisch. Der Spieltisch füllt den ganzen Bildschirm, am Handy mit Karten zum Antippen und kompakten Gegner-Kacheln. Das Host-Gerät prüft jeden Zug, verlässt jemand den Raum, gehen seine Karten zurück in den Stapel. Am Ende bekommen Platz 1 bis 3 automatisch 3, 2 und 1 Punkt im Raum-Highscore. Im Querformat (Handy quer, PC) stehen die Gegner links, der Tisch in der Mitte und Status, Farbe und Knöpfe rechts, die Hand unten. Karten fliegen beim Austeilen, Legen und Ziehen im Bogen über den Tisch und drehen sich dabei um. „Letzte Karte!“ muss man spätestens 3 Sekunden nach dem Legen der vorletzten Karte drücken, sonst zieht man automatisch 2 Karten.
- **Bots:** Der Host holt in der Raum-Leiste mit „🤖 Bot dazu“ Computer-Mitspieler dazu (Leicht, Mittel oder Schwer), solange gerade kein Spiel läuft. Bots belegen einen Platz im Raum (zusammen höchstens 8) und spielen Kartenwahn (mit Strategie, rufen „Letzte Karte!“ und erwischen Vergessliche), Golf (mit derselben Physik, ihre Bälle rollen sichtbar), Quiz (Trefferquote je nach Stufe) und raten beim Malen mit (malen selbst nicht). Gesteuert werden sie vom Gerät des Hosts. Punkte im Raum-Highscore bekommen Bots nicht. So kann man jedes Spiel auch allein testen, am Handy wie am PC. Geht der letzte Mensch, verschwinden auch die Bots.
- **Golf:** Minigolf in 3D als drittes Spiel in den Räumen. Gespielt wird von unten nach oben, die Kamera folgt dem Ball (er bleibt knapp unter der Bildmitte, damit man genug Platz zum Ziehen hat); am Anfang jeder Bahn fliegt sie einmal vom Loch zum Abschlag, und oben rechts zeigt eine kleine Karte die ganze Bahn. 30 Bahnen: die ersten kurz und leicht, danach wird jede ein Stück länger (bis etwa 330 m) und hat mehr Kurven, Blöcke, Bumper, Sand, Wasser, Hänge, Windmühlen und Schiebeblöcke. Ab Bahn 21 kommen Löcher im Boden (durchfallen kostet einen Strafschlag), Drehscheiben am Boden, die den Ball mitschleudern, schnellere Hindernisse. Zielen mit Maus oder Finger: aufs Feld drücken, nach hinten ziehen, loslassen. Alle spielen gleichzeitig und sehen die Bälle der anderen rollen. Wer eingelocht hat, schaut den anderen zu und kann rechts unter der Punktetafel mit ◀ ▶ (oder per Klick auf einen Namen) wechseln. Sind alle eingelocht, läuft ein 3-Sekunden-Countdown bis zur nächsten Bahn. Der Host wählt alle 30 Bahnen, Leicht (1–10), Mittel (11–20), Extrem (21–30) oder eine schnelle Runde mit 6 zufälligen Bahnen, und kann ohne Wartende weiter oder beenden. Wenigste Schläge gewinnen, höchstens Par + 6 pro Bahn; die Plätze 1 bis 3 bekommen automatisch 3, 2 und 1 Punkt im Raum-Highscore.
- **Eigenen Spieler ändern:** Wer seinen Spieler selbst erstellt hat, kann ihn im Tab Spieler jederzeit bearbeiten (Foto, Name, Farbe, Schrift, Spruch), und zwar auf dem Gerät, mit dem er ihn erstellt hat. Dafür bekommt jeder Spieler beim Erstellen einen geheimen Schlüssel, den nur dieses Gerät kennt; die Datenbank-Regeln lassen Änderungen nur damit zu. Turniersiege kann nur der Spielleiter ändern, und der Spielleiter kann weiterhin alle Spieler bearbeiten. Ältere Gast-Spieler ohne Schlüssel bekommen beim ersten Bearbeiten einen, auf dem Gerät, das gerade als dieser Spieler eingestellt ist.
- **Spieler gestalten:** Foto zuschneiden (ziehen und zoomen), Schriftart, Farbverlauf, Rahmen und ein kurzer Spruch. Das geht auch für Gäste, die ihren Spieler selbst anlegen.
- **Hintergrundmusik:** Die Seite erzeugt selbst leichte Musik (Chill, Arcade, Weltraum). Jeder stellt sie über den ♪-Knopf unten rechts lauter, leiser oder stumm. Unter Optionen legst du fest, ob sie bei Gästen standardmäßig an ist.
- **Eigene Bilder** (Optionen): fliegen auf Wunsch dezent über die ganze Seite.
- **Wartebildschirm** (mit Laufschrift und fliegenden Bildern): ist vorerst ausgeschaltet, der Code ist noch da. Zum Wiedereinschalten in `index.html` `const LOBBY = false;` auf `true` setzen.
- **Quiz-Musik** wird nur auf dem Gerät gespeichert, auf dem du sie auswählst. Nimm das Gerät, das an den Lautsprechern hängt.
- **Kosten:** Der kostenlose Firebase-Tarif (Spark) reicht für so ein Turnier locker aus.
- **Abmelden** als Spielleiter: ganz unten auf der Seite.
- Daten aus der alten Claude-Version werden nicht automatisch übernommen. Spieler und eigene Quizfragen trägst du einmal neu ein.

## Turnier-Vorschau (Wartebildschirm)

Solange kein Turnier läuft (Status nicht „Läuft gerade“ und kein Turnier heute), zeigt der Tab „Turnier“ allen den **Wartebildschirm im TV-Look** („Gleich geht’s los!“ mit Scheinwerfern, „Live in Kürze“, Uhr, Laufschrift und fliegenden Bildern aus den Optionen), mit Termin und Countdown, wenn einer eingetragen ist. Highscore, Zufallsrad und Spieleliste sind so lange nicht erreichbar. Der Spielleiter sieht denselben Bildschirm mit **„Turnier bearbeiten“** (alles einrichten, die Spieler sehen weiter den Wartebildschirm) und **„Jetzt für alle starten“**.

Ganz oben in **Optionen** gibt es die Karte **„🏆 Turnier“** mit vier Stufen:
- **Kein Turnier geplant:** Wartebildschirm „Aktuell kein Turnier“, Laufschrift „Aktuell ist kein Turnier geplant“ (Standard).
- **Bald (noch ohne Termin):** „Gleich geht’s los!“ und „Live in Kürze“, ohne Countdown.
- **Termin mit Countdown:** Datum und Uhrzeit; überall läuft ein Countdown bis zum Start.
- **Läuft gerade:** Turnier-Tab für alle offen.

„Wartebildschirm ansehen“ zeigt dem Spielleiter den Bildschirm so, wie ihn die Spieler sehen. Die Laufschrift-Meldung „Heute im Studio“ gibt es nicht mehr.

## Uncle Grandpa ärgere dich

Brettspiel für 2 bis 4 Spieler in den Spiele-Räumen (Regeln wie beim bekannten Klassiker: mit 6 raus, nach 6 nochmal, Startfeld räumen, rauswerfen, exakt ins Ziel). Host-Einstellungen: Zeit pro Zug, Schnellstart, Schlagzwang. Bots spielen mit (leicht, mittel, schwer). Platz 1 bis 3 bekommen 3, 2 und 1 Punkt im Raum-Highscore. Der Spielstand liegt im Raum-Feld `uno` mit `g:'mad'`, deshalb braucht es keine neuen Firebase-Regeln.

## Blackjack

Raum-Spiel für 1 bis 8 Spieler gegen die Bank (das Gerät des Hosts ist die Bank). Start-Chips einstellbar (500 bis 10.000, Standard 2000), 5, 10 oder 20 Runden. Karte, Bleiben, Verdoppeln, Teilen (einmal, geteilte Asse bekommen eine Karte). Bank zieht bis 16, bleibt ab 17. Blackjack zahlt 3:2. Bots spielen mit (schwer = Grundstrategie). Platz 1 bis 3 nach Chips bekommen ab 2 Spielern 3, 2 und 1 Punkt. Spielstand im Raum-Feld `uno` mit `g:'bj'`.

## Dicktris

Fallende-Blöcke-Spiel im Raum: alle spielen gleichzeitig auf ihrem eigenen Feld (PC: Pfeiltasten, Leertaste, C; Handy: Wischen und Knöpfe). Modi Battle (ab 2 Reihen bekommen die anderen Müllzeilen) und Klassisch, Dauer 2/3/5 Minuten oder bis alle raus sind, Start-Level einstellbar. Mini-Felder der anderen live. Jeder schreibt nur `uno.p.<Spieler>` (alle 2 Sekunden und bei Reihen/Raus). Platz 1 bis 3 nach Punkten ab 2 Spielern in den Raum-Highscore.

## Designs

In **Optionen → 🎨 Design** wählt der Spielleiter das Design der Webseite für alle: **Arcade (Pixel)** oder **Neon-Glas** (Standard). Neues Design: Eintrag in `DESIGNS` (index.html) und ein CSS-Block mit `html[data-design="id"]`.

## Turnier-Check-in

Sobald das Turnier läuft („Läuft gerade“ oder Termin erreicht), sehen alle im Turnier-Tab zuerst den Check-in: „✅ Ich bin dabei!“ und eine Liste, wer schon da ist und wer noch fehlt. Der Spielleiter bestätigt mit „✅ Alle da: Turnier starten“ (speichert `settings.chk`). Danach sieht jeder einmal die Übersicht mit den Spielen aus dem Zufallsrad und dem Preisgeld pro Platz, dann ist das Turnier offen. Check-ins liegen als `presence/chk_<Turnier>_<Spieler>`, deshalb braucht es keine neuen Firebase-Regeln.

## Private Räume

Der Host kann seinen Raum in der Raum-Leiste mit **„🔓 Öffentlich“ / „🔒 Privat“** umschalten. Bei „Privat“ lädt er über **„💌 Einladen“** Spieler ein (wer schon im Raum ist, ist automatisch eingeladen). Alle anderen sehen den Raum mit 🔒 und können weder beitreten noch zuschauen; Eingeladene sehen „Du bist eingeladen“. Wer rausgeworfen wird, verliert seine Einladung. Verlässt der Letzte den Raum oder ist der Host 10 Minuten weg, ist der Raum wieder offen. Die Firestore-Regeln prüfen das ebenfalls (nach dem Veröffentlichen der Regeln).

## Spielmodus und Teams
Unter Optionen → 👥 Spielmodus stellt der Spielleiter ein: Alle gegen alle, Duos, Trios oder Squads (4er).
Im Team-Modus werden die Teams ausgelost (unter allen, die beim Check-in dabei sind) und können danach per Tippen
getauscht, verschoben und umbenannt werden. Highscore, Siegertreppchen und Preisgeld gelten dann pro Team.
Teams stehen in `meta/settings` (`fmt`, `teams`), Team-Punkte als Punkte-Einträge mit `playerId: "T:<teamId>"`.

Ins Zufallsrad können auch die Server-Spiele (Quiz, Minigolf, Blackjack usw.) aufgenommen werden. Jedes Spiel im Rad
ist im Team-Modus als „Team“ oder „Solo“ markiert. Punkte vergibt der Spielleiter wie gewohnt mit +/−.

## Turnier-Lobby
Zieht das Zufallsrad im laufenden Turnier ein Server-Spiel, legt der Admin automatisch die eigene Turnier-Lobby `rt` an
(zusätzlich zu Raum 1 bis 3, angezeigt als „🏆 Turnier-Lobby“). Sie ist immer privat, eingeladen sind nur die Check-in-Spieler,
der Admin ist Host. In der Raumliste sehen sie nur die Eingeladenen und der Admin. `settings.tgo = {id, room, kind, go}`:
Erst wenn der Admin am Rad auf „🏆 Alle rüber“ klickt, wird `go` gesetzt und alle Turnier-Spieler wechseln gleichzeitig.
Nochmal klicken holt Nachzügler. Die Firestore-Regel erlaubt `rt` nur dem Admin zum Anlegen und hält sie privat.
Ist die neue Regel noch nicht veröffentlicht, nimmt der Admin wie früher einen freien Raum 1 bis 3.
Bei Tischtennis/Air-Hockey wählt der Host dort 2 Spieler aus, die anderen schauen zu. „Turnier stoppen“ leert die Lobby.


## User-ID (Handy und PC)
Jeder Spieler hat eine User-ID (16 Zeichen, z. B. `K7QD-M2XA-9PRT-HW4C`). Am Spieler steht nur ihr SHA-256 (`kh`), die ID selbst in
`rooms/{raum}/pk/{spieler}` – lesen darf das nur der Admin. Wer etwas Geschütztes ändert (Profil, Videogames, Tickets), schreibt im selben
Vorgang `pk` mit `t = Serverzeit`; die Regel prüft, dass der Hash der ID zu `kh` passt (`pkOk`). Die ID wechselt dabei nicht, deshalb
klappt es auf mehreren Geräten. Im eigenen Profil sieht man die eigene ID (Zeigen/Kopieren), auf einem anderen Gerät gibt man sie ein
(„Mit deiner User-ID verbinden“, auch unter Spieler ohne eigenen Spieler). Admin: Optionen → User-IDs zeigt alle, „Neu vergeben“ macht die
alte ungültig. Alte Geräte-Schlüssel (48 Hex-Zeichen, wechselten bei jedem Speichern) werden beim nächsten Speichern zu einer User-ID.
## Klick-Sounds
Leise Bestätigungstöne für Knöpfe, Reiter und Auswahl-Chips (eigene Töne für Reiter, An/Aus, Hauptknöpfe und Schließen).
Während eines laufenden Spiels bleiben sie still. Pro Gerät abschaltbar unter Optionen → Musik und Sounds (`turnier-uisnd`).

## Bowling
🎳 Bowling für alle im Raum (auch Bots), 3, 5 oder 10 Frames, echte Bowling-Wertung mit Strike, Spare und Extrawurf im letzten Frame.
Werfen wie beim Minigolf: Kugel nach unten ziehen und loslassen (Länge = Kraft, schräg = Richtung), Effet per Auswahl unter der Bahn. Wer dran ist, rechnet den Wurf
mit fester Physik durch und schreibt Wurf + Ergebnis + neuen Stand auf einmal (`uno` mit `g:'bw'`); alle spielen ihn als Animation ab.
Frames werden als Map gespeichert (`{"0":[…]}`), weil Firestore keine Listen in Listen erlaubt. Nach 45 s ohne Wurf wirft der Host automatisch.
Physik: Die Kugel rutscht vorne auf dem Öl fast gerade und hakt hinten auf trockenem Holz (Effet), dabei wird sie etwas langsamer.
Pins kippen in Stoßrichtung um und sind beim Kippen/Liegen ein Stab, der Nachbarn mitreißt; harte Treffer lassen sie springen und drehen,
an den Seitenwänden prallen sie zurück, leichte Stöße lassen sie nur wackeln. Alles in festen Schritten, damit alle Geräte dasselbe sehen.


## Schach
Raumspiel `ch` (im Feld `uno`, g:'ch'), 1 gegen 1 wie Tischtennis/Air-Hockey: Sind mehr im Raum, wählt der Host 2 aus, der Rest schaut zu.
Farben werden ausgelost, Revanche tauscht sie. Brett als 64-Zeichen-Text (`b`), Züge als „e2e4“ (`h`), Uhr optional (3/5/10/15 Min, `tl`/`at`).
Alle Regeln (Rochade, en passant, Umwandlung mit Auswahl, Matt, Patt, 50 Züge, dreifache Wiederholung, zu wenig Material,
Aufgeben, Remis anbieten). Die Zuggenerierung ist mit Perft-Stellungen geprüft. Bot (Host): Alpha-Beta mit Feldtabellen,
leicht/mittel/schwer = Tiefe 1/2/3, höchstens 0,8 s pro Zug. Highscore: Sieg +3, Niederlage +1, Remis je +2.

## Wer wird der nächste ApoRed?
Raumspiel `ap` (Feld `uno`, g:'ap'), alle im Raum spielen gleichzeitig dieselben 30 Fragen (aus `BANK`, Kategorien Games/Geschichte/
Wissen/Filme/Serien/Anime; 6 Stufen zu je 5 Fragen: sehr leicht, leicht, mittel, schwer, sehr schwer, Profi). Dazu kommen 180 eigene ApoRed-Fragen in `AP_QB` (30 pro Stufe, Schlüssel `9.<Stufe>.<Nr>`); in der Profi-Stufe sind 3 von 5 Fragen aus `AP_QB[5]`. Das startende Gerät merkt sich gespielte Fragen (`localStorage.apSeen`) und nimmt erst ungespielte. Geldleiter 25 € bis 1 Mio, Sicherheitsstufen 1.000 € (Frage 10) und 32.000 € (Frage 20),
Bestätigen per Doppelklick/doppelt tippen auf die Antwort, Aussteigen nur auf den Sicherheitsstufen (Frage 10 und 20), Joker 50:50 / Publikum / Telefon (fest aus der Frage berechnet). Beim Telefon-Joker werden 2 von 10 Personen ausgelost, man ruft eine davon an; Name und Bild der 10 Personen stellt der Spielleiter unter Optionen → Spiele ein (`rooms/{room}/media/ap_phone`). Mit 10 % taucht als dritte Person der Witz-Anrufer „ApoRed“ auf (höchstens einmal pro Spiel und Spieler); er zeigt Text oder ein MP4 (`media/ap_vid`, bis 10 MB), währenddessen steht die Zeit, danach geht es mit den 2 normalen Personen weiter. Optional 30 oder 60 s pro Frage.
Jeder schreibt nur `uno.pr.<id>` = {lv, st, at, jf/jp/jt}; die anderen sehen nur Stufe und Status, nie die Frage. Bots spielt der Host.
Highscore nach Gewinn: 1. +3, 2. +2, alle weiteren mit Gewinn +1.
Musik: Der Admin lädt unter Optionen → Musik eine MP3 (bis 8 MB) hoch. Sie liegt Base64 in Stücken in `rooms/{raum}/media`
(`apored` = Infos, `apored_0…` = Daten), jedes Gerät lädt sie einmal und speichert sie in IndexedDB. Läuft bei allen, solange das Spiel läuft;
🔊/🔇 oben im Spiel schaltet sie pro Gerät stumm.

## Air-Hockey und 2er-Spiele
🏒 Air-Hockey: 1 gegen 1 (auch gegen einen Bot), bis 5, 7 oder 10 Tore. Gespeichert im Raum-Feld `uno` mit `g:'ah'`.
Der Puck läuft auf jedem Gerät mit festen Rechenschritten gleich weiter. Treffer und Tore auf einer Hälfte schreibt nur deren
Besitzer (bei Bots der Host) als neues Puck-Ereignis. Tischtennis und Air-Hockey sind 2er-Spiele: Sind mehr als 2 im Raum, wählt der Host aus,
wer gegeneinander spielt; die anderen schauen zu.

## Pause in Raum-Spielen
In jedem laufenden Raum-Spiel gibt es rechts unten einen Pause-Knopf (für alle Mitspieler). Die Pause steht im Spiel-Objekt
als `pz = {at, by, auto}`. Während der Pause laufen keine Zeiten, Host-Abläufe oder Bots; beim Weiterspielen werden die
gespeicherten Zeitpunkte und die Zähler auf jedem Gerät um die Pausenlänge verschoben.
Spielt man allein (nur Bots oder Solo), pausiert das Spiel automatisch, sobald man die Seite verlässt (z. B. für WhatsApp).

## Tischtennis
Raum-Spiel 🏓 für 1 gegen 1 (auch gegen einen Bot), bis 5, 11 oder 21 Punkte. Gespeichert im Raum-Feld `uno` mit `g:'tt'`.
Jeder Schlag ist ein einziger Schreibvorgang. Der Ball startet auf jedem Gerät, sobald es den Schlag sieht; ob er zurückkommt,
entscheidet das Gerät des Annehmenden (bei Bots der Host). Sieger +3, Verlierer +1 im Raum-Highscore.

## Geburtstage
Jedes neue Konto muss seinen Geburtstag (Tag, Monat, Jahr) angeben; bestehende Spieler werden beim nächsten Besuch einmal danach gefragt.
Hat jemand Geburtstag (deutsche Zeit, 29.2. in normalen Jahren am 28.2.), feiert die ganze Seite: bunter Banner, Ballons, Konfetti, Partyfarben.
Weil die Firestore-Regeln kein eigenes Feld erlauben, hängt das Datum hinten an `shape` (z. B. `oval~20000314`).
Vorschau für den Spielleiter: Optionen → Aussehen → 🎂 Geburtstage.

## Rauswurf bei Inaktivität
Wer in einer Lobby eine bestimmte Zeit nichts tut (kein Tippen, Klicken, keine Taste), verlässt sie automatisch.
Eine Minute vorher kommt „Bist du noch da?“. Die Zeit (1–30 Minuten, Standard 30) stellt der Spielleiter unter
Optionen → ⏱️ Rauswurf aus der Lobby ein (`meta/settings.afk`).

## Spieler-Ansicht für den Spielleiter

Unten links gibt es für den Spielleiter den Knopf **„Spieler-Ansicht“**. Damit sieht er die Seite so, wie ein normaler Spieler sie sieht (ohne Admin-Knöpfe, Support als Spieler, Sperrbildschirm vor dem Turnierstart usw.). Ein gelber Streifen oben zeigt, dass die Spieler-Ansicht an ist; „Admin-Ansicht“ schaltet zurück. Es erscheinen dabei keine Hinweis-Meldungen. Angemeldet bleibt man dabei als Spielleiter. In laufenden Spielen ist der Knopf ausgeblendet. Nach dem Neuladen ist wieder die Admin-Ansicht an.

## Support

Eigener Tab „Support“ (links neben „Optionen“). Spieler schreiben dort Tickets in einem Assistenten mit 4 Schritten:
1. **Art:** Fehler, Idee, Verbesserung, Frage oder Sonstiges.
2. **Bereich:** 16 Bereiche (z. B. Minigolf, Kartenwahn, Profile, Handy-Ansicht), dazu passende Unterpunkte, bei Minigolf die Bahn (1 bis 30) und ein freies Feld „Wo genau?“. Kommt man aus einem Spiel in den Support, ist der Bereich (und bei Minigolf die Bahn) schon vorgeschlagen.
3. **Details:** Titel und Beschreibung; bei Fehlern Schritte zum Nachstellen, „Was hätte passieren sollen?“, wie oft und wie schlimm; bei Ideen und Verbesserungen „Warum wäre das gut?“ und wie wichtig.
4. **Bilder und Absenden:** bis zu 3 Screenshots, auf Wunsch technische Infos (Gerät, System, Browser, Fenstergröße), Vorschau des Tickets.

Angefangene Tickets werden als Entwurf gespeichert. Spieler sehen „Meine Tickets“, ein Ideen-Board und bekannte Fehler, können für fremde Ideen und Fehler stimmen („Will ich auch“ / „Passiert mir auch“), eigene Tickets ergänzen oder zurückziehen. Der Spielleiter sieht alle Tickets mit Zählern, Filtern (Status, Art, Bereich), Suche und Sortierung (z. B. „Dringlichste“), setzt den Status (Neu, In Bearbeitung, Erledigt, Abgelehnt) und antwortet, auch mit Schnellantworten. Neue Antworten und neue Tickets zeigt eine Zahl am Tab.

## Dauerlink für Discord

Unter „Optionen“ kann der Spielleiter einen **Dauerlink** erstellen. Er läuft nie ab (bis 2100), bringt neue und alte Spieler ohne Passwort direkt auf den Server und zeigt nach einem Passwortwechsel automatisch auf den neuen Server. „Neuen Link erstellen“ oder „Sperren“ macht den alten Link sofort ungültig. Beim Posten in Discord erscheint eine Vorschau mit Titel und Bild (og.png).

## Noch offen (am PC erledigen)

- Die aktuelle `firestore.rules` in der Firebase-Konsole veröffentlichen (Abschnitte `vg`, `vgm`, `vgp`, die Änderung bei `players`, der Dauerlink bei `invites` und `admin/invite`, Support bei `tickets` und `tkimg`). Vorher können Spieler keine eigenen Spiele, Screenshots oder Clips eintragen, der Dauerlink lässt sich nicht erstellen, und Spieler können keine Support-Tickets schreiben.

## Quiz-Fragen

Themen in `CATS` (Index): 0 Videospiele, 1 Flaggen, 2 Geschichte, 3 Allgemeinwissen, 4 Schätzfragen, 5 Filme, 6 Serien, 7 Animes, 8 Deutschland (`GERMANY`, 5 × 30). Weitere Fragen stehen in `QUIZ_MORE` und `FLAGS_MORE` und werden hinten an `BANK` angehängt, damit alte IDs (`v3-Thema-Stufe-Nr`) gleich bleiben. Die 180 ApoRed-Fragen (`AP_QB`) kommen im Quiz mit Thema aus `AP_QB_CAT` dazu (IDs `ap-Stufe-Nr`). Jedes Thema hat pro Stufe mindestens 30 Fragen. Schon gestellte Fragen merkt sich das Quiz in `seen` und nimmt erst ungestellte.
