<h1 align="center"><img src="assets/banner.svg" alt="Second Brain Skills: Quellen rein, verlinktes Wiki raus" width="900"></h1>

<p align="center">
  <b>Wirf Quellen rein. Bekomm ein Wiki raus, das sich selbst pflegt.</b><br>
  Vier Agent-Skills machen aus PDFs, Artikeln und Transkripten einen verlinkten Obsidian-Wissensgraphen.<br>
  Du befragst ihn, er meldet Widersprüche.
</p>

<p align="center">
  <img alt="Obsidian" src="https://img.shields.io/badge/Obsidian-Vault-7C3AED?style=for-the-badge&logo=obsidian&logoColor=white">
  <img alt="4 Skills" src="https://img.shields.io/badge/Skills-4-2563EB?style=for-the-badge">
  <img alt="Agenten" src="https://img.shields.io/badge/Claude_Code_·_Codex_·_Cursor_·_Gemini-0D9488?style=for-the-badge">
</p>

<p align="center">
  <a href="#-in-60-sekunden-starten"><img alt="⚡ Starten" src="https://img.shields.io/badge/⚡_Starten-7C3AED?style=for-the-badge"></a>
  <a href="#-was-dabei-herauskommt"><img alt="🔍 Ergebnis" src="https://img.shields.io/badge/🔍_Ergebnis-1E1B4B?style=for-the-badge"></a>
  <a href="#-lint-in-aktion"><img alt="🩺 Lint" src="https://img.shields.io/badge/🩺_Lint-1E1B4B?style=for-the-badge"></a>
  <a href="#enthaltene-skills"><img alt="🧩 Skills" src="https://img.shields.io/badge/🧩_Skills-1E1B4B?style=for-the-badge"></a>
  <a href="#-faq"><img alt="❓ FAQ" src="https://img.shields.io/badge/❓_FAQ-1E1B4B?style=for-the-badge"></a>
</p>

```bash
git clone https://github.com/guschi18/obsidian-skills.git && cp -r obsidian-skills/second-brain* ~/.claude/skills/
```

| 🪄 **Einrichten** | 📥 **Befüllen** | 💬 **Abfragen** | 🩺 **Verbessern** |
|:---:|:---:|:---:|:---:|
| `second-brain` | `second-brain-ingest` | `second-brain-query` | `second-brain-lint` |
| Vault anlegen | `raw/` → `wiki/` | Antwort mit Belegen | Fehler und Lücken finden |

<p align="center"><img src="assets/demo.svg" alt="Animation: Eine Quelle landet in raw/, ingest baut verlinkte Wiki-Seiten, eine Frage wird mit Quellenbelegen beantwortet" width="900"></p>

## ⚡ In 60 Sekunden starten

<p align="center"><img src="assets/terminal.svg" alt="Terminal: git clone, Skills nach ~/.claude/skills kopieren, in Claude Code „Richte ein Second Brain ein“ sagen, der Wizard legt den Vault an" width="900"></p>

<details>
<summary>Windows (PowerShell) statt bash</summary>

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

<p align="center"><img src="assets/vault.svg" alt="Dateibaum nach dem Ingest: eine Quelle in raw/, dazu neue Seiten in sources, entities und concepts, mit Vorschau der Konzeptseite" width="900"></p>

## 🩺 Lint in Aktion

<p align="center"><img src="assets/lint.svg" alt="Beispiel für second-brain-lint: Ein Scan prüft die Wiki-Seiten und meldet einen Fehler, eine Warnung und einen Hinweis" width="900"></p>

Nach etwa zehn Ingests laufen lassen. Lint meldet auch Widersprüche zwischen Quellen und veraltete Aussagen.

## Enthaltene Skills

<p align="center"><img src="assets/skills.svg" alt="Vier Skills: second-brain richtet den Vault ein, second-brain-ingest verdichtet Quellen, second-brain-query beantwortet Fragen mit Belegen, second-brain-lint prüft das Wiki" width="900"></p>

## Warum nicht einfach …?

<p align="center"><img src="assets/compare.svg" alt="Vergleich mit losen Notizen und Chat mit Dokumenten: Second Brain Skills verdichtet Wissen, belegt Aussagen per Wikilink, erkennt Widersprüche per Lint, bleibt als Markdown lesbar und speichert gute Antworten" width="900"></p>

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
