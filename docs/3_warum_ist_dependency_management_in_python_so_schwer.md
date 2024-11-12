# Warum ist das Abhängigkeitsmanagement in Python so schwierig?

### Die Standardwerkzeuge fördern keine Best Practices

In vielen modernen Programmiersprachen gibt es bereits ein integriertes, auf Sperrdateien basierendes Abhängigkeitsmanagement. Rust’s `Cargo` ist ein hervorragendes Beispiel.

**Bei Python sieht das anders aus**.

Der Standard-Paketmanager für Python ist `pip`, und die typische Anweisung zur Installation eines Pakets lautet `pip install paket`. Leider ist dieser imperative Ansatz völlig losgelöst von der Versionsverwaltung des Codes. Sehr schnell kann es passieren, dass hunderte Pakete installiert sind, und man verliert den Überblick: Welche Pakete wurden explizit installiert? Welche sind nur durch andere Abhängigkeiten dazugekommen? Welche Version hat in welcher Umgebung funktioniert? Ein Rollback zu einer früheren funktionierenden Umgebung ist nicht möglich, und das Hinzufügen eines neuen Pakets könnte die Umgebung zerstören.

Noch schlimmer ist, dass ein System-Python mit `pip` zu verwenden, Anwendungen beschädigen kann, die systemweit installiert sind. Dieses Risiko lässt sich zwar durch `pip install --user paket` oder durch virtuelle Umgebungen reduzieren, aber diese Methoden sind für Anfänger oft nicht leicht verständlich. Standardmäßige virtuelle Umgebungen haben außerdem ihre eigenen Einschränkungen.

### Das Problem mit System- und Projektpaketen

Python wird häufig als „Glue“-Sprache verwendet und erfordert oft zusätzliche, nicht-Python-spezifische Abhängigkeiten. Diese lassen sich jedoch nicht immer über `pip` installieren, weshalb zusätzliche Tools benötigt werden, um die Umgebung einzurichten.

Ein wesentliches Beispiel für eine nicht-Python-Abhängigkeit ist der Python-Interpreter selbst. Verwendet man den System-Paketmanager zur Installation, kann oft nur eine einzige Python-Version für alle Projekte auf dem System genutzt werden. Dadurch sind diverse Tools entstanden, die speziell darauf abzielen, mehrere Python-Versionen zu verwalten.

Je mehr Tools erforderlich sind, um eine Umgebung zu deklarieren und zu erstellen, desto schwieriger wird es, den Setup-Prozess zu automatisieren und die Reproduzierbarkeit sicherzustellen.

### Fragmentierung im Ökosystem

Aufgrund der Schwächen der Standard-Tools existiert eine Vielzahl an Drittanbieter-Tools, die diese Lücken schließen sollen. Jedes Tool wurde für bestimmte Anwendungsfälle entwickelt, und kein Tool eignet sich für alle möglichen Projekttypen oder den gesamten Entwicklungszyklus.

Statt eines komplementären Tool-Ökosystems gibt es zwei große, getrennte Ökosysteme: `pypi.org` + `pip` und `anaconda.org` + `Conda`. Zwar lassen sich diese Tools gemeinsam nutzen, aber dies kann zu Problemen führen.

Das Ergebnis ist, dass man sich intensiv mit den vorhandenen Tools auseinandersetzen muss, um die für das spezifische Projekt passenden auszuwählen. Hinzu kommt die Herausforderung, durch die Vielzahl von Meinungen zu navigieren, da viele Nutzer für ihr favorisiertes Tool als die ultimative Lösung werben.

### Drittanbieter-Tools sind oft in Python geschrieben

Eine zusätzliche Ironie ist, dass viele der Tools für Python-Entwickler selbst in Python geschrieben sind. Das bedeutet, dass zunächst eine Python-Installation und eine Umgebung erforderlich sind, um diese Tools zu installieren. Werden die Tools in der gleichen Umgebung wie das Projekt installiert, können die Abhängigkeiten der Tools mit denen der Anwendung in Konflikt geraten. Schnell entsteht eine Art „Toolception“: Man benötigt Tools, um die Abhängigkeiten für Tools zu verwalten, die wiederum die Abhängigkeiten der Anwendung verwalten.

Glücklicherweise findet hier gerade ein Paradigmenwechsel statt, da viele neue Python-Tools nun in Rust geschrieben und als statisch verlinkte Binärdateien vertrieben werden.
