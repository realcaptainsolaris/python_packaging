# Definition: Was ist eine Abhängigkeit?

Man könnte vorschlagen, dass eine Abhängigkeit ein anderes Paket oder eine Bibliothek ist, die im Code verwendet wird – also etwas, das man mit `pip install` installiert. Leider ist dies nur ein Teil der Abhängigkeiten. Letztlich ist eine Abhängigkeit **alles, was außerhalb deines eigenen Codes liegt und notwendig ist, damit dieser wie erwartet funktioniert**. Diese Abhängigkeiten lassen sich in verschiedene Ebenen unterteilen:

1. **Projektspezifische Pakete**  
   Das sind typische Python-Bibliotheken, die man über einen Python-Paketmanager wie `pip` installiert.

2. **Systempakete**  
   Dies sind globale Pakete oder Bibliotheken (z. B. `.so`- oder `.dll`-Dateien), die systemweit installiert werden, beispielsweise mit einem System-Paketmanager (z. B. `homebrew`, `apt`, `pacman`, etc.). Diese Pakete werden von allen Nutzern und Projekten auf dem System gemeinsam genutzt.

3. **Betriebssystem**  
   Es könnte den Anschein haben, dass Python-Code auf jedem Betriebssystem läuft. Dies stimmt jedoch nur, weil Python selbst und viele in C geschriebene Bibliotheken für verschiedene Plattformen kompiliert sind. Pakete, die ausschließlich für Linux kompiliert sind, funktionieren beispielsweise nicht auf Windows. Zudem können grundlegende Systemoperationen, wie Speicherzuteilung oder das Schreiben von Dateien, sich je nach Betriebssystem leicht unterschiedlich verhalten.

4. **Hardware**  
   Auch die Hardwarearchitektur (z. B. x86, amd64, arm64) spielt eine Rolle. Code, der für eine Architektur kompiliert wurde, läuft möglicherweise nicht auf einer anderen. Auch wenn Python-Code selbst nicht kompiliert werden muss, sind die zugrundeliegenden Bibliotheken und Python selbst von der Architektur abhängig. Zusätzlich kann dein Code auf bestimmte Hardware angewiesen sein, wie z. B. GPUs zur Beschleunigung.

5. **Die Umgebung**  
   Dies umfasst alles, was sich außerhalb des eigenen Computers befindet, insbesondere den Netzwerkzugriff. Der Code könnte auf externe Ressourcen angewiesen sein, z. B. auf Datenbanken, Websites oder APIs. Diese externen Ressourcen gelten ebenfalls als Abhängigkeiten.

Der Punkt hierbei ist, zu erkennen, dass dein "einfaches" Skript oder Jupyter-Notebook oft auf einem hohen und komplexen Stapel von Systemen, Bibliotheken und Umgebungsbedingungen basiert, um zu funktionieren. Wenn du Code auf deinem eigenen Rechner entwickelst, denkst du selten an diese Komplexität. Doch sie wird entscheidend, sobald du deinen Code auf anderen Rechnern ausführen oder gemeinsam mit anderen daran arbeiten möchtest.
