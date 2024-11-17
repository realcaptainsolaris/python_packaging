# Installation von Paketen in einer virtuellen Umgebung mit Pipenv

Pipenv erleichtert die Installation und Verwaltung von Paketen innerhalb einer virtuellen Umgebung, indem es alle Abhängigkeiten isoliert und so Konflikte mit anderen Projekten vermeidet. Hier sind die grundlegenden Schritte und Optionen zur Paketinstallation in einer Pipenv-Umgebung.

## 1. Paketinstallation für die Produktion

Um ein Paket in der virtuellen Umgebung zu installieren, das für die Produktion oder die allgemeine Verwendung benötigt wird, verwenden Sie den folgenden Befehl:

```bash
pipenv install <paketname>
```

### Beispiel

```bash
pipenv install requests
```

Dieser Befehl installiert das `requests`-Paket und fügt es zur `Pipfile` unter `[packages]` hinzu.

## 2. Installation von Entwicklungspaketen

Wenn Sie ein Paket installieren möchten, das nur für Entwicklungszwecke benötigt wird (z. B. Test- oder Linter-Tools), verwenden Sie das `--dev`-Flag:

```bash
pipenv install <paketname> --dev
```

### Beispiel

```bash
pipenv install pytest --dev
```

Dies installiert das `pytest`-Paket und fügt es in der `Pipfile` unter `[dev-packages]` hinzu. Diese Pakete werden nur in der Entwicklungsumgebung verwendet und nicht in der Produktion.

## 3. Spezifische Versionen installieren

Falls eine bestimmte Version eines Pakets benötigt wird, können Sie diese bei der Installation angeben:

```bash
pipenv install <paketname>==<version>
```

### Beispiel

```bash
pipenv install requests==2.25.1
```

Damit wird genau die Version `2.25.1` des `requests`-Pakets installiert.

## 4. Aktualisierung eines Pakets

Um ein Paket auf die neueste Version zu aktualisieren, verwenden Sie:

```bash
pipenv update <paketname>
```

Falls alle Pakete in der Umgebung aktualisiert werden sollen, verwenden Sie einfach:

```bash
pipenv update
```

## 5. Pakete deinstallieren

Falls ein Paket nicht mehr benötigt wird, können Sie es mit folgendem Befehl aus der Umgebung und der `Pipfile` entfernen:

```bash
pipenv uninstall <paketname>
```

Um alle Pakete zu deinstallieren und die Umgebung zu leeren, verwenden Sie:

```bash
pipenv uninstall --all
```

## Wichtige Dateien: `Pipfile` und `Pipfile.lock`

- **Pipfile**: Speichert die Pakete und Versionen, die explizit für das Projekt installiert wurden, sowohl für Produktion als auch Entwicklung.
- **Pipfile.lock**: Sichert die exakten Versionen aller Abhängigkeiten und deren Unterabhängigkeiten, um eine reproduzierbare Umgebung zu gewährleisten.

## Beispiele für häufige Pipenv-Kommandos

```bash
# Installation eines Pakets für die Produktion
pipenv install requests

# Installation eines Pakets nur für die Entwicklung
pipenv install pytest --dev

# Installation einer bestimmten Paketversion
pipenv install requests==2.25.1

# Aktualisierung eines bestimmten Pakets
pipenv update requests

# Aktualisierung aller Pakete in der Umgebung
pipenv update

# Deinstallation eines Pakets
pipenv uninstall requests

# Deinstallation aller Pakete und Leeren der Umgebung
pipenv uninstall --all
```

Mit diesen Pipenv-Befehlen ist die Verwaltung von Paketen in einer virtuellen Umgebung einfach und effizient. Pipenv stellt sicher, dass alle Pakete ordnungsgemäß isoliert und für reproduzierbare Setups dokumentiert sind.
