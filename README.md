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
- Sie können **eigene Spieler mit Foto** anlegen. Die erscheinen sofort bei allen.
- Wer seinen Spieler selbst anlegt, ist auf seinem Handy automatisch dieser Spieler. Hat der Spielleiter den Spieler angelegt, tippt man einmal im Tab „Spieler“ bei seinem Namen auf „Das bin ich“.
- **Quiz, Malen und Golf gehen jederzeit, auch ohne dich:** Unter „Spiele“ gibt es 3 Räume mit je bis zu 8 Spielern. Wer als Erster beitritt, ist Host: Er wählt Quiz, Malen oder Golf, stellt alles ein und startet. Die anderen sehen live mit. Im Quiz wählt, wer dran ist, das Feld und die Antwort selbst.
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
- **Spiele-Tab:** Zeigt die 3 Räume: wer drin ist, wer Host ist und was gerade läuft. Wer in einem Raum ist, sieht oben eine Leiste mit dem Raum und „Verlassen“. Du als Spielleiter kannst jedem Raum zuschauen, Punkte eines fertigen Spiels in die Highscore übernehmen und einen hängenden Raum zurücksetzen. Punkte übernehmen kannst nur du.
- **Eigene Begriffe und Fragen** (Malen-Wörter, Schätzfragen) legst nur du an, sie gelten dann in allen Räumen.
- **Malen** (wie skribbl.io): Wer dran ist, wählt eins von 3 Wörtern und malt es, alle anderen raten im Chat. Die Wörter sind nach Schwierigkeit sortiert und farbig umrandet: Leicht (grün), Mittel (orange), Schwer (rot). Schwere Wörter zählen mehr (Mittel ×1,5, Schwer ×2). Einstellbar sind Runden (1 bis 10), Zeit pro Bild (30 bis 240 Sekunden), welche Schwierigkeiten vorkommen, Buchstaben-Tipps und die Reihenfolge. 174 Begriffe sind dabei, eigene kannst du pro Schwierigkeit ergänzen. Am Ende gibt es eine Galerie; auf deinen Wunsch gehen die Plätze 1 bis 3 mit 3, 2 und 1 Punkt in die Highscore. Das Host-Gerät steuert die Zeit.
- **Auf dem Handy:** Hältst du das Handy während eines Spiels quer, zeigt die Seite nur noch das Spiel (beim Malen links die Leinwand, rechts Wort, Werkzeuge und Chat; beim Quiz Spielbrett und Frage groß). Mit ☰ kommst du an das Menü. Auf Android gibt es zusätzlich „Vollbild und quer“. Dreht sich der Bildschirm nicht, ist am Handy die automatische Drehung aus (iPhone: Ausrichtungssperre im Kontrollzentrum, Android: „Automatisch drehen“). Wer beim Malen dran ist, bekommt die drei Wörter als großes Fenster, egal wo er gerade auf der Seite ist.
- **Flaggenbilder** kommen von flagcdn.com, die Geräte brauchen also Internet (das brauchen sie für die Datenbank sowieso).
- **Sprache:** Beim allerersten Besuch wählt jeder zuerst Deutsch oder English, noch vor dem Intro. Das Gerät merkt sich die Wahl; ändern kann man sie jederzeit unter Optionen (die sehen jetzt alle, Gäste finden dort Sprache und Hintergrundmusik). Auf Englisch ist die ganze Seite übersetzt, auch alle eingebauten Quizfragen und Malbegriffe. Beim Malen zählt ein Begriff auf Deutsch und auf Englisch, so können gemischte Runden zusammen spielen. Was ihr selbst schreibt (Ankündigungen, Spieleliste, eigene Fragen und Begriffe), bleibt, wie es geschrieben wurde.
- **Turniersiege:** Im Tab Spieler steht statt Platz und Punkten, wie oft jemand schon ein Turnier gewonnen hat. Du zählst die Siege auf der Spielerkarte mit + und − hoch oder runter. Platz und Punkte stehen weiter im Highscore.
- **Golf:** Minigolf in 3D als drittes Spiel in den Räumen. Gespielt wird von unten nach oben, die Kamera folgt dem Ball; am Anfang jeder Bahn fliegt sie einmal vom Loch zum Abschlag, und oben rechts zeigt eine kleine Karte die ganze Bahn. 20 Bahnen: die ersten kurz und leicht, danach wird jede ein Stück länger (bis etwa 230 m) und hat mehr Kurven, Blöcke, Bumper, Sand, Wasser, Hänge, Windmühlen und Schiebeblöcke. Zielen mit Maus oder Finger: aufs Feld drücken, nach hinten ziehen, loslassen. Alle spielen gleichzeitig; sind alle eingelocht, kommt nach ein paar Sekunden die nächste Bahn. Der Host wählt alle 20 Bahnen, Leicht (1–7), Mittel (8–14), Schwer (15–20) oder eine schnelle Runde mit 6 zufälligen Bahnen, und kann ohne Wartende weiter oder beenden. Wenigste Schläge gewinnen, höchstens Par + 6 pro Bahn; die Plätze 1 bis 3 kannst du mit 3, 2 und 1 Punkt in die Highscore übernehmen.
- **Eigenen Spieler ändern:** Wer seinen Spieler selbst erstellt hat, kann ihn im Tab Spieler jederzeit bearbeiten (Foto, Name, Farbe, Schrift, Spruch), und zwar auf dem Gerät, mit dem er ihn erstellt hat. Dafür bekommt jeder Spieler beim Erstellen einen geheimen Schlüssel, den nur dieses Gerät kennt; die Datenbank-Regeln lassen Änderungen nur damit zu. Turniersiege kann nur der Spielleiter ändern, und der Spielleiter kann weiterhin alle Spieler bearbeiten. Ältere Gast-Spieler ohne Schlüssel bekommen beim ersten Bearbeiten einen, auf dem Gerät, das gerade als dieser Spieler eingestellt ist.
- **Spieler gestalten:** Foto zuschneiden (ziehen und zoomen), Schriftart, Farbverlauf, Rahmen und ein kurzer Spruch. Das geht auch für Gäste, die ihren Spieler selbst anlegen.
- **Hintergrundmusik:** Die Seite erzeugt selbst leichte Musik (Chill, Arcade, Weltraum). Jeder stellt sie über den ♪-Knopf unten rechts lauter, leiser oder stumm. Unter Optionen legst du fest, ob sie bei Gästen standardmäßig an ist.
- **Eigene Bilder** (Optionen): fliegen auf Wunsch dezent über die ganze Seite.
- **Wartebildschirm** (mit Laufschrift und fliegenden Bildern): ist vorerst ausgeschaltet, der Code ist noch da. Zum Wiedereinschalten in `index.html` `const LOBBY = false;` auf `true` setzen.
- **Quiz-Musik** wird nur auf dem Gerät gespeichert, auf dem du sie auswählst. Nimm das Gerät, das an den Lautsprechern hängt.
- **Kosten:** Der kostenlose Firebase-Tarif (Spark) reicht für so ein Turnier locker aus.
- **Abmelden** als Spielleiter: ganz unten auf der Seite.
- Daten aus der alten Claude-Version werden nicht automatisch übernommen. Spieler und eigene Quizfragen trägst du einmal neu ein.
