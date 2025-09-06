# Prompting Education

> Prompting is the process of designing and refining input queries to AI models to achieve desired outputs. It involves crafting specific instructions or questions that guide the AI in generating relevant and accurate responses.

## The Anatomy of a Prompt

<section>

## 5 Step Framework (by Google)

1. __Task:__ What the AI shall do!
2. __Context:__ Background information and details relevant to the task.
3. __References:__ Any external sources or materials to consider.
4. __Evaluate:__ Criteria for assessing the output.
5. __Iterate:__ Process for refining the prompt based on feedback.

</section>

### 1. Task

__What the AI shall do!__

``` markdown
Make suggestions for a poetry course for 2nd graders.
```

    {{1}}
<section>

#### Persona

__Instead of only focusing on the task, instruct the AI to have a certain background.__

``` markdown
You are a teacher and a hobby poet that loves to inspire young minds.
Make suggestions for a poetry course for 2nd graders.
```

</section>

    {{2}}
<section>

#### Format

__Give detailed instructions on how the output should be structured and formatted and define upper bounds.__

``` markdown
You are a teacher and a hobby poet that loves to inspire young minds.
Make suggestions for a poetry course for 2nd graders.
Format the output as a table of 5 topics.
```

</section>


### 2. Context

The more context you can provide the better the AI can understand the task and generate relevant outputs. Consider including:

- Specific details about the target audience (e.g., age, background, interests, abilities, ...)
- Any constraints or limitations (e.g., word count, style guidelines)


    {{1}}
``` markdown
You are a teacher and a hobby poet that loves to inspire young minds.
Make suggestions for a poetry course for 2nd graders.

- The students have a basic understanding of language.
- Students come from diverse cultural backgrounds.
- Some of them are not fluent in English.
```

### 3. References

References are any external sources or materials that can provide additional context or information relevant to the task.

The AI is very very very good in using examples. So if you already have some specific material that you like, probably for another target group, you can share that as well.

    {{1}}
``` markdown
You are a teacher and a hobby poet that loves to inspire young minds.
Make suggestions for a poetry course for 2nd graders.

- The students have a basic understanding of language.
- Students come from diverse cultural backgrounds.
- Some of them are not fluent in English.

----

In Germany we have a poem format called "Elfchen" (Elevenie).

It consists of 11 words arranged in a specific pattern:

1. One word (the title)
2. Two words (describing the title)
3. Three words (expressing a feeling about the title)
4. Four words (describing a scene related to the title)
5. One word (a synonym for the title)

This format can be a simple starting point, encourages creativity
and helps young poets focus on specific aspects of their subject.
```

### 4. Evaluate & 5. Iterate

    {{1}}
__Is this the output that I wanted?__

    {{2}}
__If not, what can be improved? How can I refine the prompt to get closer to the desired output?__

### Tools

    {{1-2}}
??[ai-27](https://ai-27.com)


    {{2}}
??[Prompt-Library](https://aipromptlibrary.org/library.html)


### Libraries

- [AI for Education](https://www.aiforeducation.io/prompt-library)
- [Microsoft Prompts for Education](https://github.com/microsoft/prompts-for-edu)
- [UNIGlobal Careers Prompt Library](https://learn.uniglobalcareers.com/docs/prompt-library/)

## Techniques

### Single-Shot vs. Few-Shot Prompting

{{1}} __Single-Shot:__ nur ein Beispiel / direkte Frage.

{{2}} __Few-Shot:__ mehrere Beispiele --> die KI erkennt Muster.

    {{3}}
``` markdown
Dies sind zwei Kurse in LiaScript zur Programmierung in C# und Python.
Lade und analysiere sie zuerst

- https://raw.githubusercontent.com/TUBAF-IfI-LiaScript/VL_Softwareentwicklung/master/03_CsharpGrundlagenI.md
- https://raw.githubusercontent.com/TUBAF-IfI-LiaScript/VL_EAVD/refs/heads/master/07_PythonGrundlagen.md

Erzeuge mir einen einfachen Kurs zur Einführung in die Programmiersprache Lua
```

### Variables & Templates

`[ Variables ]` are placeholders that can be used to represent different values in a prompt.

Later these variables can be replaced with specific values when the prompt is executed. (`variable = new value`)

    {{1}}
``` markdown
Create a flashcard on the topic **{topic}**.

Target audience: **{audience}**

Format: Question–Answer

Difficulty level: **{level}**

Provide a concise question and a short, clear answer.
```

    {{2}}
``` markdown
{topic} = "Quantum computers"
{audience} = "First-year university students"
{level} = "high"
```

    {{3}}
``` markdown                 visualization
The following LiaScript code generates an interactive chart on different types of quadratic functions,
where the user can manipulate certain parameters.
Rewrite this to draw another [ visualization ] and change the number of input parameters, if required.
Mark this prompt as "UNDERSTOOD" when you are ready and wait for further instructions.

$a =$ <script modify="false" input="range" step="1"   min="-1"  max="6"  value="2" output="a">@input</script>,
$b =$ <script modify="false" input="range" step="0.1" min="-10" max="10" value="0" output="b">@input</script>,
$c =$ <script modify="false" input="range" step="0.1" min="-10" max="10" value="0" output="c">@input</script>

<script modify="false" run-once style="display: inline-block; width: 100%">
"LIASCRIPT: ### $$f(x) = x^{@input(`a`)} + x * @input(`b`) + @input(`c`)$$"
</script>

<script run-once style="display: inline-block; width: 100%">
function func(x) {
  return Math.pow(x,  @input(`a`)) + @input(`b`) * x + @input(`c`);
}

function generateData() {
  let data = [];
  for (let i = -15; i <= 15; i += 0.01) {
    data.push([i, func(i)]);
  }
  return data;
}

let option = {
  grid: { top: 40, left: 50, right: 40, bottom: 50 },
  xAxis: {
    name: 'x',
    minorTick: { show: true },
    splitLine: { lineStyle: { color: '#999' } },
    minorSplitLine: { show: true, lineStyle: { color: '#ddd' } }
  },
  yAxis: {
    name: 'y', min: -10, max: 10,
    minorTick: { show: true },
    splitLine: { lineStyle: { color: '#999' } },
    minorSplitLine: { show: true, lineStyle: { color: '#ddd' } }
  },
  series: [
    {
      type: 'line',
      showSymbol: false,
      data: generateData()
    }
  ]
};

"HTML: <lia-chart option='" + JSON.stringify(option) + "'></lia-chart>"
</script>
```

### Chain of Thought (CoT)

> Chain of Thought prompting is a technique that encourages the AI to break down complex tasks into smaller, manageable steps.
> This approach helps the AI to reason through the problem and arrive at a more accurate solution.

    {{1}}
``` markdown
You are an expert educational content creator.

Task: Generate a short lesson about **{topic}** for **{audience}**.

Think step by step before writing the final output:

1. Identify the key learning objective for {audience}.
2. Break down the topic into 3–4 simple sub-concepts in logical order.
3. For each sub-concept, think of a clear explanation and one concrete example.
4. Anticipate one common misconception and explain how to avoid it.
5. Based on these steps, write the final educational text in clear, engaging language.

Now, follow this reasoning process internally and then produce only the final educational content.

Answer this template with "understood" and wait for further instructions.
```

    {{2}}
``` markdown
- {topic} = "poetry with elfchen"
- {audience} = "2nd grade students"
```

### Tree of Thought (ToT)

> Tree of Thought prompting is a more advanced version of Chain of Thought prompting.
> It allows the AI to explore multiple branches of reasoning simultaneously, leading to more comprehensive and nuanced outputs.

    {{1}}
``` markdown
You are an expert educational content creator.

Task: Generate a short lesson about **{topic}** for **{audience}**.

Think step by step before writing the final output:

1. Identify the three key learning objective for {audience}.
   Let the user decide on the specific objectives, before you go one with the next step.

2. Break down the topic into 3 distinct sets sub-concepts in logical order.
   Wait for the user to confirm the sub-concepts before proceeding.

3. For each sub-concept, think of a three variations of clear explanation and one concrete example.
   Print every explanation and example in an ordered list and let the user choose one of them.

4. Anticipate a list of common misconceptions and explain how to avoid it.
   Print every misconception and its explanation in an ordered list and let the user choose some of them.

5. Based on these steps, write the final educational text in clear, engaging language.

Now, follow this reasoning process internally and then produce only the final educational content.

Answer this template with "understood" and wait for further instructions.
```

    {{2}}
``` markdown
- {topic} = "poetry with elfchen"
- {audience} = "2nd grade students"
```

### Decomposition Prompting

> Decomposition prompting is a technique where the AI is guided to break down a complex problem into smaller, more manageable sub-problems.
> This approach helps the AI to focus on each part of the problem individually, leading to more effective solutions.

``` markdown markdown
You are an expert educational content creator.
Task: Generate a comprehensive course outline on **{topic}** for **{audience}**.
Think step by step before writing the final output:

1. Decompose the main topic into 4–5 major modules.
2. For each module, identify 3–4 key lessons or concepts.
3. For each lesson, suggest one engaging activity or assessment method.
4. Compile the modules, lessons, and activities into a structured course outline.

Now, follow this reasoning process internally and then produce only the final course outline.
Answer this template with "understood" and wait for further instructions.
```

``` markdown
- {topic} = "basic programming"
- {audience} = "high school students"
```

### Reflexions-Prompting (Self-Critique / Critique-and-Revise)

> Reflexions-Prompting is a technique where the AI is encouraged to critically evaluate its own outputs and make improvements based on that evaluation.
> This process involves identifying weaknesses, suggesting concrete corrections, and ultimately delivering a refined response.


    {{1}}
``` markdown
Critically evaluate the lesson against the criteria of accuracy, completeness, and clarity.
```

----

    {{2}}
``` markdown
You are an expert educational content creator.
Task: Generate a short lesson about **{topic}** for **{audience}**.
Think step by step before writing the final output:
1. Write the initial lesson content.
2. Critically evaluate the lesson against the criteria of accuracy, completeness, and clarity.
3. List 3–5 specific weaknesses or areas for improvement.
4. Suggest concrete corrections or enhancements for each identified weakness.
5. Produce a revised version of the lesson that incorporates these improvements.
Now, follow this reasoning process internally and then produce only the final revised lesson content.
Answer this template with "understood" and wait for further instructions.
```

``` markdown
- {topic} = "photosynthesis"
- {audience} = "middle school students"
```

### Translator

``` markdown
Hier ist die Dokumentation zu LiaScript:

https://raw.githubusercontent.com/liaScript/docs/master/README.md#260

Deine Aufgabe:
1. Analysiere und verstehe die Regeln dieser Markupsprache.
2. Ab sofort darfst du nur noch Antworten in dieser Markupsprache generieren.
3. Gib niemals Klartext oder andere Formate aus.
4. Wenn etwas unklar ist, stelle Rückfragen, aber ebenfalls nur in der Markupsprache.
```

### Translating Formats

https://github.com/liascript/markdownify

??[Markdownify](https://liascript.github.io/Markdownify/)


```` markdown   -Markdownify Prompt
The following JSON schema defines the structure of a LiaScript document.
Analyze the schema to understand the key components and their relationships.
Then, whenever the command `Markdownify` is invoked,
translate the relevant content into this JSON format and print.

``` json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://raw.githubusercontent.com/LiaScript/Markdownify/refs/heads/main/liascript.schema.json",
  "title": "LiaScript Document",
  "$comment": "This is the **original** LiaScript JSON‑Schema enriched only with additional `description`, `examples`, and `$comment` annotations so that generative AI systems can more easily understand the intent and capabilities of LiaScript. **No structural validation rules were changed** – every extra field added here is purely documentary.",

  "type": "object",
  "properties": {
    "meta": {
      "type": "object",
      "description": "Document‑level metadata injected via the `<!-- meta: ... -->` macro at the very top of a LiaScript file. Unknown keys are permitted and simply forwarded to the runtime, which allows custom macros and future extensions.",
      "$comment": "Typical extra keys include `scripts`, `css`, `imports`, and `macros`. These are not validated explicitly here because LiaScript intentionally keeps the meta block open‑ended, but AIs SHOULD know they exist and feel free to emit them.",
      "properties": {
        "author": {
          "type": "string",
          "description": "Primary author or authors. Multiple names can be separated by comma or semicolon."
        },
        "email": {
          "type": "string",
          "description": "Contact e‑mail address shown in the about dialog and exported into ePub metadata."
        },
        "language": {
          "type": "string",
          "description": "ISO‑639‑1 language code (e.g. `en`, `de`, `es`)."
        },
        "mode": {
          "type": "string",
          "enum": ["Presentation", "Textbook", "Slides"],
          "description": "Preferred presentation mode, otherwise the default user mode is used."
        },
        "dark": {
          "type": "boolean",
          "description": "Force dark theme regardless of viewer preference or auto‑detection."
        },
        "narrator": {
          "@ref": "#/definitions/Voice",
          "description": "Default TTS voice (see the `Voice` enum)."
        }
      },
      "examples": [
        {
          "author": "Ada Lovelace; Alan Turing",
          "email": "course@example.org",
          "language": "en",
          "mode": "slides",
          "scripts": ["https://example.org/3d-panorama.js"],
          "css": ["https://example.org/theme-dark.css"],
          "imports": [
            "https://raw.githubusercontent.com/LiaTemplates/CodeRunner/master/README.md"
          ]
        }
      ],
      "additionalProperties": true
    },

    "sections": {
      "type": "array",
      "items": { "$ref": "#/definitions/section" }
    }
  },

  "required": ["sections"],

  "$comment": "------------------------------------------------------------\nATTR FIELD\n------------------------------------------------------------\nEvery Block or inline element MAY contain an `attr` object. It is passed straight through to the resulting HTML tag, so any valid attribute name is accepted. Common examples include: \n  { \"id\": \"hero\", \"class\": [\"center\", \"fade-in\"], \"style\": \"color:#e91e63;\", \"data-step\": 3 }.\nLLMs should treat `attr` as a free‑form bag of key/value pairs for styling, ARIA roles, data‑attributes, etc.",

  "definitions": {
    "section": {
      "type": "object",
      "properties": {
        "title": {
          "type": "string",
          "description": "Section heading (Markdown line starting with one or more `#`)."
        },
        "indent": {
          "type": "integer",
          "minimum": 1,
          "maximum": 6,
          "description": "Heading level depth. Courses usually start at 1."
        },
        "body": { "$ref": "#/definitions/Blocks" },
        "meta": {
          "type": "object",
          "description": "Local overrides for narrator, author, etc. Same structure as the top‑level meta block."
        }
      },
      "required": ["title", "indent", "body"]
    },

    "StringOrList": {
      "oneOf": [
        { "type": "string" },
        {
          "type": "array",
          "items": {
            "type": "string"
          },
          "description": "Each string represents a line. When rendered, all lines are concatenated with a newline separator so authors can keep long code or formulas readable."
        }
      ]
    },

    "Blocks": {
      "type": "array",
      "items": {
        "oneOf": [
          { "$ref": "#/definitions/Block" },
          { "$ref": "#/definitions/inlines" }
        ]
      },
      "description": "An ordered list of block‑level elements. For convenience, a single inline (or an array of inlines) can also stand in as a block so authors don't have to wrap e.g. a lone image inside a `Paragraph`."
    },

    "Block": {
      "oneOf": [
        { "$ref": "#/definitions/Paragraph" },
        { "$ref": "#/definitions/Line" },
        { "$ref": "#/definitions/Comment" },
        { "$ref": "#/definitions/Effect" },
        { "$ref": "#/definitions/Gallery" },
        { "$ref": "#/definitions/Formula" },
        { "$ref": "#/definitions/Quote" },
        { "$ref": "#/definitions/List" },
        { "$ref": "#/definitions/Html" },
        { "$ref": "#/definitions/Code" },
        { "$ref": "#/definitions/Table" },
        { "$ref": "#/definitions/Tasks" },
        { "$ref": "#/definitions/Quiz" },
        { "$ref": "#/definitions/Ascii" },
        { "$ref": "#/definitions/Chart" }
      ]
    },

    "Paragraph": {
      "type": "object",
      "properties": {
        "type": { "const": "Paragraph" },
        "body": { "$ref": "#/definitions/inlines" },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "A block element that displays its content as a paragraph. The 'body' can be a string, a single inline element, or an array of strings and inlines. Additional HTML attributes can be set via 'attr' for custom styling."
    },

    "Line": {
      "type": "object",
      "properties": {
        "type": { "const": "Line" },
        "attr": { "type": "object" }
      },
      "required": ["type"],
      "description": "A horizontal line, corresponds to hr tag in html, can be styled via attr and has no body"
    },

    "Comment": {
      "type": "object",
      "properties": {
        "type": { "const": "Comment" },
        "body": {
          "$ref": "#/definitions/inlines",
          "description": "The content of the comment, which can be a string, a single inline element, or an array of strings and inlines. This text will be read aloud by the TTS engine at the specified animation step."
        },
        "start": {
          "type": "integer",
          "minimum": 0,
          "description": "The animation step at which this comment will be read aloud in Presentation or Slides mode."
        },
        "voice": {
          "$ref": "#/definitions/Voice",
          "description": "Overrides the default TTS voice for this comment. Optional."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "A comment is a paragraph that will be read aloud by the TTS engine at a specific animation step in Presentation or Slides mode. In Textbook mode, it is rendered as visible text. Comments are typically used to narrate or explain animation steps. If multiple comments share the same 'start' value, they are read together in order of appearance."
    },

    "Effect": {
      "type": "object",
      "properties": {
        "type": { "const": "Effect" },
        "body": {
          "oneOf": [
            { "$ref": "#/definitions/Block" },
            { "$ref": "#/definitions/Blocks" }
          ],
          "description": "The content to animate. Can be a single block or an array of blocks."
        },
        "start": {
          "type": "integer",
          "minimum": 0,
          "description": "Step when the effect appears (optional)."
        },
        "stop": {
          "type": "integer",
          "description": "Step when the effect disappears, should only be defined in combination with start (optional)."
        },
        "playback": {
          "type": "boolean",
          "description": "If true, adds a TTS playback button (optional)."
        },
        "voice": {
          "$ref": "#/definitions/Voice",
          "description": "Specifies the TTS voice to use for playback. Only relevant if 'playback' is true. Overrides the default voice set at the document or section level (optional)."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "A block element that animates its content to appear and/or disappear at specific steps in a slide. Optionally, a TTS playback button can be added, and a custom voice can be set for spoken output."
    },

    "Gallery": {
      "type": "object",
      "properties": {
        "type": { "const": "Gallery" },
        "body": {
          "type": "array",
          "items": { "$ref": "#/definitions/multimedia" },
          "description": "An array of multimedia links (image, audio, video, or embed) to display in the gallery."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Displays a gallery of media elements. The body must be an array of multimedia links."
    },

    "Formula": {
      "type": "object",
      "properties": {
        "type": { "const": "Formula" },
        "body": {
          "$ref": "#/definitions/StringOrList",
          "description": "The formula content in KaTeX syntax. Can be a single string or an array of strings (for readability); if an array, lines are joined with newlines before rendering."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Displays a mathematical formula using KaTeX. The body can be a single string or an array of strings for multi-line formulas."
    },

    "Quote": {
      "type": "object",
      "properties": {
        "type": { "const": "Quote" },
        "body": {
          "oneOf": [
            { "$ref": "#/definitions/Block" },
            { "$ref": "#/definitions/Blocks" }
          ],
          "description": "The quoted content. Can be a single block or an array of blocks."
        },
        "by": {
          "$ref": "#/definitions/inlines",
          "description": "Optional. If provided, displays the quote as a citation with the given author or source."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Displays a blockquote. The 'body' contains the quoted content (single block or array of blocks). If 'by' is set, the quote is rendered as a citation."
    },

    "List": {
      "type": "object",
      "properties": {
        "type": { "const": "List" },
        "body": {
          "oneOf": [
            { "$ref": "#/definitions/Block" },
            { "$ref": "#/definitions/Blocks" }
          ],
          "description": "The quoted content. Can be a single block or an array of blocks."
        },
        "ordered": {
          "type": "boolean",
          "description": "Defines if it is an ordered or an unordered list, by default it is false."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Displays an ordered or unordered list of block elements. The 'body' contains list entries as blocks or nested blocks."
    },

    "Html": {
      "type": "object",
      "properties": {
        "type": { "const": "Html" },
        "htmlTag": {
          "type": "string",
          "description": "Define an inline html tag name like div, span, etc."
        },
        "body": {
          "oneOf": [
            { "$ref": "#/definitions/Block" },
            { "$ref": "#/definitions/Blocks" }
          ]
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "htmlTag", "body"],
      "description": "In contrast to an html inline element, this body can contain entire Block elements."
    },

    "Code": {
      "type": "object",
      "properties": {
        "type": { "const": "Code" },
        "title": { "type": "string", "description": "A filename" },
        "language": {
          "type": "string",
          "description": "This is a short code for the used syntax highlighting, such java, markdown, cpp, lua, prolog, etc."
        },
        "closed": {
          "type": "boolean",
          "description": "Defines if the content of the file shall be hidden at first, the user can decide to open it afterwards."
        },
        "body": { "$ref": "#/definitions/StringOrList" },
        "execute": {
          "$ref": "#/definitions/StringOrList",
          "description": "This optional property that makes the code block editable and executable. It contains JavaScript with an @input marker. This marker is replaced before the execution with the current content of the code-block."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "This will show an entire code block with syntax highlighting and an optional title. The execute field will turn the code-block into an editor with a run button that will execute the code."
    },

    "Table": {
      "type": "object",
      "properties": {
        "type": { "const": "Table" },
        "head": {
          "type": "array",
          "items": { "$ref": "#/definitions/inlines" },
          "description": "Defines the table header. Each entry represents the content of a column header and can be a string, a single inline element, or an array of inlines."
        },
        "alignment": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["left", "right", "center"]
          },
          "description": "Specifies the alignment of each column: 'left', 'right', or 'center'. The number of entries must match the number of columns in the header. If omitted, all columns default to left alignment."
        },
        "body": {
          "type": "array",
          "items": {
            "type": "array",
            "items": { "$ref": "#/definitions/inlines" }
          },
          "description": "Defines the table rows. Each row is an array of cells, and each cell can contain a string, a single inline element, or an array of inlines."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "head", "body"],
      "description": "Displays a table with a header, optional column alignment, and a body of rows. Each cell can contain rich inline content. Additional HTML attributes can be set via 'attr' for custom styling."
    },

    "Tasks": {
      "type": "object",
      "properties": {
        "type": { "const": "Tasks" },
        "body": {
          "type": "array",
          "items": { "$ref": "#/definitions/inlines" },
          "description": "An array of task descriptions. Each entry represents a single task and can contain text or rich inline content."
        },
        "done": {
          "$ref": "#/definitions/Solution",
          "description": "Defines which tasks are marked as completed. Can be a single integer (one checked), an array of integers (multiple checked), an empty array (none checked), or a boolean array (true for checked tasks)."
        },
        "attr": {
          "type": "object",
          "description": "Optional HTML attributes for custom styling or additional properties."
        }
      },
      "required": ["type", "body", "done"],
      "description": "Displays a GitHub-flavored task list. Each task can contain rich inline content. The 'done' property specifies which tasks are checked."
    },

    "Quiz": {
      "type": "object",
      "properties": {
        "type": { "const": "Quiz" },
        "quizType": {
          "type": "string",
          "enum": [
            "input",
            "selection",
            "single-choice",
            "multiple-choice",
            "gap-text"
          ],
          "description": "Specifies the type of quiz. Determines the interaction style and which properties are required. \n\n- 'input': A single-line text input where the user's answer is matched against a solution string.\n- 'selection': A dropdown menu where the user selects one or more options from a list.\n- 'single-choice': A list of radio buttons where only one option can be selected.\n- 'multiple-choice': A list of checkboxes where multiple options can be selected.\n- 'gap-text': A fill-in-the-blank quiz where input/select elements are placed directly in the content."
        },
        "hints": {
          "type": "array",
          "items": { "$ref": "#/definitions/inlines" },
          "description": "Optional hints to assist the user in solving the quiz."
        },
        "answer": {
          "oneOf": [
            { "$ref": "#/definitions/Block" },
            { "$ref": "#/definitions/Blocks" }
          ],
          "description": "The answer or solution block(s) for the quiz. Revealed only after the user solves the quiz or requests the solution."
        },
        "execute": {
          "$ref": "#/definitions/StringOrList",
          "description": "Optional code to execute for code-based quizzes. The @input marker within the code block will be replaced with the user's input or the selected option index, allowing for custom processing."
        }
      },
      "required": ["type", "quizType"],
      "allOf": [
        {
          "if": { "properties": { "quizType": { "const": "input" } } },
          "then": {
            "required": ["type", "quizType", "solution"],
            "properties": {
              "solution": {
                "type": "string",
                "description": "The user input will be matched against this string. Trailing whitespace is ignored."
              }
            },
            "description": "A quiz block presenting a single-line text input. The user's input is checked against the 'solution' string."
          }
        },
        {
          "if": { "properties": { "quizType": { "const": "selection" } } },
          "then": {
            "required": ["type", "quizType", "solution", "body"],
            "properties": {
              "body": {
                "type": "array",
                "items": { "$ref": "#/definitions/inlines" },
                "description": "An array of selectable options presented in a dropdown menu. Each option can contain rich inline content."
              },
              "solution": {
                "$ref": "#/definitions/Solution",
                "description": "Defines the correct answer(s) for the dropdown. Can be a single integer, an array of integers, an empty array, or a boolean array."
              }
            },
            "description": "A quiz block presenting a dropdown field with multiple options. The user's selection is checked against the 'solution'."
          }
        },
        {
          "if": { "properties": { "quizType": { "const": "single-choice" } } },
          "then": {
            "required": ["type", "quizType", "solution", "body"],
            "properties": {
              "body": {
                "type": "array",
                "items": { "$ref": "#/definitions/inlines" },
                "description": "An array of options presented as radio buttons. Each option can contain rich inline content."
              },
              "solution": {
                "$ref": "#/definitions/Solution",
                "description": "Defines the correct answer for the radio buttons. Should be a single integer."
              }
            },
            "description": "A quiz block presenting a list of radio buttons. The user's selection is checked against the 'solution'."
          }
        },
        {
          "if": {
            "properties": { "quizType": { "const": "multiple-choice" } }
          },
          "then": {
            "required": ["type", "quizType", "solution", "body"],
            "properties": {
              "body": {
                "type": "array",
                "items": { "$ref": "#/definitions/inlines" },
                "description": "An array of options presented as checkboxes. Each option can contain rich inline content."
              },
              "solution": {
                "$ref": "#/definitions/Solution",
                "description": "Defines the correct answers for the checkboxes. Can be an array of integers or booleans."
              }
            },
            "description": "A quiz block presenting a list of checkboxes, where multiple options can be selected. The user's selection is checked against the 'solution'."
          }
        },
        {
          "if": { "properties": { "quizType": { "const": "gap-text" } } },
          "then": {
            "required": ["type", "quizType", "body"],
            "properties": {
              "body": {
                "oneOf": [
                  { "$ref": "#/definitions/Paragraph" },
                  { "$ref": "#/definitions/Table" },
                  { "$ref": "#/definitions/Gallery" },
                  { "$ref": "#/definitions/Quote" }
                ],
                "description": "The block containing the gap(s) for fill-in-the-blank quizzes. Inline input/select elements define the gaps."
              }
            },
            "description": "A quiz block presenting a gap text. No 'solution' is required, as the correct answers are defined by inline input and select elements within the body."
          }
        }
      ],
      "description": "A flexible quiz block supporting various quiz types:\n- 'input': Single-line text input matched against a solution string.\n- 'select': Dropdown menu with selectable options.\n- 'single-choice': Radio buttons for single selection.\n- 'multiple-choice': Checkboxes for multiple selections.\n- 'gap-text': Fill-in-the-blank with inline input/select elements.\n\nThe structure and required properties depend on the selected 'quizType'. The actual quiz question should be defined in a separate block or paragraph above the quiz-block."
    },

    "Ascii": {
      "type": "object",
      "properties": {
        "type": { "const": "Ascii" },
        "title": {
          "$ref": "#/definitions/inlines",
          "description": "Image title"
        },

        "body": { "$ref": "#/definitions/StringOrList" },

        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "This is an ASCII-art image, with support for boxes, lines, arrows, text and Unicode and emojis."
    },

    "Chart": {
      "type": "object",
      "properties": {
        "type": { "const": "Chart" },

        "body": { "$ref": "#/definitions/StringOrList" },

        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "This is a special type of diagram drawn as an ASCII art with points x an y axes and values in form of +,*,#,a,b,c, ...."
    },

    "inlines": {
      "oneOf": [
        {
          "type": "array",
          "items": { "$ref": "#/definitions/inline" }
        },
        { "$ref": "#/definitions/inline" }
      ]
    },

    "inline": {
      "oneOf": [
        { "$ref": "#/definitions/bold" },
        { "$ref": "#/definitions/italic" },
        { "$ref": "#/definitions/strike" },

        { "$ref": "#/definitions/sup" },
        { "$ref": "#/definitions/underline" },
        { "$ref": "#/definitions/effect" },
        { "$ref": "#/definitions/html" },
        { "$ref": "#/definitions/script" },
        { "$ref": "#/definitions/code" },
        { "$ref": "#/definitions/footnote" },
        { "$ref": "#/definitions/formula" },
        { "$ref": "#/definitions/symbol" },

        { "$ref": "#/definitions/link" },
        { "$ref": "#/definitions/multimedia" },

        { "$ref": "#/definitions/input" },
        { "$ref": "#/definitions/select" },

        { "type": "string" }
      ]
    },

    "bold": {
      "type": "object",
      "properties": {
        "type": { "const": "bold" },
        "body": { "$ref": "#/definitions/inlines" },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "An inline element that displays its content in bold. --> __bold text__"
    },

    "italic": {
      "type": "object",
      "properties": {
        "type": { "const": "italic" },
        "body": { "$ref": "#/definitions/inlines" },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Displays the contained elements in italic text. --> _italic text_"
    },

    "strike": {
      "type": "object",
      "properties": {
        "type": { "const": "strike" },
        "body": { "$ref": "#/definitions/inlines" },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Displays the contained elements with a strikethrough (crossed out). --> ~striked text~"
    },

    "sup": {
      "type": "object",
      "properties": {
        "type": { "const": "sup" },
        "body": { "$ref": "#/definitions/inlines" },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Displays the contained elements as superscript (raised text). --> ^bold text^"
    },

    "underline": {
      "type": "object",
      "properties": {
        "type": { "const": "underline" },
        "body": { "$ref": "#/definitions/inlines" },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Displays the contained elements with an underline. --> ~~underlined text~~"
    },

    "html": {
      "type": "object",
      "properties": {
        "type": { "const": "html" },
        "htmlTag": {
          "type": "string",
          "description": "Define an inline html tag name like div, span, etc."
        },
        "body": { "$ref": "#/definitions/inlines" },
        "attr": { "type": "object" }
      },
      "required": ["type", "htmlTag"],
      "description": "Displays an inline HTML element that might contain further inline elements, parameters are defined in attr."
    },

    "script": {
      "type": "object",
      "properties": {
        "type": { "const": "script" },

        "body": {
          "oneOf": [
            { "type": "string" },
            {
              "type": "array",
              "items": { "type": "string" },
              "description": "Each string represents a line; all lines will be joined with a newline separator."
            }
          ]
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Create a script tag with code from the body. The body can be a single string or an array of strings (joined with newlines for readability)."
    },

    "code": {
      "type": "object",
      "properties": {
        "type": { "const": "code" },

        "body": { "type": "string" },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Display a verbatim element, the body will be displayed as it is."
    },

    "footnote": {
      "type": "object",
      "properties": {
        "type": { "const": "footnote" },
        "body": { "type": "string" },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Add a reference to a footnote block element."
    },

    "formula": {
      "type": "object",
      "properties": {
        "type": { "const": "formula" },
        "body": { "type": "string" },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Use KaTeX formatted formulas in the string."
    },

    "effect": {
      "type": "object",
      "properties": {
        "type": { "const": "effect" },
        "body": { "$ref": "#/definitions/inlines" },
        "start": {
          "type": "integer",
          "minimum": 0,
          "description": "Step when the effect appears (optional)."
        },
        "stop": {
          "type": "integer",
          "description": "Step when the effect disappears, should only be defined in combination with start (optional)."
        },
        "playback": {
          "type": "boolean",
          "description": "If true, adds a TTS playback button (optional)."
        },
        "voice": {
          "$ref": "#/definitions/Voice",
          "description": "Specifies the TTS voice to use for playback. Only relevant if 'playback' is true. Overrides the default voice set at the document or section level (optional)."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "An inline element that animates its content to appear and/or disappear at specific steps in a slide. Optionally, a TTS playback button can be added, and a custom voice can be set for spoken output."
    },

    "link": {
      "type": "object",
      "properties": {
        "type": { "const": "link" },
        "url": {
          "type": "string",
          "description": "The target URL for the hyperlink."
        },
        "body": {
          "$ref": "#/definitions/inlines",
          "description": "The link text. If omitted, the URL is shown."
        },
        "title": {
          "$ref": "#/definitions/inlines",
          "description": "A title or tooltip for the link. Optional."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "url"],
      "description": "Specifies a hyperlink"
    },

    "multimedia": {
      "type": "object",
      "properties": {
        "type": { "const": "multimedia" },
        "embedType": {
          "type": "string",
          "enum": ["image", "audio", "video", "embed"]
        },
        "alt": { "$ref": "#/definitions/inlines" },
        "url": { "type": "string" },
        "title": { "$ref": "#/definitions/inlines" }
      },
      "required": ["type", "embedType", "url"],
      "description": "Embed a multimedia resource (image, audio, video, or embeddable content via oEmbed)."
    },

    "symbol": {
      "type": "object",
      "properties": {
        "type": { "const": "symbol" },
        "body": {
          "oneOf": [
            { "$ref": "#/definitions/symbols" },
            {
              "type": "string",
              "description": "Any Unicode character, such as an emoji or special symbol."
            }
          ]
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body"],
      "description": "Displays a single symbol, such as an arrow, emoji, or any Unicode character. Use a predefined symbol from the list or provide any string for custom symbols or emojis."
    },

    "input": {
      "type": "object",
      "properties": {
        "type": { "const": "input" },
        "solution": {
          "type": "string",
          "description": "The correct answer that user input will be checked against. Trailing whitespaces in the user's input will be ignored during comparison."
        },
        "length": {
          "type": "integer",
          "description": "Specifies the visible width of the input field in characters. Should be greater than or equal to the length of the solution. Optional."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "solution"],
      "description": "An inline text input field, typically used for fill-in-the-blank (GapText) quizzes. The 'solution' property defines the correct answer."
    },

    "select": {
      "type": "object",
      "properties": {
        "type": { "const": "select" },
        "solution": {
          "$ref": "#/definitions/Solution",
          "description": "Defines the correct answer(s) for the dropdown. Can be a single integer (for one correct option), an array of integers (for multiple correct options), an empty array (if no selection is correct), or an array of booleans (where 'true' marks the correct options)."
        },
        "body": {
          "type": "array",
          "items": { "$ref": "#/definitions/inlines" },
          "description": "The selectable options displayed in the dropdown. Each option can be any inline element, including text, images, formulas, HTML, etc."
        },
        "attr": { "type": "object" }
      },
      "required": ["type", "body", "solution"],
      "description": "Displays a dropdown menu with selectable options, typically used for fill-in-the-blank (GapText) quizzes. The 'body' property defines the list of options, and the 'solution' property specifies which option(s) are correct."
    },

    "Solution": {
      "description": "Defines the correct answer(s) for selection-based quizzes. Can be a single integer (for one correct option), an array of integers (for multiple correct options), an empty array (if no selection is correct), or an array of booleans (where 'true' marks the correct options).",
      "oneOf": [
        {
          "type": "integer",
          "description": "A single integer indicating the index of the correct option."
        },
        {
          "type": "array",
          "items": { "type": "integer" },
          "description": "An array of integers indicating the indices of all correct options. Use an empty array if no selection is correct."
        },
        {
          "type": "array",
          "items": { "type": "boolean" },
          "description": "An array of booleans, where each 'true' value marks the corresponding option as correct."
        }
      ]
    },

    "symbols": {
      "type": "string",
      "enum": [
        "<-->",
        "<--",
        "-->",
        "<<-",
        "->>",
        "<->",
        ">->",
        "<-<",
        "->",
        "<-",
        "<~",
        "~>",
        "<==>",
        "==>",
        "<==",
        "<=>",
        "=>",
        "<=",
        ":-)",
        ";-)",
        ":-D",
        ":-O",
        ":-(",
        ":-|",
        ":-/",
        ":-\\",
        ":-P",
        ":-p",
        ";-P",
        ";-p",
        ":-*",
        ";-*",
        ":')",
        ":'(",
        ":'[",
        ":-[",
        ":-#",
        ":-X",
        ":-§"
      ],
      "description": "A predefined symbol, such as an arrow, emoticon, or other special character. Use one of these for common symbols, or provide any Unicode string in the 'body' property for custom symbols or emojis."
    },
    "Voice": {
      "type": "string",
      "enum": [
        "UK English Female",
        "UK English Male",
        "US English Female",
        "US English Male",
        "Afrikaans Male",
        "Albanian Male",
        "Arabic Female",
        "Arabic Male",
        "Armenian Male",
        "Australian Female",
        "Australian Male",
        "Bangla Bangladesh Female",
        "Bangla Bangladesh Male",
        "Bangla India Female",
        "Bangla India Male",
        "Bosnian Male",
        "Brazilian Portuguese Female",
        "Brazilian Portuguese Male",
        "Catalan Male",
        "Chinese Female",
        "Chinese Male",
        "Chinese (Hong Kong) Female",
        "Chinese (Hong Kong) Male",
        "Chinese Taiwan Female",
        "Chinese Taiwan Male",
        "Croatian Male",
        "Czech Female",
        "Czech Male",
        "Danish Female",
        "Danish Male",
        "Deutsch Female",
        "Deutsch Male",
        "Dutch Female",
        "Dutch Male",
        "Esperanto Male",
        "Estonian Male",
        "Filipino Female",
        "Finnish Female",
        "Finnish Male",
        "French Canadian Female",
        "French Canadian Male",
        "French Female",
        "French Male",
        "Greek Female",
        "Greek Male",
        "Hindi Female",
        "Hindi Male",
        "Hungarian Female",
        "Hungarian Male",
        "Icelandic Male",
        "Indonesian Female",
        "Indonesian Male",
        "Italian Female",
        "Italian Male",
        "Japanese Female",
        "Japanese Male",
        "Korean Female",
        "Korean Male",
        "Latin Female",
        "Latin Male",
        "Latvian Male",
        "Macedonian Male",
        "Moldavian Female",
        "Moldavian Male",
        "Montenegrin Male",
        "Nepali",
        "Norwegian Female",
        "Norwegian Male",
        "Polish Female",
        "Polish Male",
        "Portuguese Female",
        "Portuguese Male",
        "Romanian Female",
        "Romanian Male",
        "Russian Female",
        "Russian Male",
        "Serbian Male",
        "Serbo-Croatian Male",
        "Sinhala",
        "Slovak Female",
        "Slovak Male",
        "Spanish Female",
        "Spanish Male",
        "Spanish Latin American Female",
        "Spanish Latin American Male",
        "Swahili Male",
        "Swedish Female",
        "Swedish Male",
        "Tamil Female",
        "Tamil Male",
        "Thai Female",
        "Thai Male",
        "Turkish Female",
        "Turkish Male",
        "Ukrainian Female",
        "Vietnamese Female",
        "Vietnamese Male",
        "Welsh Male"
      ],
      "description": "TTS voice to use (optional)."
    }
  }
}
```
````

## Video generation & narration

> heygen is an AI-powered video generation platform that allows users to create high-quality videos from text prompts. It offers a range of customization options, including voice selection, video style, and more.
>
> ![heygen screenshot](img/heygen.png)
>
> https://www.heygen.com

    {{1}}
!?[LiaScript Hello World example](https://www.youtube.com/watch?v=YYhvGnE1PAA)

### How is it done?

````markdown
    --{{1}}--
This is a comment, where the last or the first element is a video or and audio element.
?[audio](todo#t=start,end)

     {{1}}
This is a markdown-block that will appear on the first animation step.
````

## AI Workflows

### n8n

> n8n is a powerful open-source workflow automation tool that allows you to connect various services and automate tasks. It can be used to create complex workflows with minimal coding.
>
> ![n8n screenshot](img/n8n.png)
>
> https://n8n.io


    {{1}}
!?[n8n Tutorial](https://www.youtube.com/watch?v=ONgECvZNI3o)

### Google Opal

> Googles Opal is an AI for generating workflows from prompts, it is not available in the EU.
>
> ![Opal screenshot](img/opal.png)

    {{1}}
1. Download and install the [Opera browser](https://www.opera.com/de/download)
2. Enable the VPN and choose a location inside the US.
3. Visit: https://opal.withgoogle.com


## Local AIs

![LM Studio screenshot](img/LM-Studio.png)

https://lmstudio.ai



## BMAD - Method

Breakthrough Method of Agile AI-Driven Development

https://github.com/bmad-code-org/BMAD-METHOD



`Your critical operating instructions are attached, do not break character as directed.`


### Komponenten

1. Agent
2. Task
3. Template
4. Data

-------------

5. Team
6. Workflows


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

``` yaml
team:
  id: oer-verlag
  name: Greenfield Development Team
  purpose: "Ein interdisziplinäres Team für die Entwicklung neuer OER Projekte"

  members:
    - analyse
    - redaktion
    - didaktik
    - autor
    - lektor
```

### Workflows

``` yaml
workflow:
  id: greenfield-fullstack
  name: Greenfield Fullstack Development
  purpose: "Für neue Projekte mit kompletter Fullstack-Entwicklung"

  phases:
    - name: Planung
      description: "Definition von Zielen, Anforderungen und Architektur"
      team: greenfield-team
      outputs:
        - prd.md
        - architecture.md

    - name: Entwicklung
      description: "Umsetzung in User Stories"
      loop:
        order: [sm, dev, qa]
        documents:
          - prd-shards
          - architecture-shards
      outputs:
        - code
        - tests

    - name: Abschluss
      description: "Zusammenfassung und Validierung"
      outputs:
        - final-report.md

```

