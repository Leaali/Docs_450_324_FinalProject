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

## V* = Vorbedingungen:
1. Keine To-Do’s vorhanden/erstellt  
2. Min. eine To-Do vorhanden/erstellt  
3. Min. 2 To-Do’s mit unterschiedlichen Werten bei Priorität, Kategorie und Datum  

## Nachbedingungen:
Keine  

| Nr. | Testfall                                | V* | Beschreibung                                                                                                          | Erwartetes Ergebnis                                                                                      | Testtyp |
|-----|-----------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|---------|
| 1   | Keine To-Dos vorhanden                 | 1              | Home Seite, wenn keine To-Do’s erstellt sind                                                                         | Anzeige von «Keine ToDos vorhanden, erstelle welche» unterhalb von dem Erstellungsformular               | Positiv |
| 2   | To-Do Erstellen                        | -              | Eingabe Erstellungsformular:<br>Titel: «Test-1»<br>Kategorie: «Private»<br>Priorität: «Medium»<br>Datum: leer<br>Erstellen «+» Button klicken | To-Do wird korrekt erstellt und unterhalb dargestellt                                                    | Positiv |
| 3   | Ungültige Eingabe (ungültiger Titel)   | -              | Eingabe Erstellungsformular:<br>Titel: «266 Zeichen langer Text»<br>Kategorie: default<br>Priorität: default<br>Datum: leer<br>Erstellen «+» Button klicken | Backend blockiert das Speichern (500er) und Frontend zeigt eine rote Fehlermeldung                       | Negativ |
| 4   | To-Do Bearbeiten & Vergangenheit Styling | 2              | Bestehende To-Do Felder Eingabe:<br>Titel: «Test-2-bearbeitet»<br>Kategorie: «Private»<br>Priorität: «Medium»<br>Datum: 10.01.2025 14:00 | Änderungen werden korrekt gespeichert und angezeigt                                                     | Positiv |
| 5   | To-Do Löschen                          | 2              | Klicken auf das Müll-Icon bei einer bestehenden To-Do                                                                | To-Do wird aus der Liste entfernt und ist nicht mehr ersichtlich                                         | Positiv |
| 6   | To-Do Abschliessen                     | 2              | Checkbox auswählen                                                                                                   | Titel des To-Do’s wird durchgestrichen und verblasst dargestellt                                         | Positiv |
| 7   | Filtern/Sortieren nach Priorität       | 3              | Klicken auf: «Priority High to Low»                                                                                  | To-Dos mit Priority High werden zuoberst angezeigt, dann Medium und dann Low                             | Positiv |
| 8   | Filtern/Sortieren nach Priorität       | 3              | Klicken auf: «Priority Low to High»                                                                                  | To-Dos mit Priority Low werden zuoberst angezeigt, dann Medium und dann High                             | Positiv |
| 9   | Filtern nach Kategorie                 | 3              | Klicken auf: «By Category»<br>Kategorien Dropdown: Kategorie «Private» auswählen                                    | Nur To-Dos mit der Kategorie Private werden angezeigt (keine, falls keine To-Do diese Kategorie hat)     | Positiv |
| 10  | To-Do Kategorie Erstellen & Auswählen | -              | Eingabe Erstellungsformular:<br>Titel: «Neue Kategorie»<br>Kategorie: «Custom» auswählen<br>Im neuen Inputfeld: «Test-Kategorie» eingeben<br>Erstellen «+» Button klicken | Kategorie wird korrekt erstellt und zugewiesen                                                          | Positiv | 
| 11  | Farbige Markierung bei Fälligkeit     | -              | Eingabe Erstellungsformular:<br>Titel: «Test-datum-1»<br>Kategorie: default<br>Priorität: default<br>Datum: 10.01.2025 14:00<br>Erstellen «+» Button klicken | To-Do wird mit einer roten Border umrahmt, da das Datum in der Vergangenheit liegt                        | Positiv |


<details>
  <summary>Notizen - Archiv - Testbeschreibungen</summary>



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













