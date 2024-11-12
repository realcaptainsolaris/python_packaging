## Die beste Methode zur Verwaltung von Abhängigkeiten

Bevor wir uns mit dem Management von Abhängigkeiten beschäftigen, gibt es zwei grundlegende Voraussetzungen:

1. **Versionskontrolle**
2. **Umgebungsisolation**

### Voraussetzungen für Abhängigkeitsmanagement

**Versionskontrolle**: Der Code sollte in einem Versionskontrollsystem wie Git nachverfolgt werden. So kann man den Code jederzeit zu einem früheren Stand zurückrollen (einem „Commit“), was Anpassungen einfacher und sicherer macht. Auch die Dateien, in denen die Abhängigkeiten deklariert sind, müssen mit der Versionskontrolle verfolgt werden.

**Umgebungsisolation**: Es sollte eine Methode geben, die Entwicklungsumgebung vom Hostsystem zu isolieren. Ohne Isolation könnten Projektabhängigkeiten die Hostumgebung oder andere Projekte beeinflussen. Eine starke Isolation, wie separate Maschinen, erreicht man mit virtuellen Maschinen oder Containern. Oftmals bevorzugen Entwickler jedoch eine leichtere Isolation, etwa virtuelle Python-Umgebungen. Diese isolieren in der Regel nur `pip`-installierbare Pakete und bieten in vielen Fällen eine ausreichende Abtrennung.

Ein weiteres, fortgeschritteneres Konzept ist Nix, das ein extrem striktes Abhängigkeitsmanagement über das gesamte System hinweg bietet. Wir behandeln Nix näher im späteren Verlauf des Artikels.

### Schritte für gutes Abhängigkeitsmanagement

Nachdem Versionskontrolle und Isolation eingerichtet sind, umfasst gutes Abhängigkeitsmanagement die folgenden Schritte:

1. Erstellen einer Definitionsdatei
2. Generieren einer Sperrdatei (Lock-File)
3. Synchronisieren der Umgebung mit der Sperrdatei
4. Verfolgen der Definitions- und Sperrdateien in der Versionskontrolle

### Warum diese Schritte?

**Definitionsdatei**: In dieser Datei werden die Abhängigkeiten und minimale Versionsanforderungen angegeben. Sie enthält die Pakete, die direkt im Code verwendet werden (beispielsweise `import pandas`). Eine Definitionsdatei kann jedoch nur bedingt sicherstellen, dass alle möglichen gültigen Versionen des Codes funktionieren. Durch die Kombinatorik der Paketversionen können fehlerhafte Umgebungen entstehen.

**Problem transitive Abhängigkeiten**: Viele Pakete bringen zusätzliche, implizite Abhängigkeiten mit. Daher ist es möglich, dass eine Abhängigkeitskette zu einem Fehler führt, auch wenn in der Definitionsdatei alles korrekt deklariert wurde. So kann es passieren, dass zwei identische Umgebungen zu unterschiedlichen Zeiten eingerichtet werden und trotzdem unterschiedliche Abhängigkeiten erhalten, da eine neue Version einer transitive Abhängigkeit Fehler enthält.

### Sperrdatei (Lock-File) – eine Lösung

Um das Problem der zeitlichen Variabilität zu umgehen, fixieren wir sowohl die direkten als auch die transitiven Abhängigkeiten – hier kommt die Sperrdatei ins Spiel. Anstatt die Umgebung direkt aus der Definitionsdatei zu erstellen, lassen wir einen Abhängigkeits-Resolver bestimmen, welche Pakete und Versionen er installieren würde. Diese schreiben wir in die Sperrdatei, die alle Versionen und Hashes der Pakete festhält. Damit kann jeder Nutzer dieselben Artefakte herunterladen und die Umgebung zuverlässig reproduzieren.

**Beispiel mit einer Sperrdatei**:  
1. **Bob** erstellt eine Sperrdatei und Umgebung. Seine Umgebung funktioniert, und er commitet die Sperrdatei.
2. **Alice** erhält genau dieselbe Umgebung, da sie die Sperrdatei nutzt und nicht unter fehlerhaften neuen Versionen leidet.
3. **Dave** aktualisiert die Sperrdatei, da eine neue Version von Paket A erschienen ist. Nach erfolgreicher Installation commitet er die aktualisierte Sperrdatei. Die Umgebung wird nun kontrolliert zusammen mit dem Code weiterentwickelt. Bei Problemen kann jederzeit auf eine funktionierende Umgebung in der Versionshistorie zurückgegriffen werden.

### Grenzen des Abhängigkeitsmanagements

Dieses System löst nicht alle Probleme: Möglicherweise stellt man fest, dass eine früher funktionierende Sperrdatei nicht mehr korrekt arbeitet. In solchen Fällen bleibt oft nur die manuelle Problemanalyse im Abhängigkeitsstapel, was kompliziert und zeitaufwendig sein kann. Manche schlagen daher vor, Abhängigkeiten möglichst ganz zu vermeiden – was in Python jedoch kaum realisierbar ist.

Leider macht das aktuelle Abhängigkeitsmanagement in Python diese Arbeit oft unnötig kompliziert.
