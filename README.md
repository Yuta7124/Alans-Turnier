# Alans Turnier

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

- Sie öffnen den Link, geben einmal das Turnier-Passwort ein (ihr Gerät merkt es sich) und landen im Wartebildschirm, bis du die Lobby öffnest.
- Sie können **eigene Spieler mit Foto** anlegen. Die erscheinen sofort bei allen.
- Im Quiz tippen sie unten bei „Wer bist du?“ auf ihren Namen. Nur wer dran ist, **wählt das Feld und die Antwort selbst**, das zählt sofort. Alle anderen schauen zu.
- Links steht, wer gerade dran ist und wer danach kommt, rechts die Punkteführung, die sich live neu sortiert.
- 5 Sekunden nach jeder Antwort geht es automatisch zurück zum Spielbrett und der nächste Spieler ist dran. Mit **Anhalten** stoppst du das, mit **Sofort weiter** geht es direkt weiter.
- Wichtig: Die Antworten der Gäste und das automatische Weiter laufen über dein Spielleiter-Gerät. Lass die Seite dort während des Quiz offen.

## Gut zu wissen

- **Passwort ändern** (Optionen → Turnier-Passwort): Alle Daten ziehen mit um, Gäste müssen danach einmal das neue Passwort eingeben.
- **Quiz-Themen:** Videospiele, Flaggen (mit Flaggenbild), Geschichte, Allgemeinwissen und Schätzfragen, je 20 Fragen pro Schwierigkeit. Bei Schätzfragen schiebt man einen Regler; richtig ist alles innerhalb der angezeigten Abweichung. Eigene Schätzfragen legst du im Quiz-Bereich unter „Schätzfragen“ an.
- **Neun Themen:** Vor jedem Quiz wählst du 3 bis 6 Themen fürs Spielbrett (Videospiele, Flaggen, Geschichte, Allgemeinwissen, Schätzfragen, Videospiel-Soundtracks, Filme, Serien, Animes).
- **Videospiel-Soundtracks:** Hier legst du die Clips selbst an (Quiz → Eigene Fragen → Videospiel-Soundtracks): Audiodatei wählen, Startpunkt einstellen, 10 Sekunden werden automatisch herausgeschnitten, dazu drei Spiele als Antworten. Auf dem Spielleiter-Gerät startet der Clip automatisch, Gäste können ihn zusätzlich auf dem Handy anhören. Für jede Schwierigkeit mindestens ein Clip, sonst bleibt das Feld leer.
- **Flaggenbilder** kommen von flagcdn.com, die Geräte brauchen also Internet (das brauchen sie für die Datenbank sowieso).
- **Spieler gestalten:** Foto zuschneiden (ziehen und zoomen), Schriftart, Farbverlauf, Rahmen und ein kurzer Spruch. Das geht auch für Gäste, die ihren Spieler selbst anlegen.
- **Hintergrundmusik:** Die Seite erzeugt selbst leichte Musik (Chill, Arcade, Weltraum). Jeder stellt sie über den ♪-Knopf unten rechts lauter, leiser oder stumm. Unter Optionen legst du fest, ob sie bei Gästen standardmäßig an ist.
- **Eigene Bilder** (Optionen): fliegen durch den Wartebildschirm und auf Wunsch dezent über die ganze Seite.
- **Laufschrift im Wartebildschirm** (Optionen): eigene Einträge mit Text und kleinem Bild, zum Beispiel Sponsoren-Logos. Mit „Vorschau ansehen“ siehst du sofort, wie es aussieht.
- **Quiz-Musik** wird nur auf dem Gerät gespeichert, auf dem du sie auswählst. Nimm das Gerät, das an den Lautsprechern hängt.
- **Kosten:** Der kostenlose Firebase-Tarif (Spark) reicht für so ein Turnier locker aus.
- **Abmelden** als Spielleiter: ganz unten auf der Seite.
- Daten aus der alten Claude-Version werden nicht automatisch übernommen. Spieler und eigene Quizfragen trägst du einmal neu ein.
