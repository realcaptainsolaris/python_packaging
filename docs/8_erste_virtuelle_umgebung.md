# Einrichten einer ersten virtuellen Umgebung mit Pipenv

Pipenv erleichtert das Erstellen und Verwalten von virtuellen Umgebungen in Python, indem es sowohl die Umgebung als auch die Abhängigkeiten eines Projekts isoliert. Hier ist eine Schritt-für-Schritt-Anleitung zur Einrichtung einer virtuellen Umgebung mit Pipenv.

## Schritte zur Einrichtung einer virtuellen Umgebung

1. **Wechseln in das Projektverzeichnis**  
   Erstellen Sie ein neues Verzeichnis für Ihr Projekt (falls noch nicht vorhanden) und navigieren Sie hinein:

   ```bash
   mkdir mein_projekt
   cd mein_projekt
   ```

2. **Virtuelle Umgebung erstellen und erste Abhängigkeit installieren**  
   Um eine virtuelle Umgebung zu erstellen und gleichzeitig das erste Paket (z. B. `requests`) zu installieren, verwenden Sie:

   ```bash
   pipenv install requests
   ```

   Dieser Befehl erstellt eine virtuelle Umgebung und eine `Pipfile`, die alle Abhängigkeiten des Projekts verwaltet. Pipenv erstellt zudem eine `Pipfile.lock`, die für eine reproduzierbare Umgebung sorgt.

3. **Pipenv ohne Pakete verwenden**  
   Wenn Sie zunächst nur die Umgebung einrichten möchten, ohne Pakete zu installieren, verwenden Sie:

   ```bash
   pipenv install
   ```

   Pipenv erstellt eine leere virtuelle Umgebung, die Sie später mit Paketen befüllen können.

4. **Die virtuelle Umgebung aktivieren**  
   Starten Sie die virtuelle Umgebung mit:

   ```bash
   pipenv shell
   ```

   Sie befinden sich nun in der isolierten Umgebung des Projekts und können Ihre Python-Skripte und -Pakete hier sicher verwenden.

5. **Zusätzliche Pakete installieren**  
   Um weitere Pakete hinzuzufügen, nutzen Sie den Befehl `pipenv install <paketname>`. Wenn Sie Entwicklungswerkzeuge wie Linter oder Test-Frameworks nur für die Entwicklungsumgebung installieren möchten, verwenden Sie das `--dev`-Flag:

   ```bash
   pipenv install pytest --dev
   ```

   So werden die Pakete in der `Pipfile` unter `[dev-packages]` gelistet.

6. **Verlassen der virtuellen Umgebung**  
   Um die virtuelle Umgebung zu verlassen, geben Sie einfach den folgenden Befehl ein:

   ```bash
   exit
   ```

## Wichtige Dateien: `Pipfile` und `Pipfile.lock`

- **Pipfile**: Enthält alle Abhängigkeiten, die für das Projekt installiert sind, sowie deren Kategorien (Produktion oder Entwicklung).
- **Pipfile.lock**: Dokumentiert die genauen Versionen aller Abhängigkeiten, um sicherzustellen, dass das Projekt überall gleich eingerichtet wird.

## Beispiel einer `Pipfile`

Nach der Installation von `requests` und `pytest --dev` könnte Ihre `Pipfile` wie folgt aussehen:

```toml
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[packages]
requests = "*"

[dev-packages]
pytest = "*"

[requires]
python_version = "3.8"
```

```
