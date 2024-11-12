## Warum sollten wir "Abhängigkeiten verwalten" und was bedeutet das überhaupt?

Der Hauptgrund, gute Praktiken im Abhängigkeitsmanagement anzuwenden, ist die **Reproduzierbarkeit**. Reproduzierbarkeit bedeutet, dass wir einer bestimmten Abfolge von Schritten folgen und immer exakt das gleiche Ergebnis erhalten können. Reproduzierbarkeit macht das Verhalten des Codes deterministisch: Alle, die mit dem Code arbeiten, erleben dasselbe Verhalten und finden dieselben Fehler. Sobald ein Schritt in der Kette nicht reproduzierbar ist, wird das Verhalten des Codes nicht mehr vorhersehbar.

Es gibt drei Phasen, in denen Reproduzierbarkeit entscheidend ist:

1. **Die Entwicklungsphase**:  
   Während der Entwicklung möchtest du sicherstellen, dass du die Umgebung für deinen Code jederzeit einfach neu erstellen kannst. Dies ist wichtig, selbst wenn du alleine entwickelst. Falls deine Umgebung versehentlich beschädigt wird, hast du die Möglichkeit, von vorne zu beginnen. Besonders kritisch wird es, wenn du im Team entwickelst: Ideal wäre es, wenn alle Entwickler in identischen Umgebungen arbeiten. In der Entwicklungsphase können zusätzliche Abhängigkeiten erforderlich sein, die zur Laufzeit nicht gebraucht werden, z. B. Tools für Linting und Formatierung.

2. **Die Build-Phase**:  
   Wenn du deinen Code veröffentlichen oder deine Anwendung bereitstellen möchtest, können zusätzliche Schritte notwendig sein. Bei einer reinen Python-Bibliothek könnte dies bedeuten, den Code als Zip- oder Tar-Datei zu packen und hochzuladen. Falls du Erweiterungen in anderen Sprachen geschrieben hast, musst du sie möglicherweise kompilieren. Wenn du einen Webservice bereitstellst, könnte dies den Aufbau eines Docker-Containers erfordern. Das Ergebnis der Build-Phase sind ein oder mehrere Artefakte. Reproduzierbarkeit bedeutet hier, dass du durch erneutes Ausführen des Build-Prozesses immer identische Artefakte erzeugen kannst – also eine direkte Zuordnung zwischen deinem Code und dem, was du veröffentlichst, sicherstellst. Auch die Build-Phase kann zusätzliche Abhängigkeiten erfordern, z. B. einen Compiler, eine Tool-Chain zum Containeraufbau oder ein Tool zur Erstellung von Zip-Dateien.

3. **Die Bereitstellungsphase / Laufzeit**:  
   Wenn dein Code oder deine Anwendung „in freier Wildbahn“ läuft, möchtest du ein vorhersagbares Verhalten garantieren. Du willst nicht, dass sich das Verhalten deines Codes verändert, weil du deine Abhängigkeiten nicht genau nachverfolgt hast. Idealerweise verhält sich der Code genauso wie in der Entwicklungsphase.

### Was bedeutet gutes Abhängigkeitsmanagement?

- **Alle Abhängigkeiten** für Entwicklungs-, Build- und Bereitstellungsphasen werden explizit deklariert und zusammen mit dem Code in der Versionskontrolle verfolgt. Das spiegelt die Tatsache wider, dass **deine Anwendung = dein Code + alle Abhängigkeiten** ist.
- **Ein automatisierter Prozess** stellt sicher, dass die deklarierten Abhängigkeiten in eine funktionierende Umgebung überführt werden können.
- **Sichere Weiterentwicklung und Aktualisierung** der Umgebung sind möglich, wenn neue Versionen von Abhängigkeiten verfügbar werden.

In den meisten Fällen lässt sich dies bis zur Abhängigkeitsebene des Betriebssystems umsetzen. Wenn du in der Cloud oder auf einem Hypervisor arbeitest, wo Hardware in Code deklariert werden kann, lässt sich die Kontrolle über den Abhängigkeitsstapel sogar noch weiter ausdehnen. In der Regel müssen jedoch Annahmen über die Umgebung, wie die Verfügbarkeit von Hardware oder Netzwerkverbindungen, im Anwendungscode behandelt werden.

Im weiteren Verlauf dieses Artikels befassen wir uns hauptsächlich mit Software-Abhängigkeiten bis zur Ebene des Betriebssystems.
