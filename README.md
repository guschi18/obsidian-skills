<h1 align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="assets/banner-light.svg">
    <img src="assets/banner.svg" alt="Second Brain Skills: Quellen rein, verlinktes Wiki raus" width="100%">
  </picture>
</h1>

<p align="center">
  <b>Wirf Quellen rein. Bekomm ein Wiki raus, das sich selbst pflegt.</b><br>
  Vier Agent-Skills machen aus PDFs, Artikeln und Transkripten einen verlinkten Obsidian-Wissensgraphen.<br>
  Du befragst ihn, er meldet Widersprüche.
</p>

```bash
git clone https://github.com/guschi18/obsidian-skills.git && cp -r obsidian-skills/second-brain* ~/.claude/skills/
```

<p align="center">

[**⚡ Starten**](#-in-60-sekunden-starten) · [🔍 Ergebnis](#-was-dabei-herauskommt) · [💬 Session](#-so-fühlt-sich-das-an) · [🧩 Skills](#enthaltene-skills) · [❓ FAQ](#-faq)

</p>

<p align="center">
  <img alt="Obsidian" src="https://img.shields.io/badge/obsidian-vault-7C3AED">
  <img alt="Skills" src="https://img.shields.io/badge/skills-4-2563EB">
  <img alt="Sprache" src="https://img.shields.io/badge/language-DE%20%7C%20EN-111827">
</p>

| 🪄 **Einrichten** | 📥 **Befüllen** | 💬 **Abfragen** | 🩺 **Verbessern** |
|:---:|:---:|:---:|:---:|
| `second-brain` | `second-brain-ingest` | `second-brain-query` | `second-brain-lint` |
| Vault anlegen | `raw/` → `wiki/` | Antwort mit Belegen | Fehler und Lücken finden |

<p align="center"><img src="assets/demo.svg" alt="Animation: Eine Quelle landet in raw/, ingest baut verlinkte Wiki-Seiten, eine Frage wird mit Quellenbelegen beantwortet" width="900"></p>

## ⚡ In 60 Sekunden starten

```bash
git clone https://github.com/guschi18/obsidian-skills.git
cp -r obsidian-skills/second-brain* ~/.claude/skills/
```

<details>
<summary>Windows (PowerShell)</summary>

```powershell
git clone https://github.com/guschi18/obsidian-skills.git
Copy-Item -Recurse obsidian-skills\second-brain* $HOME\.claude\skills\
```

</details>

Dann in Claude Code (oder einem anderen Agenten mit Skill-Pfad):

| Du sagst | Es passiert |
|---|---|
| „Richte ein Second Brain ein" | Wizard legt den Vault an (Name, Ort, Thema, Agent-Configs) |
| „Ich habe etwas in `raw/` gelegt" | Ingest fasst zusammen, fragt nach Schwerpunkten, baut Wiki-Seiten |
| „Was weiß ich über X?" | Query antwortet aus dem Wiki, jede Aussage mit `[[Wikilink]]` belegt |
| „Mach einen Health-Check" | Lint listet Fehler, Warnungen und Lücken, auf Wunsch mit Fixes |

## 🔍 Was dabei herauskommt

Eine einzige Datei geht rein:

```text
raw/karpathy-llm-wiki.md        ← Web-Clip, unverändert
```

Nach `second-brain-ingest` sieht dein Vault so aus (Beispiel):

```text
wiki/
├── sources/
│   └── karpathy-llm-wiki.md    ← Zusammenfassung + Kernaussagen
├── entities/
│   └── Andrej Karpathy.md      ← Person, neu angelegt
├── concepts/
│   └── LLM Wiki Pattern.md     ← Konzept, neu angelegt
├── index.md                    ← Master-Katalog, 3 neue Einträge
└── log.md                      ← "## [2026-11-01] ingest | Karpathy LLM Wiki"
```

Und so sieht eine erzeugte Seite aus:

```markdown
---
tags: [llm, wissensmanagement]
sources: [karpathy-llm-wiki.md]
created: 2026-11-01
updated: 2026-11-01
---

# LLM Wiki Pattern

Ein Agent pflegt ein Markdown-Wiki, statt bei jeder Frage Rohtexte neu zu durchsuchen.

## Aus den Quellen
- Wissen wird einmal verdichtet und danach nur noch erweitert ([[karpathy-llm-wiki]])

## Verbunden mit
- [[Andrej Karpathy]]
```

Jede weitere Quelle ergänzt diese Seiten. Widersprüche werden mit beiden Quellen vermerkt, nicht überschrieben.

## 💬 So fühlt sich das an

```text
Du:     Ich habe karpathy-llm-wiki.md in raw/ gelegt.
Agent:  Kernaussagen: 1. Wissen wird einmal verdichtet. 2. Ein Agent pflegt Index
        und Querverweise. Soll ich etwas betonen?
Du:     Betone Punkt 2.
Agent:  Fertig: 1 Quellenseite, 1 Entität, 1 Konzept, Index und Log aktualisiert.

Du:     Was weiß ich über das LLM Wiki Pattern?
Agent:  Laut [[karpathy-llm-wiki]] wird Wissen einmal verdichtet und nur noch
        erweitert, siehe [[LLM Wiki Pattern]] und [[Andrej Karpathy]].
        Als Synthese-Seite speichern?
```

## Enthaltene Skills

| Skill | Macht | Auslöser |
|---|---|---|
| 🪄 `second-brain` | Legt den Vault an: Ordner, Index, Log, Agent-Config | „Second Brain einrichten" |
| 📥 `second-brain-ingest` | Fasst `raw/` zusammen, fragt nach Schwerpunkten, baut Wiki-Seiten | „ich habe etwas in raw/ abgelegt" |
| 💬 `second-brain-query` | Antwortet aus dem Wiki, jede Aussage per `[[Wikilink]]` belegt | „was weiß ich über X?" |
| 🩺 `second-brain-lint` | Findet kaputte Links, Waisen, Widersprüche, Lücken | „health check" |

## Warum nicht einfach …?

| | Lose Notizen | Chat mit Dokumenten (RAG) | Dieses System |
|---|---|---|---|
| Wissen wird verdichtet | nein | nein, jede Frage startet bei null | ja, einmal pro Quelle |
| Aussagen mit Beleg | nur manuell | Textstellen, ohne Struktur | `[[Wikilinks]]` |
| Widersprüche erkennen | nein | nein | Lint meldet sie |
| Lesbar ohne KI | ja | nein | ja, reines Markdown |

## Unter der Haube

<details>
<summary><b>Vault-Aufbau und Seitenformat</b></summary>

| Ordner | Bedeutung |
|---|---|
| `raw/` | Unveränderte Originalquellen (Web-Clips, PDFs, Transkripte, Notizen) |
| `wiki/` | Wissensgraph, den der Agent pflegt |
| `output/` | Reports, Query-Ergebnisse, generierte Artefakte |

Unterordner von `wiki/`: `sources/`, `entities/`, `concepts/`, `synthesis/`, dazu `index.md` und `log.md`.

Jede Seite beginnt mit YAML-Frontmatter:

```yaml
---
tags: [tag1, tag2]
sources: [source-filename.md]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

</details>

<details>
<summary><b>Agenten und Tools</b></summary>

| Agent | Datei im Vault |
|---|---|
| Claude Code | `CLAUDE.md` |
| Codex | `AGENTS.md` |
| Cursor | `.cursor/rules/second-brain.mdc` |
| Gemini CLI | `GEMINI.md` |

Optionale Tools: Obsidian Web Clipper (Quellen nach `raw/`), `summarize`, `qmd` (Suche ab ca. 100 Seiten), `agent-browser`.

</details>

## ❓ FAQ

<details>
<summary><b>Braucht es Obsidian?</b></summary>

Nein. Das Ergebnis ist reines Markdown mit `[[Wikilinks]]`. Obsidian zeigt nur den Graphen schöner an.

</details>

<details>
<summary><b>Kann der Agent meine Quellen verändern?</b></summary>

Nein. `raw/` ist unveränderlich, `wiki/log.md` ist append-only.

</details>

<details>
<summary><b>Wann lohnt sich Lint, wann `qmd`?</b></summary>

Lint nach etwa zehn Ingests. `qmd` (`npm i -g @tobilu/qmd`) ab etwa 100 Seiten. Query nutzt es automatisch.

</details>

Gefällt dir das Setup? Ein ⭐ auf GitHub hilft anderen, es zu finden.

*Antworten sind nur so gut wie deine Quellen. Prüfe bei wichtigen Entscheidungen die Originale.*
