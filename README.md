# 🧪 Virtuelles Ionenfischen

Eine interaktive, browserbasierte Lernanwendung zur qualitativen anorganischen Analyse für den Chemieunterricht (Sekundarstufe I & II).

Dieses Tool ermöglicht es Schülerinnen und Schülern, klassische Nachweisreaktionen im virtuellen Reagenzglas durchzuführen, Beobachtungen zu dokumentieren und unbekannte Salzlösungen systematisch zu identifizieren – ganz ohne realen Chemikalienverbrauch.

## 🎯 Didaktisches Konzept & Funktionen

Das "Virtuelle Ionenfischen" simuliert einen realitätsnahen analytischen Laborablauf:

* **Umfangreicher Probenpool:** Das System wählt zufällig aus 27 verschiedenen Salzen (inklusive relevanter Distraktoren). Keine Probe wiederholt sich innerhalb einer Session.
* **Realistische Labor-Aktionen:** * Prüfung von Lösungsfarbe und pH-Wert (animiertes Indikatorpapier).
    * Flammenfärbung mit Magnesiastäbchen.
    * Geruchsnachweise (z.B. Ammoniak oder Essig durch Erwärmen).
    * Gezielte Reagenzienzugabe (Säuren, Basen, weitere Fällungsmittel) inklusive "Überschuss"-Reaktionen (Auflösen von Niederschlägen) und Ringprobe.
* **Ressourcen-Management (Gamification):** Jede Aktion kostet Tropfen aus einem virtuellen Budget (100 Tropfen Startwert). Ein integriertes Highscore-System belohnt zielgerichtetes analytisches Denken und bestraft planloses "Zusammenschütten".
* **Fehlertolerante Auswertung:** Schülerinnen und Schüler müssen Kation, Anion, deren Nachweise sowie den exakten chemischen Namen des Salzes bestimmen. Das System gibt präzises Feedback zu Fehlern und weist auf korrekte Nomenklatur (z.B. Wertigkeiten bei Übergangsmetallen) hin.
* **Expertenmodus:** Für fortgeschrittene Klassen können direkte Text-Hinweise (z.B. "Flamme färbt sich gelb") ausgeblendet werden, sodass rein auf Basis der visuellen Animationen entschieden werden muss.

## 💻 Technische Umsetzung

Die Anwendung ist als leichtgewichtige, clientseitige Single-Page-Application konzipiert:
* **Frontend:** Reines HTML5, Vanilla JavaScript und Tailwind CSS (via CDN).
* **Datenbasis (`salze.json`):** Sämtliche Reaktionen, Farben, Nachweise und Salze sind in einer externen JSON-Datei ausgelagert. Lehrkräfte können diese Datei jederzeit anpassen oder um eigene Salze erweitern, ohne den Quellcode der App berühren zu müssen. Dropdowns generieren sich vollautomatisch aus der JSON-Struktur.
* **Responsive & Design:** Entwickelt für Desktop- und Tablet-Nutzung, inklusive Dark-/Light-Mode für optimale Lesbarkeit am Beamer oder Smartboard.

## 🚀 Installation & Nutzung

Da die Anwendung die chemischen Daten aus einer externen JSON-Datei (`salze.json`) lädt, muss sie über einen Webserver aufgerufen werden (lokales Öffnen via `file://` wird von modernen Browsern aus CORS-Sicherheitsgründen oft blockiert).

**Die einfachste Lösung:**
Laden Sie die Dateien (`index.html` und `salze.json`) in ein GitHub-Repository hoch und aktivieren Sie **GitHub Pages**. Die App ist danach sofort weltweit über Ihren GitHub-Pages-Link für den Unterricht nutzbar.

## 📝 Lizenz & Autor

Ein didaktisches Tool von **Mag. Erich Kerzendorfer**.
Entwickelt im Rahmen der Integration von Künstlicher Intelligenz im naturwissenschaftlichen Unterricht (Vorgestellt in *Chemie & Schule*).


## Analytik-Hub-Adapter

Der Single-Mode bleibt vollständig erhalten. Nur ein Aufruf mit

```text
?bridge=1&run=RUN_...
```

aktiviert den Hub-Modus.

Im Hub-Modus:

- wird die vom Hub vorgegebene unbekannte Probe geladen, ohne ihre Identität im UI offenzulegen,
- ist „Neue Probe“ deaktiviert,
- müssen Kation, Anion, Nachweise und Salzname weiterhin von den Lernenden selbst eingegeben werden,
- kann der Hub zusätzlich verlangen, dass bestimmte Nachweise tatsächlich durchgeführt wurden,
- wird erst nach korrekter Auswertung und vollständiger Evidenz ein `QUALITATIVE_ION_ANALYSIS`-RESULT freigegeben,
- enthält das RESULT die bestätigten Ionen, ausgewählten Begründungen und die tatsächlich durchgeführten Tests,
- kann ein optionaler Realversuch als Anschlussidee an den Hub übergeben werden.

Für VCÖ-01 wird intern `probe_05` (Kupfer(II)-sulfat) verwendet; diese interne Modell-ID wird im Hub-Modus nicht als Stoffidentität angezeigt.
