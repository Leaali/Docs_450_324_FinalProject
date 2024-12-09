# Testkonzept
### Beschreibung
Für das Testkonzept orientieren wir uns an der Testpyramide und deren Testarten, um die Funktionalität der To-Do-List Anwendung inkl. deren User Stories sicherzustellen. Ziel des Konzeptes ist es aufzuzeigen, wo welche Tests wofür eingesetzt werden inkl. erster Testfälle.

### Testarten (Testpyramide)
![Testpyramide](./img/test-pyramid.png)



|Testart|Wie (Tool)| Ziel / Funktion |Mögliche Testfälle|
|-|-|-|-|
| Manuelles Testen | Manuell - über das Frontend testen | Ganzes System testen aus End-User-Sicht| Erstellen / Löschen / Editieren einer To-Do |
| End-to-End Tests | Systemtesten mit Cypress| Ganzes System testen| Erstellen / Löschen / Editieren einer To-Do |
| Integrationstest   | Automatisierte API Schnittstellen tests mit WireMock | Schnittstellen testen Backend| CRUD To-Do-List (Jeden Endpunkt)|
| Component Test| Frontend mit Jest| Laden von Seiten sicherstellen| Seite /home / new / edit|
| Unittest| Backend mit JUnit & Mockito| Einzelne Codeeinheiten wie Funktionen testen | Erstellen, Bearbeiten, Löschen|

### Testumgebung:
**Automatisierte Tests**: CICD Github Action Pipeline (Ubuntu)

**Manuelle Tests**: Über das Frontend in einem Webbrowser wie Chrome


### Testfälle Manuelles Testen
Testen der Funktionalitäten: Erstellen, Bearbeiten, Anzeigen und Löschen Manuell über das Frontend testen und in einem Test-Protokoll festhalten.

Manuelle Testfälle für das Testen des Frontends:

  | **Testfall** | **Beschreibung** | **Erwartetes Ergebnis** | **Testtyp** |
  |--------------|------------------|-------------------------|-------------|
  | **To-Do Erstellen** | Erstellen eines neuen To-Dos mit Priorität, Fälligkeitsdatum und Kategorie | To-Do wird korrekt erstellt | Positiv |
  | **Ungültige Eingaben** | Eingabe von ungültigem Titel (zu lang), Datum (z.B. 30. Februar), Priorität oder fehlende Pflichtfelder | Frontend blockiert das Speichern und zeigt Fehler | Negativ |
  | **Keine To-Dos vorhanden** | Keine To-Dos im System | Anzeige von "Keine ToDos vorhanden, erstelle welche" | Positiv |
  | **To-Do Bearbeiten** | Bearbeiten einer Aufgabe (Titel, Priorität, Fälligkeitsdatum) | Änderungen werden korrekt gespeichert | Positiv |
  | **To-Do Löschen** | Löschen eines To-Dos | To-Do wird aus der Liste entfernt | Positiv |
  | **Filtern/Sortieren nach Priorität und Fälligkeitsdatum** | To-Dos nach Priorität und Fälligkeitsdatum filtern/sortieren | To-Dos werden korrekt gefiltert und sortiert | Positiv |
  | **To-Do Kategorie Erstellen und Auswählen** | Neue Kategorie erstellen und zuweisen sowie eine vorhandene Kategorie auswählen und zuweisen | Kategorie wird korrekt erstellt und zugewiesen | Positiv |
  | **Farbige Markierung bei Fälligkeit** | Fälligkeitsdatum innerhalb der nächsten 24 Stunden | Aufgabe wird farblich markiert | Positiv |


<details>
  <summary>Notizen - Archiv - Testbeschreibungen</summary>

Mit berücksichtigen "Negativ tests" wo man prüft, ob erwartete Errors zurückkommen / passendes Handeling gemacht wird z.B.:
- beim Erstellen und Editieren den Titel zu lang machen -> Errormeldung / Frontend-form-validierung
    - Weitere ungültige eingabeverhalten Testen: 
    - ungültiges Datum eingeben
    - keine Priorität mitgeben/angeben ()
- Wenn keine To-Do vorhanden sind kommt kein error,  sonder sowas wie "keine ToDos vorhanden, erstelle welche um sie zu sehen"




**Front und Backend Tests**
- To-Do Erfassen (mit Priorität, Fälligkeitsdatum und bestehende Kategorie )
- To-Do Holen / Anzeigen
- To-Do Bearbeiten
- To-Do Löschen

- To-Do Holen / Anzeigen -> Filtern/ Sortieren nach Priorität & Fälligkeitstadum

**nur Frontend testen, sofern es keine eigene DB Tabelle ist - wenn eigene Tabelle, dann auch Backend testen**
- To-Do Kategorie Erstellen

**Explizitere beschreibung für Frontend Cypress tests**:
- Erstellen: inkl. Fälligkeitsdatum auswählen, Priorität, Kategorie erstellen
- Anzeigen: Fälligkeitsdatum , Kategorie anzeigen, Farbliche hervorhebung für Aufgaben innerhalb der nächsten 24 Stunden fällig sind
- Löschen von To-Do
- Bearbeiten von einer To-Do

</details>













