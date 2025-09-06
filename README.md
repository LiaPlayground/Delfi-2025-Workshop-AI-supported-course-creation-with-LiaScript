# Delfi 2025 Workshop - AI-supported course creation with LiaScript

A compact tutorial on LiaScript, the open framework for interactive learning content. Learn how to use AI to generate questions, explanations, and exercises—making course creation efficient, time-saving, and pedagogically meaningful for educators and e-learning enthusiasts.


## LiaScript

LiaScript is an open-source framework for creating interactive learning content using a simple Markdown-like syntax. It allows educators to design and publish courses that are engaging, adaptive, and easy to use.




### Markdown for interactive learning content

LiaScript uses a simple Markdown syntax to create interactive learning content. Here are some key features:

- **Text Formatting**: Use standard Markdown syntax for headings, lists, and emphasis.
- **Interactive Elements**: Embed quizzes, flashcards, and other interactive components using special tags.
- **Multimedia Support**: Include images, videos, and audio files to enrich the learning experience.




## AI & Prompting




LiaScript is an open framework for creating interactive learning content. It allows educators to design and publish courses that are engaging, adaptive, and easy to use.

## What is a good Prompt?


### Anatomy of a prompt

Kontext + Ziel + Format + Beispiele = klar strukturierter Input.

Single-Shot vs. Few-Shot Prompting

Single-Shot: nur ein Beispiel / direkte Frage.

Few-Shot: mehrere Beispiele → die KI erkennt Muster.


### Variables




    Prompt Chaining

        Komplexe Aufgaben in einzelne Schritte zerlegen.

        Beispiel: „Erstelle Lernziele → Generiere Quizfragen → Formuliere Zusammenfassung.“

    Decomposition Prompting

        KI zerlegt ein Problem in Teilprobleme und entwickelt dazu Lösungen.

        Hilfreich für komplexe Kursmodule oder längere Lernpfade.

    Chain-of-Thought / Step-by-Step Prompting

        KI soll ihren Lösungsweg Schritt für Schritt offenlegen.

        Besonders nützlich bei logischen, mathematischen oder didaktischen Aufgaben.

    Reflexions-Prompting (Self-Critique / Critique-and-Revise)

        KI wird aufgefordert, ihre Antwort kritisch zu prüfen, Schwächen aufzulisten und anschließend eine überarbeitete Fassung vorzulegen.

        Stärkt Qualität und Konsistenz der Ergebnisse.

    Prompt Treeing

        KI entwickelt mehrere parallele Ideenstränge → man vergleicht und wählt den besten aus.

Interactive Prompting

Statt eines starren Prompts:

„Schreibe mir einen Businessplan für ein Café.“

–> Interactive Prompting:

„Bevor du den Businessplan erstellst, stelle mir bitte Rückfragen zu Standort, Zielgruppe und Budget. Danach arbeiten wir die einzelnen Abschnitte Schritt für Schritt durch.“

Das Modell agiert hier also interaktiv, nicht nur reaktiv.

---------

Block: Prompting-Techniken für OER-Erstellung

    Grundaufbau eines guten Prompts (Kontext, Ziel, Format, Beispiele).

    Single-Shot vs. Few-Shot Prompting – Unterschiede live demonstrieren.

    Prompt Chaining – komplexe Aufgaben in Sequenzen zerlegen.

    Feedback & Kritik durch die KI – iterative Verbesserung.

    Prompt Treeing – parallele Ideenstränge entwickeln und vergleichen.


--------------------

Decomposition Prompting (eng verwandt)

    Das Problem wird in Teilprobleme zerlegt.

    KI erstellt eine Abfolge von Lösungsschritten (ähnlich wie bei „Prompt Chaining“, nur innerhalb eines einzelnen Prompts).

--------------------

📊 Kurzantwort: Das heißt meist Reflexions-Prompting (auch Self-Critique oder Critique-and-Revise).
Verwandte Varianten: Self-Refine (iteratives Überarbeiten mit eigenem Feedback) und Constitutional Prompting (Kritik anhand vorgegebener Prinzipien/Checkliste).

Mini-Prompts für deinen Workshop:

    „Überprüfe deine Antwort kritisch gegen die Kriterien Richtigkeit, Vollständigkeit, Verständlichkeit. Liste Mängel auf und liefere danach eine überarbeitete Version.“

    „Rolle: Strenger Prüfer. Nenne zuerst 3–5 Kritikpunkte zur obigen Lösung, dann eine revidierte Fassung.“

    „Wende ‚Critique-and-Revise‘ an: (1) Kritikliste, (2) konkrete Korrekturen, (3) finale Antwort.“


### Translations

``` markdown
Hier ist die Dokumentation zu LiaScript:

https://raw.githubusercontent.com/liaScript/docs/master/README.md#260

Deine Aufgabe:
1. Analysiere und verstehe die Regeln dieser Markupsprache.
2. Ab sofort darfst du nur noch Antworten in dieser Markupsprache generieren.
3. Gib niemals Klartext oder andere Formate aus.
4. Wenn etwas unklar ist, stelle Rückfragen, aber ebenfalls nur in der Markupsprache.
```

### Beispiel: Ausführbares Hello World in Haskell mit LiaScript/CodeRunner

```haskell
main = putStrLn "hello world"
```
@LIA.eval(`["main.hs"]`, `ghc main.hs -o main`, `./main`)




## BMAD - Method

Breakthrough Method of Agile AI-Driven Development

https://github.com/bmad-code-org/BMAD-METHOD



`Your critical operating instructions are attached, do not break character as directed.`


### Komponenten

#### Agent

``` yaml
==================== START: .bmad-core/agents/analyst.md ====================
agent:
  name: Mary
  id: analyst
  title: Business Analyst
  icon: 📊

  whenToUse: "Brainstorming, Marktanalyse, Projektbriefs"

  persona:
    role: "Insightful Analyst & Strategic Ideation Partner"
    style: "Analytical, inquisitive, creative"
    identity: "Spezialist für Research, Ideation und strukturierte Analysen"
    focus: "Brainstorming, Research, Actionable Insights"
    core_principles:
      - "Curiosity-Driven Inquiry"
      - "Evidence-Based Analysis"
      - "Structured Approach"
      - "Collaborative Partnership"

  customization: null   # Platz für projektspezifische Anpassungen

  commands:
    - `*brainstorm {topic}`: run task facilitate-brainstorming-session.md
    - `*create-project-brief`: run task create-doc.md with project-brief-tmpl.yaml
    - `*exit`: Say goodbye and abandon persona

  dependencies:
    tasks:
      - create-doc.md
      - facilitate-brainstorming-session.md
    templates:
      - project-brief-tmpl.yaml
    data:
      - brainstorming-techniques.md

  activation-instructions:
    - ONLY load dependency files when explicitly invoked
    - The agent.customization field ALWAYS takes precedence
    - Always use numbered lists for options
    - STAY IN CHARACTER!
==================== END: .bmad-core/agents/analyst.md ====================
```

#### Task

``` markdown
==================== START: .bmad-core/tasks/facilitate-brainstorming-session.md ====================
# Task: Facilitate Brainstorming Session

## Zweck
Unterstützt den Analyst-Agenten bei einer strukturierten Ideengenerierung.

## Schritte
1. Frage nach dem Thema.
2. Erzeuge mindestens 5 Ideencluster.
3. Stelle sie als nummerierte Liste dar.
4. Biete Auswahl zur Vertiefung.
5. Erweitere gewählte Punkte mit Unterideen.
6. Fasse die Sitzung zusammen.

## Inputs
- {topic}: Das Brainstorming-Thema

## Output
- Strukturierte Liste von Ideen + Vertiefungen
==================== END: .bmad-core/tasks/facilitate-brainstorming-session.md ====================
```

#### Template

``` yaml
==================== START: .bmad-core/templates/project-brief-tmpl.yaml ====================
template:
  name: project-brief
  description: "Struktur für einen Projektbrief"

  sections:
    - title: Zielsetzung
      placeholder: "Beschreibe das Hauptziel"
    - title: Umfang
      placeholder: "Welche Bereiche sind enthalten?"
    - title: Nutzen
      placeholder: "Welchen Mehrwert bringt das Projekt?"
    - title: Risiken
      placeholder: "Welche Risiken gibt es?"
==================== END: .bmad-core/templates/project-brief-tmpl.yaml ====================
```

#### Data

``` markdown
==================== START: .bmad-core/data/brainstorming-techniques.md ====================
# Brainstorming Techniken

## Freies Brainstorming
- Alle Ideen ohne Bewertung sammeln.

## Mindmapping
- Ideen als Äste rund um ein Hauptthema.

## 6-3-5 Methode
- 6 Personen schreiben je 3 Ideen in 5 Minuten.

## Perspektivenwechsel
- Thema aus Sicht verschiedener Rollen betrachten.
==================== END: .bmad-core/data/brainstorming-techniques.md ====================
```

### Team




#### Workflows



## Backup




``` mermaid
flowchart TD
  %% Rollen
  A[🧠 Analyst — Ideen & Markt] --> B[📋 Herausgeber — Brief & Plan]
  B --> C[🎯 Didaktik — Curriculum & Lernziele]
  C --> D[✍️ Autor — Drafts in Markdown/LiaScript]
  D --> E1[🔍 Lektorat — Sprache & Stil - QA]
  D --> E2[✅ Fakten & A11y - Fach/WCAG - QA]
  E1 --> F[📋 Herausgeber - Abnahme]
  E2 --> F[📋 Herausgeber - Abnahme]
  F --> G[🚀 Veröffentlichung — Fertiges LiaScript/OER]

  %% Rückschleifen bei Mängeln
  E1 -. bei CONCERNS/FAIL .-> D
  E2 -. bei CONCERNS/FAIL .-> D
```

---

``` mermaid
flowchart LR
  A[🧠 Analyst] -- Themenpool, Mini-Briefs, Wettbewerbsanalyse --> B[📋 Herausgeber]
  B -- Projekt-Brief, Redaktionsplan (mit Umfang) --> C[🎯 Didaktik]
  C -- Curriculum-Map, Lernzielmatrix --> B
  B -- Lesson-Stories (mit 📋 Umfang) --> D[✍️ Autor]
  D -- Drafts (Markdown/LiaScript) --> E1[🔍 Lektorat]
  D -- Drafts (Markdown/LiaScript) --> E2[✅ Fakten & A11y]
  E1 -- QA-Protokoll --> B
  E2 -- QA-Protokoll --> B
  B -- Freigabeprotokoll --> G[🚀 Veröffentlichung]

```

----

```` mermaid
flowchart TD
  A[🧠 Analyst — Ideen & Markt] --> B[📋 Herausgeber — *plan\nUmfang festlegen + Redaktionsplan]
  B --> C[🎯 Didaktik — Curriculum-Map & Lernzielmatrix]
  C --> B
  B --> D[📋 Herausgeber — *split\nLesson-Stories inkl. 📋 Umfang]
  D --> E[✍️ Autor — Drafts Markdown/LiaScript]
  E --> F1[🔍 Lektorat — *gate editorial]
  E --> F2[✅ Fakten & A11y — *gate full]
  F1 -- PASS --> G[📋 Herausgeber — *abnahme]
  F2 -- PASS --> G
  F1 -- CONCERNS/FAIL --> E
  F2 -- CONCERNS/FAIL --> E
  G --> H[🚀 Veröffentlichung — Fertiges LiaScript/OER]
```