# Über einen Discord Webhook einen apcupsd alert senden
**[apcupsd](http://www.apcupsd.org/) muss komplett installiert und eingerichtet sein!**

<p align="center">
<img src="https://data.jonnytutorials.de/img/apcupsd-github/1.png" border="0" alt="bot-announce">
</p>

## Setup Linux
1. Installation der nötigen Erweiterungen
<br> Hinweis: Manchmal ist [curl](https://de.wikipedia.org/wiki/CURL) schon vorinstalliert!
``` shell
apt-get install curl
```

2. Wechsle in den apcupsd Ordner
``` shell
cd /etc/apcupsd/
```

3. Öffne die `onbattery` (In der Datei werden alle Befehle ausgeführt, wenn der Server auf Batterie-Strom läuft.)
``` shell
nano onbattery
```

4. Füge diese Zeilen über `exit 0` ein. Fülle noch die `WEBHOOK_URL` und die `NACHRICHT` aus!
``` shell
WEBHOOK_URL="" #Trage hier deinen Webhook-URL ein
NACHRICHT="" #Trage hier die Nachricht, die gesendet werden soll wenn der Strom ausfaellt.
DATE=$(date +"%s")
TIMESTAMP="<t:$DATE:R>"
PAYLOAD=" { \"content\": \"$TIMESTAMP | $NACHRICHT\" }"
curl -X POST -H 'Content-Type: application/json' -d "$PAYLOAD" "$WEBHOOK_URL"
```
<p align="center">
<img src="https://data.jonnytutorials.de/img/apcupsd-github/2.png" alt="onbattery">
</p>

5. Speichere und Verlasse die `onbattery` Datei.
6. Öffne nun die `offbattery` (In der Datei werden alle Befehle ausgeführt, wenn der Server wieder auf Netz-Strom läuft.)
``` shell
nano offbattery
```
7. Füge diese Zeilen über `exit 0` ein. Fülle noch die `WEBHOOK_URL` und die `NACHRICHT` aus!
``` shell
WEBHOOK_URL="" #Trage hier deinen Webhook-URL ein
NACHRICHT="" #Trage hier die Nachricht, die gesendet werden soll wenn der Strom wieder da ist.
DATE=$(date +"%s")
TIMESTAMP="<t:$DATE:R>"
PAYLOAD=" { \"content\": \"$TIMESTAMP | $NACHRICHT\" }"
curl -X POST -H 'Content-Type: application/json' -d "$PAYLOAD" "$WEBHOOK_URL"
```

<p align="center">
<img src="https://data.jonnytutorials.de/img/apcupsd-github/3.png" alt="offbattery">
</p>

8. Speichere und Verlasse die `offbattery` Datei.
### Fertig! Fehler kannst du [hier](https://github.com/jonnytutorials/apcupsd_discord-webhook_alert/issues/new) melden. Für Verbesserungsvorschläge steht mein [Discord Server](https://discord.gg/s9tD46Fwh8) zur Verfügung.
