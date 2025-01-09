**Alternativen zu Pipenv**  
_Python-Projekte erfolgreich verwalten und paketieren_

---  

Pipenv hat sich in den letzten Jahren zu einem häufig genutzten Tool für die Verwaltung von virtuellen Umgebungen und Abhängigkeiten in Python-Projekten entwickelt. Es kombiniert dabei das Erzeugen von virtuellen Umgebungen mit dem Verwalten der Pakete und den dazugehörigen *Pipfile* / *Pipfile.lock*. Dennoch gibt es zahlreiche Entwickler:innen, die sich von Pipenv abwenden oder nach anderen Lösungen suchen. Sei es aus Gründen der Geschwindigkeit, der Flexibilität, Kompatibilitätsfragen oder einfach, weil neue Tools spannende Features mitbringen.

In diesem Tutorial schauen wir uns die gängigsten Alternativen zu Pipenv an, wie sie funktionieren, und welche Vor- und Nachteile sie mit sich bringen.  

---

## 1. Poetry

### 1.1 Was ist Poetry?  
[Poetry](https://python-poetry.org/) ist ein Tool, das alle Aspekte des Python-Paketmanagements abdeckt. Dazu gehören unter anderem:  
- Paket-Abhängigkeiten verwalten (inkl. automatischer Auflösung von Abhängigkeiten)  
- Erstellung und Upload eigener Pakete (z. B. auf PyPI)  
- Automatische Generierung von *pyproject.toml*, *poetry.lock*, u. a.  
- Integrierte Virtual-Environment-Verwaltung  

Poetry konzentriert sich auf eine moderne Herangehensweise, ist sehr gut dokumentiert und setzt auf den [PEP 517/518](https://peps.python.org/pep-0517/) Standard, der für das Build- und Packaging-System von Python eingeführt wurde.

### 1.2 Installation von Poetry  
Die offizielle und empfohlene Installationsmethode ist via [install.python-poetry.org](https://install.python-poetry.org/). Dabei wird ein kleines Skript heruntergeladen und ausgeführt. Auf Linux/macOS sieht das so aus:
```bash
curl -sSL https://install.python-poetry.org | python3 -
```
Alternativ gibt es auf der offiziellen Website weitere Installationsoptionen sowie Installationspakete.

### 1.3 Grundlegende Nutzung

1. **Initialisierung eines Projekts**  
   ```bash
   poetry init
   ```
   Hier beantwortet man die Fragen zu Paketname, Version, Autor etc.  
   Alternativ kann man direkt eine `pyproject.toml` anlegen.

2. **Abhängigkeiten hinzufügen**  
   ```bash
   poetry add requests
   ```
   Dadurch wird `requests` in die `pyproject.toml` und `poetry.lock` geschrieben.  

3. **Virtuelle Umgebung verwalten**  
   Poetry erstellt und verwaltet automatisch ein Virtual Environment. Man kann es aktivieren via:
   ```bash
   poetry shell
   ```
   oder einfach Befehle darin ausführen (ohne es dauerhaft zu aktivieren) mittels:
   ```bash
   poetry run python main.py
   ```

4. **Abhängigkeiten installieren**  
   ```bash
   poetry install
   ```
   Lädt alle in `pyproject.toml` angegebenen Dependencies (bzw. die gespeicherten Versionen in `poetry.lock`) herunter und installiert sie.

5. **Erstellung eines Pakets**  
   ```bash
   poetry build
   ```
   Erzeugt ein distributables Paket (Wheel und/oder Source Archive), das man direkt mit 
   ```bash
   poetry publish
   ```
   auf PyPI hochladen kann.

### 1.4 Vor- und Nachteile von Poetry  
| **Vorteile**                                                      | **Nachteile**                                                         |
|-------------------------------------------------------------------|------------------------------------------------------------------------|
| - Einfache und einheitliche Verwaltung von Abhängigkeiten         | - Kann im Vergleich zu einfachen Pip-Skripten anfangs etwas komplexer sein |
| - Moderne Build- und Package-Standards (PEP 517/518)              | - Erfordert anfangs eine Umstellung der Projektstruktur               |
| - Sehr gute Dokumentation und stetig weiterentwickelt             | - Manchmal Inkompatibilitäten mit exotischen Setups/Plattformen        |
| - Zuverlässige Versionsverwaltung in `poetry.lock`                |                                                                        |

---

## 2. Pip-Tools (pip-tools)

### 2.1 Was sind pip-tools?  
[**pip-tools**](https://github.com/jazzband/pip-tools) ist ein Paket, das auf `pip` aufsetzt und zwei zentrale Werkzeuge bietet:  
- `pip-compile`: Erstellt aus einer `requirements.in` eine fixierte `requirements.txt`, wobei Abhängigkeiten und deren Versionen automatisch aufgelöst werden.  
- `pip-sync`: Sorgt dafür, dass die installierten Pakete exakt der aktuellen `requirements.txt` entsprechen.

Das bedeutet, dass man seine *primären* Dependencies in einer `requirements.in` festlegt, `pip-compile` kümmert sich um die Transitiv-Abhängigen (z. B. `requests` → `urllib3`, `chardet`, etc.) und schreibt alles in die `requirements.txt`.

### 2.2 Installation von pip-tools
In einer (am besten neuen) virtuellen Umgebung:
```bash
python -m pip install pip-tools
```
Es wird einfach das `pip-tools`-Paket installiert.

### 2.3 Grundlegende Nutzung
1. **Erstellen einer `requirements.in`**  
   Diese enthält nur die direkten Abhängigkeiten, z. B.:  
   ```
   requests==2.28.1
   flask
   ```
2. **Kompilieren zu `requirements.txt`**  
   ```bash
   pip-compile requirements.in
   ```
   Jetzt wird `requirements.txt` erstellt – inklusive aller Unterabhängigkeiten mit fixierten Versionen.  

3. **Synchronisation**  
   ```bash
   pip-sync
   ```
   Sorgt dafür, dass alle Pakete in der aktuellen Umgebung genau den Einträgen in `requirements.txt` entsprechen. Pakete, die nicht in der `requirements.txt` stehen, werden entfernt.  

### 2.4 Vor- und Nachteile von pip-tools  
| **Vorteile**                                                    | **Nachteile**                                                  |
|-----------------------------------------------------------------|-----------------------------------------------------------------|
| - Minimalistisch: greift nicht in Virtual-Environment-Verwaltung ein    | - Keine integrierte Virtual-Environment-Verwaltung             |
| - Leicht zu verstehen, da es `pip` erweitert                           | - Bietet weniger Komfortfunktionen als Poetry oder Pipenv       |
| - Flexible Nutzung auch in CI/CD-Pipelines (Automatisierung)   | - Keine integrierte „Lockfile“ im Pipenv-Sinn (allerdings fixierte `requirements.txt`) |

---

## 3. Conda (Anmerkung: nicht nur eine Pipenv-Alternative)  

### 3.1 Was ist Conda?  
[**Conda**](https://docs.conda.io/) ist ein plattformunabhängiger Paket- und Environment-Manager, der nicht nur für Python-Pakete, sondern auch für Bibliotheken in C/C++, R und anderen Sprachen genutzt wird. Es kommt ursprünglich aus dem Scientific-Python-Umfeld (Anaconda/Miniconda), ist aber auch allgemein sehr verbreitet.

Conda kann virtuelle Umgebungen erstellen und Pakete installieren, allerdings nicht rein über PyPI, sondern über eigene Channels (z. B. `conda-forge`). Man kann aber in Conda-Umgebungen selbstverständlich auch `pip` nutzen.  

### 3.2 Vorteile von Conda  
- Verwaltung von Python- und Non-Python-Paketen gleichzeitig (z. B. NumPy, OpenCV usw.)  
- Sehr ausgereiftes Environment-Management (isolierte Umgebungen)  
- Große Community und viele Pakete im `conda-forge`-Channel  

### 3.3 Nachteile von Conda  
- Installation und Nutzung sind schwergewichtiger als Poetry oder Pipenv (größerer Overhead, besonders bei Anaconda)  
- Das System der Channels und Versionen kann verwirrend sein  
- Keine automatische Generierung von Lockfiles wie in Pipenv/Poetry  

---

## 4. Weitere Tools und Erwähnenswertes

### 4.1 Hatch  
[**Hatch**](https://github.com/pypa/hatch) ist ein relativ neues Tool, das als modernes Build-Tool für Python auftritt und ebenfalls virtuelle Umgebungen verwalten kann. Es orientiert sich an den [PEP 517/518](https://peps.python.org/pep-0517/)-Standards, ähnlich wie Poetry, und bietet u. a. ein plugin-basiertes Ökosystem.

### 4.2 Virtualenv (Klassiker)  
Das Original-Werkzeug zum Erstellen virtueller Umgebungen. Heute meist durch den in Python integrierten Befehl `python -m venv` ersetzt. Man kann `virtualenv` bzw. `venv` zusammen mit einem eigenständigen Requirements-Workflow (z. B. manuelle `requirements.txt`) nutzen, wenn man maximale Kontrolle wünscht.

### 4.3 Pipx (für CLI-Tools)  
Wenn man hauptsächlich CLI-Werkzeuge installieren und isolieren möchte (z. B. `black`, `mypy`, `flake8` etc.), ist [**pipx**](https://pypa.github.io/pipx/) ideal. Pipx installiert Python-CLI-Tools jeweils in einer eigenen kleinen Virtual Environment – so können die Tools nicht gegenseitig in Konflikt geraten.

---

## 5. Fazit: Welche Alternative ist die richtige?

- **Poetry** ist oft die erste Wahl, wenn man ein _all-in-one_ Tool für Abhängigkeitsmanagement, Projektstruktur und Paketierung sucht. Es bietet zudem komfortable Befehle für Packaging und Deployment.  
- **pip-tools** ist hervorragend, wenn man gerne weiterhin mit `pip` (und eventuell `venv`/`virtualenv`) arbeiten möchte, aber eine professionelle Lösung für die Verwaltung fixierter Dependencies benötigt.  
- **Conda** empfiehlt sich für datenwissenschaftliche Projekte, bei denen viele Abhängigkeiten außerhalb des Python-Ökosystems benötigt werden oder wenn man besonders unkompliziert Pakete in isolierten Umgebungen installieren möchte (z. B. C++-Bibliotheken).  
- **Hatch** wird immer beliebter für modern strukturierte Python-Projekte und ähnelt in seiner Philosophie teilweise Poetry.  
- **Virtualenv / venv** + manuelle `requirements.txt` bleibt der minimalistische Standard, wenn man maximale Einfachheit/Transparenz schätzt (etwa in sehr kleinen Projekten oder DevOps-Skripten).  
- **pipx** eignet sich, um Python-CLI-Tools zu installieren und zu isolieren, ohne direkt ein ganzes Projekt zu verwalten.

Im Endeffekt kommt es darauf an, welche Anforderungen dein Projekt und dein Team haben. Für die meisten klassischen Python-Projekte ist Poetry (oder Pipenv) sehr praktisch und benutzerfreundlich. Wer dagegen mehr Feintuning braucht oder sich stärker an `pip` orientieren will, ist mit `pip-tools` sehr gut beraten. Gerade für Data-Science-Projekte lohnt sich auch ein Blick in die Welt von Conda.

---

### Weiterführende Links
- [Uv](https://astral.sh/blog/uv)
- [Poetry Doku](https://python-poetry.org/docs/)  
- [pip-tools Repo](https://github.com/jazzband/pip-tools)  
- [Conda Doku](https://docs.conda.io/en/latest/)  
- [Hatch Doku](https://ofek.dev/hatch/latest/)  
- [PyPA Tools Übersicht](https://packaging.python.org/key_projects/)

