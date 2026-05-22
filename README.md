# 🧠 Second Brain Skills

> **Vier Skills. Ein Schema. Ein lokaler Wissensgraph.**
> Obsidian * Markdown * LLM-Workflows - aufgebaut als wiederverwendbares Skill-Set fuer persoenliche Knowledge Bases.
> Die strukturierte Arbeitsgrundlage, um rohe Quellen in ein verlinktes, wartbares Second Brain zu verwandeln.

![Status](https://img.shields.io/badge/status-active-brightgreen)
![Obsidian](https://img.shields.io/badge/obsidian-vault-7C3AED)
![Skills](https://img.shields.io/badge/skills-4-2563EB)
![Language](https://img.shields.io/badge/language-DE%20%7C%20EN-111827)

## Worum es geht

Dieses Repository enthaelt lokale Skills fuer den Aufbau und die Pflege eines Obsidian-basierten Second Brains. Es ist kein fertiger Notizbestand, sondern ein Werkzeugkasten: Die Skills helfen dabei, einen neuen Vault zu initialisieren, Quellen zu verarbeiten, Fragen gegen das Wiki zu beantworten und die Qualitaet des Wissensgraphen regelmaessig zu pruefen.

Das System folgt dem **LLM Wiki Pattern**: Ein KI-Agent arbeitet als Bibliothekar. Rohe Quellen bleiben unveraendert in `raw/`, waehrend das eigentliche Wissen als strukturierte, verlinkte Markdown-Seiten in `wiki/` entsteht.

Dadurch wird aus einzelnen Artikeln, Transkripten, PDFs oder Notizen ein navigierbarer Wissensgraph:

- Welche Quellen stuetzen eine bestimmte Aussage?
- Welche Konzepte tauchen in mehreren Quellen wieder auf?
- Welche Personen, Organisationen, Produkte oder Tools sind miteinander verbunden?
- Welche Synthesen, Vergleiche und Analysen sind bereits entstanden?
- Wo fehlen Querverweise, Seiten oder aktuelle Quellen?

## Enthaltene Skills

| Skill | Rolle | Wofuer er wichtig ist |
|---|---|---|
| `second-brain` | Onboarding Wizard | Erstellt einen neuen Obsidian-Vault mit Verzeichnisstruktur, Index, Log und Agent-Konfigurationen |
| `second-brain-ingest` | Quellenverarbeitung | Verarbeitet Dateien aus `raw/` zu Quellen-, Entitaeten- und Konzeptseiten im Wiki |
| `second-brain-query` | Wissensabfrage | Beantwortet Fragen gegen `wiki/index.md`, Wiki-Seiten und optional lokale Suche mit `qmd` |
| `second-brain-lint` | Qualitaetspruefung | Findet kaputte Wikilinks, Waisen-Seiten, Widersprueche, veraltete Claims und fehlende Querverweise |

Zusammen bilden diese Skills einen vollstaendigen Arbeitszyklus: **einrichten, befuellen, abfragen, verbessern**.

## Perfekt fuer

Diese Skills sind besonders nuetzlich fuer:

- persoenliche Obsidian-Wissensdatenbanken
- Recherche-Brains zu Fachthemen, Projekten oder Maerkten
- LLM-gestuetzte Arbeit mit kontrollierten lokalen Quellen
- Aufbau eines versionierten Knowledge Graphs aus Webartikeln, PDFs, Transkripten und Notizen
- Teams oder Einzelpersonen, die Agenten mit klaren Wiki-Regeln arbeiten lassen wollen
- wiederholbare Workflows fuer Claude Code, Codex, Cursor oder Gemini CLI

## Obsidian als lokaler Wissensgraph

Der Ziel-Vault ist fuer Obsidian gebaut. Die Skills erzeugen und pflegen eine klare Wiki-Struktur:

- Quellen werden als eigene Summary-Seiten dokumentiert.
- Entitaeten und Konzepte erhalten eigene Seiten.
- Alle internen Beziehungen laufen ueber `[[wikilinks]]`.
- `wiki/index.md` bleibt der Master-Katalog aller Seiten.
- `wiki/log.md` protokolliert jede Operation chronologisch.
- `wiki/synthesis/` sammelt wertvolle Vergleiche, Analysen und Querverbindungen.

Statt Informationen nur als lose Notizen abzulegen, entsteht ein lokales Wissenssystem, das von LLMs gezielt gelesen, erweitert und zitiert werden kann.

## Projektstruktur

```text
.
+-- second-brain/
|   +-- SKILL.md                      # Onboarding Wizard fuer neue Vaults
|   +-- scripts/
|   |   +-- onboarding.sh             # Erstellt raw/, wiki/, output/ und Basisdateien
|   +-- references/
|       +-- wiki-schema.md            # Kanonisches Schema fuer alle Ziel-Vaults
|       +-- tooling.md                # Empfohlene CLI-Tools
|       +-- agent-configs/
|           +-- claude-code.md        # Vorlage fuer CLAUDE.md
|           +-- codex.md              # Vorlage fuer AGENTS.md
|           +-- cursor.md             # Vorlage fuer .cursor/rules/second-brain.mdc
|           +-- gemini.md             # Vorlage fuer GEMINI.md
+-- second-brain-ingest/
|   +-- SKILL.md                      # Verarbeitet neue Quellen in Wiki-Seiten
+-- second-brain-query/
|   +-- SKILL.md                      # Beantwortet Fragen aus dem lokalen Wiki
+-- second-brain-lint/
    +-- SKILL.md                      # Prueft Wiki-Gesundheit und Konsistenz
```

## Wie das Wissen modelliert wird

Ein mit diesen Skills erzeugter Vault besteht aus drei Hauptbereichen:

| Ordner | Bedeutung |
|---|---|
| `raw/` | Unveraenderte Originalquellen, z. B. Web-Clips, PDFs, Transkripte oder Notizen |
| `wiki/` | Strukturierter Wissensgraph, den der LLM-Agent pflegt |
| `output/` | Reports, Query-Ergebnisse und generierte Artefakte |

Jede Wiki-Seite besitzt YAML-Frontmatter:

```yaml
---
tags: [tag1, tag2]
sources: [source-filename.md]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

Die Wiki-Unterstruktur trennt die Rollen klar:

- `wiki/sources/` - eine Zusammenfassungsseite pro Quelle
- `wiki/entities/` - Personen, Organisationen, Produkte und Tools
- `wiki/concepts/` - Ideen, Frameworks, Muster und Theorien
- `wiki/synthesis/` - Analysen, Vergleiche und uebergreifende Zusammenhaenge

## Workflow

Der typische Ablauf ist bewusst einfach:

1. **Vault anlegen** mit `second-brain`
2. **Quellen sammeln** in `raw/`, idealerweise mit dem Obsidian Web Clipper
3. **Quellen ingestieren** mit `second-brain-ingest`
4. **Fragen stellen** mit `second-brain-query`
5. **Wiki pruefen** mit `second-brain-lint`

Der wichtigste Designpunkt: Quellen bleiben stabil, das Wiki wird kontinuierlich verdichtet.

## Agenten-Unterstuetzung

Der Onboarding-Skill kann Konfigurationsdateien fuer mehrere Agenten erzeugen:

| Agent | Datei im Ziel-Vault |
|---|---|
| Claude Code | `CLAUDE.md` |
| Codex | `AGENTS.md` |
| Cursor | `.cursor/rules/second-brain.mdc` |
| Gemini CLI | `GEMINI.md` |

Alle Templates verwenden dasselbe `wiki-schema.md`. Dadurch arbeiten verschiedene Agenten nach denselben Regeln und erzeugen kompatible Wiki-Seiten.

## Beispiel-Fragen an ein erzeugtes Brain

- Was weiss mein Wiki bereits ueber ein bestimmtes Unternehmen?
- Welche Quellen erwaehnen ein bestimmtes Konzept?
- Welche Tools werden in mehreren Artikeln verglichen?
- Welche Aussagen widersprechen sich zwischen zwei Quellen?
- Welche Themen sind haeufig erwaehnt, aber noch nicht gut ausgearbeitet?
- Welche Synthese sollte aus den vorhandenen Notizen gespeichert werden?

## Quickstart - In 3 Schritten einsatzbereit

### Schritt 1 - Skills installieren oder in den Skill-Pfad legen

Dieses Repository ist als lokales Skill-Verzeichnis gedacht. Die Ordner `second-brain`, `second-brain-ingest`, `second-brain-query` und `second-brain-lint` muessen im Skill-Pfad des verwendeten Agenten liegen.

### Schritt 2 - Neuen Vault initialisieren

Starte den Skill `second-brain`. Der Wizard fragt nacheinander:

- Name des Vaults
- Speicherort
- Thema oder Domain
- gewuenschte Agent-Konfigurationen
- optionale CLI-Tools

Danach erzeugt das Onboarding die Grundstruktur:

```text
raw/
raw/assets/
wiki/
wiki/sources/
wiki/entities/
wiki/concepts/
wiki/synthesis/
output/
wiki/index.md
wiki/log.md
```

### Schritt 3 - Quellen verarbeiten und abfragen

Lege Quellen in `raw/` ab und fuehre danach `second-brain-ingest` aus. Sobald die ersten Wiki-Seiten entstanden sind, kann `second-brain-query` Fragen gegen den lokalen Wissensbestand beantworten.

Nach groesseren Aenderungen oder etwa alle zehn Ingests sollte `second-brain-lint` laufen.

## Empfohlene Tools

| Tool | Zweck |
|---|---|
| Obsidian Web Clipper | Speichert Webartikel sauber als Markdown in `raw/` |
| `summarize` | Fasst Links, Dateien und Medien per CLI zusammen |
| `qmd` | Lokale Suche fuer groessere Markdown-Wikis |
| `agent-browser` | Browser-Automation fuer Recherchefaelle, in denen Standardtools nicht reichen |

Die Tools sind optional, aber fuer wachsende Vaults sinnvoll. Der Skill funktioniert auch ohne Datenbank oder Server.

## GitHub-Ziel

Dieses Repository repraesentiert den wiederverwendbaren Skill-Kern:

- Skill-Definitionen fuer Setup, Ingest, Query und Lint
- das kanonische Wiki-Schema
- Agent-Konfigurationsvorlagen fuer mehrere LLM-Umgebungen
- ein Onboarding-Script fuer neue Obsidian-Vaults
- Tooling-Hinweise fuer lokale Recherche- und Suchworkflows

Nicht enthalten sind persoenliche Vault-Inhalte, private Quellen, lokale Obsidian-Einstellungen oder projektspezifische Wissensdatenbanken.

## Hinweis

Diese Skills erzeugen und pflegen lokale Wissensgraphen. Die Qualitaet der Antworten haengt von den eingepflegten Quellen, der Konsistenz des Wikis und regelmaessigen Lint-Pruefungen ab. Fuer fachlich verbindliche Entscheidungen sollten relevante Originalquellen immer mitgeprueft werden.
