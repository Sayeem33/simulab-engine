# SimuLab Engine ER Diagram - Mermaid Code

Use this code in **Gemini AI**, **Mermaid Live Editor**, or any tool that supports Mermaid syntax to generate a PNG.

## Copy This Code to Gemini:

```mermaid
erDiagram
    USER ||--o{ EXPERIMENT : creates
    USER ||--o{ TUTORIAL : writes
    EXPERIMENT ||--|| EXPERIMENT_STATE : has
    EXPERIMENT ||--o{ ACHIEVEMENT : "earns"
    TUTORIAL ||--o{ CHAPTER : "contains"
    CHAPTER ||--o{ EXAMPLE : "demonstrates"
    TUTORIAL ||--o{ REFERENCE : "cites"

    USER {
        string _id PK "ObjectId"
        string email UK "unique"
        string name
        string passwordHash
        string role "student|teacher|admin"
        string studentId
        string institution
        string grade
        string avatar
        timestamp createdAt
        timestamp updatedAt
    }

    EXPERIMENT {
        string _id PK "ObjectId"
        string userId FK "owner"
        string title
        string description
        string category "physics|chemistry|electronics"
        string experimentType
        mixed state "flexible payload"
        string labReport
        boolean isTemplate
        string templateCreatedBy FK
        string[] sharedWith FK "array of ObjectId"
        string[] tags
        string status "draft|completed|submitted"
        timestamp createdAt
        timestamp updatedAt
    }

    EXPERIMENT_STATE {
        string category "{physics, chemistry}"
        array objects "PhysicsObject[]"
        object chemistry "ChemistrySetup"
        array dataPoints "DataPoint[]"
        object graphConfig "chart settings"
    }

    TUTORIAL {
        string _id PK "ObjectId"
        string experimentId UK "unique reference"
        string experimentName
        string category
        string description
        string difficulty "beginner|intermediate|advanced"
        number duration "minutes"
        string[] objectives
        string[] prerequisites
        array chapters "TutorialChapter[]"
        string[] relatedTopics
        array references "Reference[]"
        timestamp createdAt
        timestamp updatedAt
    }

    CHAPTER {
        number chapterNumber
        string title
        string content
        string[] keyPoints
        string visualDescription
        string formula
        array examples "Example[]"
    }

    EXAMPLE {
        string title
        string description
        string calculation
    }

    REFERENCE {
        string title
        string url
    }

    ACHIEVEMENT {
        string _id PK "ObjectId"
        string title
        string description
        number points
        timestamp createdAt
    }
```

---

## Alternative: ASCII Art Text Representation

If you prefer a simple text-based diagram for quick reference:

```
┌─────────────────────────────────────────────────────────────────────┐
│                    SIMULAB ENGINE - ER DIAGRAM                      │
└─────────────────────────────────────────────────────────────────────┘

┌──────────────┐
│     USER     │
├──────────────┤
│ _id (PK)     │
│ email (UK)   │◄──┐
│ name         │   │
│ role         │   │ 1:N creates
│ institution  │   │
└──────────────┘   │
       │ 1:N       │
       │ writes    │
       │           │
       ▼           │
┌──────────────┐   │
│   TUTORIAL   │   │
├──────────────┤   │
│ _id (PK)     │   │
│ expId (UK)   │   │
│ difficulty   │   │
│ chapters[ ]  │   │
│ references[]◄┼───┘
└──────────────┘   │
       │           │
       │ 1:N       │
    contains       │
       │           │
       ▼           │
  ┌────────────┐   │
  │  CHAPTER   │   │
  ├────────────┤   │
  │ title      │   │
  │ keyPoints[]│   │
  │ examples[] │   │
  └────────────┘   │
                   │
                   ▼ 1
        ┌──────────────────────┐
        │    EXPERIMENT        │
        ├──────────────────────┤
        │ _id (PK)             │
        │ userId (FK)◄─────────┘
        │ title                │
        │ state (mixed)────────┐
        │ isTemplate           │
        │ sharedWith[] (FK)    │
        │ status               │
        └──────────────────────┘
                   │
                   │ 1:1 has
                   ▼
      ┌──────────────────────┐
      │  EXPERIMENT_STATE    │
      ├──────────────────────┤
      │ objects[]            │
      │ (PhysicsObject)      │
      │ chemistry            │
      │ (ChemistrySetup)     │
      │ dataPoints[]         │
      │ (DataPoint)          │
      │ graphConfig          │
      └──────────────────────┘

┌──────────────┐
│ ACHIEVEMENT  │
├──────────────┤
│ _id (PK)     │
│ title        │
│ points       │
└──────────────┘
```

---

## How to Use in Gemini:

1. **Copy the Mermaid code** (the block starting with ` ```mermaid`)
2. Open **Google Gemini** (gemini.google.com)
3. Paste this message: *"Generate a database ER diagram PNG from this Mermaid code:"* and paste the code
4. Gemini will render it as a PNG image you can download

---

## Key Relationships:
- **USER** creates 1:N **EXPERIMENT** (one user, many experiments)
- **USER** writes 1:N **TUTORIAL** (one user, many tutorials)
- **EXPERIMENT** has 1:1 **EXPERIMENT_STATE** (flexible mixed document)
- **TUTORIAL** contains 1:N **CHAPTER** (tutorials have multiple chapters)
- **CHAPTER** demonstrates 1:N **EXAMPLE** (chapters have examples)
- **TUTORIAL** cites 1:N **REFERENCE** (external sources)
- **EXPERIMENT** may earn N:M **ACHIEVEMENT** (achievements awarded on completion)
