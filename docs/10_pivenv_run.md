# Unterschied zwischen `pipenv run` und `pipenv shell`

Pipenv bietet zwei verschiedene Möglichkeiten, um Befehle innerhalb einer virtuellen Umgebung auszuführen: `pipenv run` und `pipenv shell`. Beide haben unterschiedliche Anwendungszwecke und Funktionsweisen. Hier ist der Unterschied:

## 1. `pipenv shell`

Der Befehl `pipenv shell` startet eine neue Shell-Sitzung innerhalb der virtuellen Umgebung des Projekts. Nach dem Ausführen dieses Befehls befinden Sie sich direkt in der virtuellen Umgebung, und alle weiteren Befehle, die Sie eingeben, werden innerhalb dieser Umgebung ausgeführt.

### Anwendungsfall

- Ideal, wenn Sie mehrere Befehle nacheinander innerhalb der virtuellen Umgebung ausführen möchten, ohne jedes Mal `pipenv run` voranstellen zu müssen.
- Nützlich für interaktive Arbeit, bei der verschiedene Skripte oder Kommandos in der virtuellen Umgebung ausgeführt werden sollen.

### Beispiel

```bash
pipenv shell
# Jetzt befinden Sie sich in der virtuellen Umgebung
python skript.py     # Führt skript.py innerhalb der Umgebung aus
pip install numpy    # Installiert ein Paket in der virtuellen Umgebung
exit                 # Verlassen der virtuellen Umgebung
```

## 2. `pipenv run`

Der Befehl `pipenv run` ermöglicht das Ausführen eines einzelnen Befehls innerhalb der virtuellen Umgebung, ohne die Shell-Sitzung explizit betreten zu müssen. `pipenv run` führt den angegebenen Befehl innerhalb der Umgebung aus und kehrt danach automatisch zur ursprünglichen Shell zurück.

### Anwendungsfall

- Ideal, wenn Sie nur einen bestimmten Befehl einmalig innerhalb der virtuellen Umgebung ausführen möchten.
- Praktisch für Skripte oder kurze Kommandos, ohne die Umgebung betreten und verlassen zu müssen.

### Beispiel

```bash
pipenv run python skript.py
```

Dieser Befehl führt `skript.py` in der virtuellen Umgebung aus, kehrt aber nach der Ausführung direkt in die reguläre Shell zurück.
