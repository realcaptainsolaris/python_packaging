
# Überblick über Tools für das Dependency-Management in Python

## Übersicht über die Tools und deren Vor- und Nachteile

### 1. **pip**
   - **Funktionen**: Installiert Python-Pakete von `pypi.org`
   - **Vorteile**: Eingebaut in Python (ab Version 3.4); schnelle Installation durch `wheel`-Format; akzeptable Abhängigkeitslösung (ab Version 20.3)
   - **Nachteile**: Nur Python-Tools; keine Unterstützung für Lock-Dateien; kein Management von Python selbst

### 2. **venv**
   - **Funktionen**: Erstellt virtuelle Umgebungen
   - **Vorteile**: Eingebaut in Python (ab Version 3.3)
   - **Nachteile**: Beschränkt auf denselben Python-Interpreter; keine Installation nicht-Python-basierter Pakete

### 3. **virtualenv**
   - **Funktionen**: Erstellt virtuelle Umgebungen, ermöglicht Auswahl eines anderen Python-Interpreters
   - **Vorteile**: Flexibilität bei der Wahl des Python-Interpreters
   - **Nachteile**: Erfordert Installation via `pip`; alle Nachteile wie bei `venv`

### 4. **pip-tools**
   - **Funktionen**: Fügt Lock-File-Funktionalität zu `pip` hinzu
   - **Vorteile**: Leichtgewichtig, einfach, gut kompatibel mit `pip/venv`
   - **Nachteile**: Erfordert manuelle Pflege der Definitionsdateien; kein Management nicht-Python-basierter Pakete

### 5. **Pipenv**
   - **Funktionen**: Kombiniert `pip`, `virtualenv`, und `pip-tools`; verwaltet `Pipfile` und `Pipfile.lock`
   - **Vorteile**: Einfache Bedienung durch CLI, All-in-One-Tool für Umgebungen
   - **Nachteile**: In Python geschrieben; begrenzt auf "dev" und "non-dev"-Abhängigkeiten

### 6. **Poetry**
   - **Funktionen**: All-in-One-Tool für Projekt-Setup, virtuelle Umgebungen, Abhängigkeits- und Paket-Management
   - **Vorteile**: Unterstützt Projektaufbau und Veröffentlichungen; CLI mit Gruppierung von Abhängigkeiten
   - **Nachteile**: In Python geschrieben; komplexe und schwergewichtige Abhängigkeiten; begrenzte Unterstützung für inkompatible Umgebungen

### 7. **pyenv**
   - **Funktionen**: Installiert und verwaltet mehrere Python-Versionen
   - **Vorteile**: Shell-Skripte ohne Python-Abhängigkeit; einfache Installation von Python-Versionen
   - **Nachteile**: Lange Kompilierzeiten; benötigt C-Compiler und andere Systemabhängigkeiten; keine Windows-Unterstützung

### 8. **pipx**
   - **Funktionen**: Installiert Python-Pakete als ausführbare Dateien in isolierten Umgebungen
   - **Vorteile**: Bessere Lösung als direkte Installation von Tools in der Benutzerumgebung
   - **Nachteile**: In Python geschrieben; unterstützt keine mehrfachen Versionen desselben Tools

### 9. **uv**
   - **Funktionen**: All-in-One-Tool für Pakete, virtuelle Umgebungen, Python-Versionen und mehr, geschrieben in Rust
   - **Vorteile**: Sehr schnell, portabel, CLI für die gesamte Entwicklungsumgebung
   - **Nachteile**: Keine Unterstützung für mehrere inkompatible Umgebungen

### 10. **Conda**
   - **Funktionen**: Installiert verschiedene Software und Bibliotheken, verwaltet Python-Versionen und virtuelle Umgebungen
   - **Vorteile**: Multiplattform, robuster Algorithmus für Abhängigkeitslösungen, gut geeignet für wissenschaftliche Python-Pakete
   - **Nachteile**: Langsam, benötigt viele Systemressourcen; eingeschränkte Interoperabilität mit dem Python-Haupt-Ökosystem

### 11. **Mamba**
   - **Funktionen**: Drop-in-Ersatz für `Conda`, schnelle Abhängigkeitslösungen
   - **Vorteile**: Schneller als `Conda`, parallele Downloads
   - **Nachteile**: Erben alle `Conda`-Beschränkungen außer Geschwindigkeit

### 12. **conda-lock**
   - **Funktionen**: Lock-File-Mechanismus für Conda-Umgebungen
   - **Vorteile**: Unterstützt auch `pip`-installierbare Pakete; interoperabel mit Conda/Mamba
   - **Nachteile**: In Python geschrieben; Definitionsdateien müssen manuell gepflegt werden

### 13. **Pixi**
   - **Funktionen**: Rust-Tool für Conda-Umgebungen, ähnlich wie `uv`
   - **Vorteile**: Schnelles Tool in Rust, unterstützt Multiplattform, globale Paket-Cache
   - **Nachteile**: Abweichende Philosophie zu `Conda`-Umgebungen; keine globalen Umgebungen
