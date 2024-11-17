# Den Überblick über virtuelle Umgebungen behalten

Bei der Arbeit an verschiedenen Projekten mit Pipenv und anderen Tools zur Verwaltung virtueller Umgebungen kann es schnell unübersichtlich werden, welche Umgebung für welches Projekt eingerichtet wurde und welche Abhängigkeiten installiert sind. Hier sind einige Tipps und Techniken, um den Überblick über Ihre virtuellen Umgebungen zu behalten und effizient zu verwalten.

## 1. Übersichtliche Projektstruktur

- **Projektordner organisieren**: Halten Sie alle Projekte in klar strukturierten Ordnern, z. B. `~/Projekte`, mit eindeutigen Unterordnern für jedes Projekt. Dies hilft, jedes Projektverzeichnis und dessen Umgebung einfach zu identifizieren.
- **Standardisierte Benennung**: Verwenden Sie konsistente und beschreibende Namen
für Ihre Projektverzeichnisse, damit Sie sofort erkennen, welches Projekt und
welche Umgebung Sie gerade bearbeiten.

## 2. Pipenv-Kommandos zur Verwaltung und Übersicht

Pipenv bietet nützliche Befehle, um schnell auf Informationen zu den
installierten Abhängigkeiten und zur Umgebung zuzugreifen.

- **Liste aller Abhängigkeiten anzeigen**:

  ```bash
  pipenv graph
  ```

Dieser Befehl zeigt eine grafische Übersicht über alle installierten Pakete
und deren Abhängigkeiten. Dies ist hilfreich, um zu sehen, welche Pakete und
Versionen aktuell in der Umgebung sind.

- **Informationen zur Umgebung abrufen**:

  ```bash
  pipenv --venv
  ```

Dieser Befehl zeigt den Pfad der virtuellen Umgebung des aktuellen Projekts an,
sodass Sie schnell zur Umgebung navigieren oder prüfen können, ob Sie die
richtige Umgebung verwenden.

- **Paket- und Versionsinformationen prüfen**:
Die `Pipfile` und `Pipfile.lock` geben Aufschluss über die installierten Pakete und deren Versionen. Durch einen kurzen Blick in diese Dateien sehen Sie, welche Pakete für das Projekt vorgesehen sind und welche Versionen gesperrt wurden.

## 3. Systematischer Einsatz von `pipenv shell` und `pipenv run`

- **`pipenv shell` für interaktive Arbeit**: Verwenden Sie `pipenv shell` nur dann, wenn Sie mehrere Befehle in einer Umgebung ausführen möchten. Denken Sie daran, die Shell mit `exit` zu verlassen, um Verwirrung zu vermeiden, wenn Sie in andere Projektverzeichnisse wechseln.
- **`pipenv run` für einzelne Befehle**: Falls Sie nur einen spezifischen Befehl ausführen möchten, nutzen Sie `pipenv run <befehl>`, um sicherzustellen, dass dieser nur einmalig in der Umgebung ausgeführt wird, ohne die Shell betreten zu müssen.

## 4. Verwendung eines `.env`-Files

- **Umgebungsvariablen für Projekte festlegen**: Viele Projekte benötigen spezielle Umgebungsvariablen. Legen Sie eine `.env`-Datei im Projektverzeichnis an, um wichtige Variablen zu speichern und zu automatisieren. Pipenv lädt diese Datei automatisch und stellt die Variablen in der virtuellen Umgebung bereit.

## 5. Virtual Environments in die Versionskontrolle aufnehmen

- **Teilen Sie `Pipfile` und `Pipfile.lock` mit Ihrem Team**: Nehmen Sie diese Dateien in die Versionskontrolle (z. B. mit Git) auf. Dies stellt sicher, dass alle Teammitglieder die gleiche Umgebung reproduzieren können und hält die Abhängigkeiten konsistent.

## 6. Zusätzliche Tools zur Verwaltung und Übersicht

- **pipenv-venv-wrapper**: Tools wie `pipenv-venv-wrapper` bieten eine zusätzliche grafische Verwaltung von Pipenv-Umgebungen. Sie ermöglichen das einfache Hinzufügen, Entfernen und Verwalten von Umgebungen über eine benutzerfreundliche Schnittstelle.
- **pyenv und pipx für globale Python-Versionen und Tools**: Wenn Sie an mehreren Projekten mit unterschiedlichen Python-Versionen arbeiten, kann `pyenv` nützlich sein, um die Python-Versionen pro Projekt zu verwalten. `pipx` eignet sich für das Installieren von globalen Python-Tools (wie `pipenv` selbst) in isolierten Umgebungen.

## Zusammenfassung

Mit diesen Techniken und Tools können Sie den Überblick über Ihre virtuellen Umgebungen behalten:

- Klare Ordnerstruktur und konsistente Projektbenennung
- Nutzung der Pipenv-Kommandos für die schnelle Übersicht über Abhängigkeiten und Umgebungen
- `.env`-Datei für projektbezogene Variablen
- Versionskontrolle für `Pipfile` und `Pipfile.lock`
- Zusätzliche Tools wie `pyenv` und `pipx` für bessere Verwaltung

Durch eine organisierte Struktur und ein systematisches Vorgehen wird die Arbeit mit mehreren virtuellen Umgebungen einfacher und übersichtlicher.
