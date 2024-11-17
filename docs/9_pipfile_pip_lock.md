# Pipfile und Pipfile.lock – Wozu dienen diese Dateien?

Pipenv verwendet zwei zentrale Dateien zur Verwaltung von Abhängigkeiten in einem Python-Projekt: `Pipfile` und `Pipfile.lock`. Beide Dateien spielen eine wichtige Rolle, um eine reproduzierbare und kontrollierte Umgebung für das Projekt zu schaffen. Hier ist eine Übersicht über die Funktion jeder Datei:

## 1. Pipfile

Die `Pipfile` ersetzt die herkömmliche `requirements.txt`-Datei und dient als zentrale Definitionsdatei für alle Abhängigkeiten des Projekts. Sie wird automatisch von Pipenv erstellt, sobald das erste Paket installiert wird.

### Inhalt und Struktur der `Pipfile`

Eine typische `Pipfile` enthält:

- **[source]**: Gibt die Paketquelle (z. B. das PyPI-Repository) an, aus der Pakete installiert werden.
- **[packages]**: Listet die Hauptabhängigkeiten des Projekts auf (z. B. `requests`). Hier werden alle Pakete definiert, die für die Ausführung der Anwendung erforderlich sind.
- **[dev-packages]**: Listet die Entwicklungsabhängigkeiten auf, die nur während der Entwicklung benötigt werden (z. B. `pytest` für Tests).
- **[requires]**: Gibt die Python-Version an, die das Projekt benötigt.

### Beispiel für eine `Pipfile`

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

Die `Pipfile` dient also als eine Art "Definition" der gewünschten Umgebung. Sie legt fest, welche Pakete und Mindestversionen benötigt werden, aber nicht die genauen Versionsnummern aller Abhängigkeiten und Unterabhängigkeiten.

## 2. Pipfile.lock

Die `Pipfile.lock` ist eine ergänzende Datei zur `Pipfile` und sichert die Reproduzierbarkeit der Umgebung. Während die `Pipfile` eine grobe Definition der Pakete enthält, dokumentiert die `Pipfile.lock` die exakten Versionen aller installierten Pakete und deren Abhängigkeiten. Dies umfasst auch die Versionen aller indirekten (transitiven) Abhängigkeiten.

### Funktionen der `Pipfile.lock`

- **Reproduzierbarkeit**: Die `Pipfile.lock` stellt sicher, dass jedes Setup identisch wiederhergestellt werden kann. Sie enthält die exakten Versionsnummern und Hashes der Pakete, um eine gleichbleibende Umgebung zu gewährleisten.
- **Stabilität**: Durch die Verwendung einer `Pipfile.lock` wird verhindert, dass unkontrollierte Änderungen in Abhängigkeiten das Projekt brechen. Selbst wenn neuere Versionen von Paketen veröffentlicht werden, bleibt die Umgebung stabil, solange die `Pipfile.lock` verwendet wird.

### Beispiel für eine `Pipfile.lock`

Eine `Pipfile.lock` ist eine JSON-Datei, die in etwa so aussieht:

```json
{
    "_meta": {
        "hash": {
            "sha256": "abc123..."
        }
    },
    "default": {
        "requests": {
            "version": "==2.25.1",
            "hashes": [
                "sha256:xyz456...",
                "sha256:uvw789..."
            ]
        }
    },
    "develop": {
        "pytest": {
            "version": "==6.2.2",
            "hashes": [
                "sha256:klm012...",
                "sha256:opq345..."
            ]
        }
    }
}
```

Die `Pipfile.lock` dokumentiert somit die genaue Umgebung und ermöglicht, dass jeder Entwickler oder jede Instanz des Projekts exakt dieselben Abhängigkeiten und Versionen installiert.
