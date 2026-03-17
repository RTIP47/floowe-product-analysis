🇬🇧 English version → [See English version](../en/03-event-storming.md)

---

# Event Storming – Floowe

Ten dokument przedstawia analizę Event Storming dla produktu Floowe, identyfikując kluczowe zdarzenia domenowe (domain events), komendy (commands), aktorów oraz systemy zewnętrzne zaangażowane w proces tworzenia i dystrybucji treści.

Analiza została początkowo wsparta przez Claude AI, a następnie dopracowana na podstawie wcześniej zidentyfikowanych przepływów użytkownika (user flows).

---

# Aktorzy

- User
- AI Content Engine (aktor systemowy)

---

# Komendy

- Register Account
- Save Brand Profile
- Link Social Channels
- Generate Article
- Edit Article
- Attach Image
- Approve Article
- Publish Article
- Distribute Content

---

# Zdarzenia domenowe

## Domena Onboarding
- Account Created
- Brand Profile Saved
- Channels Linked

## Domena Generowania Treści
- Article Generation Requested
- Draft Article Created

## Domena Edycji
- Article Edited
- Image Attached
- Article Approved

## Domena Publikacji
- Article Published
- Social Posts Generated

## Domena Dystrybucji
- Social Post Published
- Content Distributed
- SEO Loop Started

---

# Systemy zewnętrzne

- AI Content Engine
- Website CMS
- Facebook API
- LinkedIn API
- X (Twitter) API
- Search Engines

---

# Granice domen

## 1. Onboarding

Użytkownik tworzy konto, definiuje kontekst marki oraz łączy konta społecznościowe.

Kluczowa zależność: kanały społecznościowe muszą być połączone, zanim możliwe będzie publikowanie treści.

---

## 2. Generowanie treści

System AI generuje szkic artykułu zoptymalizowany pod SEO na podstawie komendy użytkownika.

Zdarzenie **Draft Article Created** uruchamia dalszy przepływ w systemie.

---

## 3. Edycja

Użytkownik dopracowuje treść artykułu oraz dodaje obrazy.

Zdarzenie **Article Approved** działa jako bramka przed publikacją.

---

## 4. Publikacja

Publikacja uruchamia dwa procesy:

- publikację artykułu w systemie CMS
- generowanie postów w mediach społecznościowych

Operacje te mogą być wykonywane asynchronicznie.

---

## 5. Dystrybucja

Treść jest dystrybuowana na wielu platformach społecznościowych poprzez integracje API.

Zdarzenia końcowe **Content Distributed** oraz **SEO Loop Started** reprezentują biznesowy efekt działania systemu — zwiększanie zasięgu organicznego w czasie.

---

# Diagram Event Storming

```mermaid
flowchart LR

  %% ── Styles ──────────────────────────────────────────
  classDef actor    fill:#EEEDFE,stroke:#AFA9EC,color:#3C3489,font-weight:600
  classDef command  fill:#E6F1FB,stroke:#85B7EB,color:#0C447C,font-weight:600
  classDef event    fill:#FAEEDA,stroke:#EF9F27,color:#633806,font-weight:600
  classDef external fill:#E1F5EE,stroke:#5DCAA5,color:#085041,font-weight:600
  classDef domain   fill:#F1EFE8,stroke:#B4B2A9,color:#5F5E5A,font-weight:700

  %% DOMAIN 1 — ONBOARDING
  subgraph D1["① Onboarding"]
    direction TB
    U1(["User"]):::actor

    C1["Register Account"]:::command
    C2["Save Brand Profile"]:::command
    C3["Link Social Channels"]:::command

    E1(["Account Created"]):::event
    E2(["Brand Profile Saved"]):::event
    E3(["Channels Linked"]):::event

    U1 --> C1 --> E1 --> C2 --> E2 --> C3 --> E3
  end

  %% DOMAIN 2 — CONTENT GENERATION
  subgraph D2["② Content Generation"]
    direction TB
    U2(["User"]):::actor
    SYS1[["AI Content Engine"]]:::external

    C4["Generate Article"]:::command

    E4(["Article Generation Requested"]):::event
    E5(["Draft Article Created"]):::event

    U2 --> C4 --> E4 --> SYS1 --> E5
  end

  %% DOMAIN 3 — EDITING
  subgraph D3["③ Editing"]
    direction TB
    U3(["User"]):::actor

    C5["Edit Article"]:::command
    C6["Attach Image"]:::command
    C7["Approve Article"]:::command

    E6(["Article Edited"]):::event
    E7(["Image Attached"]):::event
    E8(["Article Approved"]):::event

    U3 --> C5 --> E6 --> C6 --> E7 --> C7 --> E8
  end

  %% DOMAIN 4 — PUBLISHING
  subgraph D4["④ Publishing"]
    direction TB
    U4(["User"]):::actor
    SYS2[["Website CMS"]]:::external

    C8["Publish Article"]:::command

    E9(["Article Published"]):::event
    E10(["Social Posts Generated"]):::event

    U4 --> C8 --> E9 --> SYS2
    E9 --> E10
  end

  %% DOMAIN 5 — DISTRIBUTION
  subgraph D5["⑤ Distribution"]
    direction TB
    SYS3[["Facebook API"]]:::external
    SYS4[["LinkedIn API"]]:::external
    SYS5[["X API"]]:::external
    SYS6[["Search Engines"]]:::external

    C9["Distribute Content"]:::command

    E11(["Social Post Published"]):::event
    E12(["Content Distributed"]):::event
    E13(["SEO Loop Started"]):::event

    C9 --> SYS3 --> E11
    C9 --> SYS4 --> E11
    C9 --> SYS5 --> E11
    E11 --> E12 --> SYS6 --> E13
  end

  %% DOMAIN TRANSITIONS
  E3 -->|triggers| C4
  E5 -->|triggers| C5
  E8 -->|triggers| C8
  E9 -->|triggers| C9
