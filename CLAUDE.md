# IDS Builder — Projektstand

## Projekt
- **Datei:** `C:\Users\mmueller01\Desktop\ids-builder\index.html`
- **Mirror:** `C:\Users\mmueller01\Desktop\QG-IDS-Builder.html`
- **GitHub:** https://github.com/CADMECAdmin/IDS-Builder
- **GitHub Pages:** https://cadmecadmin.github.io/IDS-Builder/
- **Workflow:** Nach jeder Änderung: Mirror kopieren + Git commit + push

## Was bereits gebaut ist (Stand 2026-05-14)
- Vollständiger IDS 1.0 Builder (Single HTML File, kein Backend)
- IFC-versionsspezifische Entity-Listen (IFC2X3, IFC4, IFC4X3_ADD2)
- IFC-versionsspezifische Datentyp-Dropdowns
- Alle Facetten: Entity, Attribute, Property, Classification, Material, PartOf
- Korrekte Kardinalitäten per Facette (simpleCardinality für Material/PartOf)
- Property dataType als Kind-Element (nicht als XML-Attribut)
- minOccurs/maxOccurs korrekt auf ids:specification (nicht applicability)
- Preset-Buttons für Erwartete Anzahl inkl. «Keines (verboten)» (min=0, max=0)
- Fix: Preset-Wert wird aus aktivem Button gelesen (nicht aus number-Input)
- Leeres ids:requirements wird nicht ausgegeben (per IDS 1.0 XSD optional)
- File System Access API: «Speichern» schreibt direkt ins Original (Chrome/Edge)
- SIA-Phasen Dropdown (SIA 11-61)
- Deutsche Begriffe (Anwendungsbereich, Anforderungen)
- Placeholder-Texte ohne Kundendaten

## Bekannte Limitationen
- Solibri unterstuetzt maxOccurs="0" nicht (bestaetigt durch Tests)
- Solibri wertet Spezifikationen ohne Requirements nicht aus (bestaetigt)
- URI-Felder vorhanden aber bSDD-Integration nicht implementiert

## Naechste grosse Features (in dieser Reihenfolge)

### 1. IDS Checker im Browser (WebAssembly)
- IFC-Datei + IDS-Datei direkt im Browser pruefen
- Kein Python, kein Server, kein Solibri noetig
- Library-Kandidaten: web-ifc (https://github.com/tomvandig/web-ifc)
- Zuerst Proof-of-Concept: IFC laden + Entity auslesen
- Dann vollstaendige IDS-Regelprüfung implementieren

### 2. AI-Assistent fuer IDS-Erstellung
- Natuerliche Sprache -> IDS-Spezifikation
- Zweistufig:
  a) Onboarding: Provider-Wahl (Anthropic/Ollama), API-Key Setup mit Anleitung,
     Arbeitskontext (Disziplin, eigene Psets, SIA-Phasen)
  b) IDS-Chat: Konversation, AI erkennt fehlende Felder, stellt Rueckfragen,
     generiert Spezifikation wenn alle Infos vorhanden
- API-Key pro Nutzer in localStorage (kein geteiltes Risiko)
- Ollama-Option fuer eigenen Server in der Schweiz (Datensouveraenitaet)
- System-Prompt = Standard IDS-Wissen + personalisierter Nutzer-Kontext
- Multi-Turn Konversation (Gespraechsverlauf wird mitgeschickt)

## Architektur-Entscheidungen
- Kein Backend - alles im Browser (JavaScript/WebAssembly)
- Vanilla JS, kein Framework
- Business-Logik (XML-Generator, Parser) ist wiederverwendbar fuer spaeteren Umbau
- File System Access API fuer direktes Speichern (Chrome/Edge), Fallback Download

## Testdateien
- `TEST_mit_Proxy.ifc` - Modell mit eingefuegtem IFCBUILDINGELEMENTPROXY
- `CADMEC-Test.ids` - Test-IDS-Datei
