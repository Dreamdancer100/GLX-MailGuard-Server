# GLX MailGuard Server 0.1.4

Eigenständige PHP-Anwendung von GLX Tools. Keine Nextcloud-Abhängigkeit; auf dem Kundenserver ist kein Node.js erforderlich.

Diese Version bietet Installation, Benutzer- und Postfachzuordnung, getrennte Mailbereiche, persönliche und bereichsweite Regeln, Entsperranträge und eine API für eine externe Mailserver-Anbindung. Die mitgelieferte Postfix-Policy startet im Testmodus. Eine gespeicherte Regel bedeutet noch keine aktive Ablehnung auf einem Mailserver.

## Lizenz und Testphase

GLX MailGuard Server ist kommerzielle Software: **14 Tage Testphase**, anschließend Freischaltung der **29,00-€-Version** per gültigem Token. Die Produktkennung lautet `glx-mailguard-server`. Preisangaben zur Laufzeit und Umsatzsteuer müssen vom Shopbetreiber festgelegt werden.

## Unterbrochene Übertragung fortsetzen

Den bestehenden MailGuard-Ordner nicht löschen. Die aktuelle EXE mit dem vollständigen aktuellen Server-Ordner verwenden und im Übertragungsschritt **Vorhandene Übertragung prüfen und fortsetzen** wählen. Vorhandene Dateien und der Setup-Token werden geprüft. Fremde Daten oder unbekannte Änderungen werden nicht überschrieben.

## Shop- und SourceForge-Texte

- [Warenkorb-, Kurz- und Langbeschreibung mit Serveranforderungen](Shop/Produkttexte-DE.md)
- [English SourceForge copy: 70 / 1,000 characters and ten features](Shop/SourceForge-EN.md)

## Downloads

**Sofort verfuegbar:** [PHP-Webinstallation als ZIP](Downloads/GLX-MailGuard-Server-0.1.4-Webinstallation.zip?raw=true). Dieses Paket enthaelt `install.php`, das PHP-Paket und beide Installationsanleitungen.

Den vollstaendigen Quellcode kannst du ueber **Code → Download ZIP** herunterladen. Fuer das Windows-Setup oben **Actions → Installationspakete erstellen → letzter erfolgreicher Lauf** oeffnen und unten unter **Artifacts** das Paket **GLX-MailGuard-Server-0.1.4-Installationspakete** herunterladen. Es enthaelt die Windows-EXE im Windows-x64-ZIP, PHP-Pakete, Quellcode und Pruefsummen. Dafuer bei GitHub anmelden. Die automatisierte Bereitstellung laeuft nach Aenderungen auf `main` und kann auch ueber **Run workflow** gestartet werden.

Der Windows-Build ersetzt keinen Ausfuehrungstest unter Windows und keine Mailserver-Abnahme. Die Grenzen des Entwicklungsstands stehen im Entwicklungsbericht.

## Einstieg

- [Installation Deutsch](Dokumentation/Installation-DE.md)
- [Installation English](Dokumentation/Installation-EN.md)
- [Plesk und Postfix](Dokumentation/Plesk-Postfix.md)
- [API](Dokumentation/API.md)
- [Windows-Setup kompilieren](Windows-Setup/README.md)
- [Entwicklungsbericht und Einschränkungen](Dokumentation/Entwicklungsbericht.md)

Bei manueller Bereitstellung zeigt der Document Root ausschließlich auf `Server/public`. `app`, `database`, `bin` und `var` gehören außerhalb des öffentlichen Webverzeichnisses.

Die Originalpakete von GLX Mail Server 0.9.9, GLX MailGuard Nextcloud 1.2.5 und Preview 0.1.0 werden nicht verändert. Die zwölf Design-Paletten stammen aus dem gelieferten GLX Mail Server 0.9.9. Eine vollständige visuelle Übereinstimmung mit der nicht eingelesenen Windows-EXE wurde nicht geprüft.

## Entwicklung und Tests

PHP 8.2+, MariaDB 10.6+ oder MySQL 8.0+, Erweiterungen `pdo_mysql`, `sodium`, `session`, `json`, `filter`, `zip`, `curl`, `simplexml`. Die Anwendung enthält keinen öffentlichen Demo- oder Testbenutzer.

```sh
php tests/rules.php
python3 tests/policy_bridge.py
```

Für HTTP-Tests eine frische, ausschließlich für Tests vorgesehene Datenbank installieren. Danach `requests` und für den Browsertest Playwright in einer eigenen virtuellen Python-Umgebung installieren.

```sh
MAILGUARD_TEST_URL=http://127.0.0.1:8080 \
MAILGUARD_TEST_ADMIN_PASSWORD='your-test-password' python3 tests/http_integration.py
MAILGUARD_TEST_ADMIN_PASSWORD='your-test-password' python3 tests/browser_smoke.py
```

Die Integrationssuite legt feste Testdaten an und muss gegen eine leere Testinstallation laufen. Der HTTP-Entwicklungsmodus wird nur durch `MAILGUARD_DEV=1` und eine Loopback-Clientadresse aktiviert; er gehört nicht in eine öffentlich erreichbare Installation.

Shop: https://glx-tools.de/product/glx-mail-guard-server/

SourceForge: https://sourceforge.net/projects/glx-mail-guard-server/

Updates benötigen eine gültige GLX-Signatur und eine passende SHA-256-Prüfsumme. [Veröffentlichung auf dem GLX-Server](Dokumentation/Updates-veroeffentlichen.md). Die Updatepakete werden mit dem bereitgestellten GLX-Updateschlüssel signiert und gegen den fest hinterlegten öffentlichen Schlüssel geprüft. Die konkrete Plesk-/SMTP-Abnahme ist weiterhin erforderlich.

## Upgrade auf 0.1.4

[Signiertes FTP-Updatepaket 0.1.4](Downloads/GLX-MailGuard-Server-0.1.4-Update.zip?raw=true). Das äußere ZIP enthält genau vier Dateien für den Updateordner. Das innere `GLX-MailGuard-Server.zip` bleibt gezippt. Danach in MailGuard unter **Einstellungen → Lizenz & Updates** prüfen und installieren. Der durchgehende Ablauf **0.1.3 installieren → signiert auf 0.1.4 aktualisieren → Daten sichern → deinstallieren** wurde mit lokalen PHP-/MariaDB-/HTTPS-Diensten geprüft.

Für vorhandene SSH-Installationen kann der aktuelle Windows-Assistent unter **Vorhandene Installation: Domains und Postfächer verbinden** den Bestand einlesen. Bei Root-Anmeldung korrigiert er ausschließlich bekannte Anwendungsdateirechte und richtet die regelmäßige Bestandsabfrage ein. Vorhandene Konfigurationsinhalte und fremde Dateien bleiben erhalten.

Für eine alte 0.1.2 bleibt die [damalige Updater-Korrektur](Downloads/GLX-MailGuard-Server-0.1.2-Updater-Korrektur.zip?raw=true) als Legacy-Hilfe verfügbar. [Veröffentlichung und Signaturprüfung](Dokumentation/Updates-veroeffentlichen.md). [Prüfergebnis 0.1.4 und tatsächliche Grenzen](Dokumentation/Arbeitsstand-Korrekturen.md).

Eine separate Windows-Uninstaller-EXE liegt im Actions-Download neben dem Setup-Paket. Die Web-Deinstallation steht unter Einstellungen → Deinstallation bereit.
