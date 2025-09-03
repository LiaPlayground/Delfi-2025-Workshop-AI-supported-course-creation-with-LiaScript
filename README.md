<!--
import: https://raw.githubusercontent.com/LiaScript/CodeRunner/master/README.md
-->

# Delfi 2025 Workshop - AI-supported course creation with LiaScript

A compact tutorial on LiaScript, the open framework for interactive learning content. Learn how to use AI to generate questions, explanations, and exercises—making course creation efficient, time-saving, and pedagogically meaningful for educators and e-learning enthusiasts.


## LiaScript

LiaScript is an open framework for creating interactive learning content. It allows educators to design and publish courses that are engaging, adaptive, and easy to use.

## What is a good Prompt?




### Beispiel: Ausführbares Hello World in Haskell mit LiaScript/CodeRunner

```haskell
main = putStrLn "hello world"
```
@LIA.eval(`["main.hs"]`, `ghc main.hs -o main`, `./main`)




## BMAD - Method

`Your critical operating instructions are attached, do not break character as directed.`


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