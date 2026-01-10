# Ninolex Pronunciation Resolution Pipeline

## Overview

Ninolex provides a pronunciation resolution pipeline that transforms arbitrary text entities into IPA (International Phonetic Alphabet) phonemes, then exports to TTS-engine-specific dictionary formats.

## Pipeline Architecture

```mermaid
flowchart TB
    subgraph Input["Input Layer"]
        UI[Web UI]
        API[REST API]
        BATCH[Batch Upload]
    end

    subgraph Preprocessing["Preprocessing"]
        NORM[Normalizer]
        EXP[Alphanumeric<br/>Expander]
        TOK[Tokenizer]
    end

    subgraph Resolution["Resolution Engine"]
        CACHE[Cache<br/>Lookup]
        CMU[CMUdict]
        PHON[Phonemizer]
        OVR[Override<br/>Registry]
    end

    subgraph Storage["Storage Layer"]
        DB[(Supabase)]
        IDX[Search Index]
    end

    subgraph Export["Export Layer"]
        EL[ElevenLabs<br/>Dictionary]
        AWS[AWS Polly<br/>Lexicon]
        VAPI[Vapi<br/>Dictionary]
    end

    UI --> NORM
    API --> NORM
    BATCH --> NORM

    NORM --> EXP
    EXP --> TOK
    TOK --> CACHE

    CACHE -->|miss| CMU
    CACHE -->|miss| PHON
    CACHE -->|hit| DB

    CMU --> OVR
    PHON --> OVR
    OVR --> DB

    DB --> EL
    DB --> AWS
    DB --> VAPI
    DB --> IDX
```

## Pipeline Stages

### Stage 1: Input

Multiple input methods converge to the same pipeline:

```mermaid
flowchart LR
    subgraph Sources
        A[Web UI<br/>Single entity]
        B[API<br/>Programmatic]
        C[Batch<br/>CSV upload]
    end

    subgraph Unified
        D[Input<br/>Queue]
    end

    A --> D
    B --> D
    C --> D
```

### Stage 2: Preprocessing

```mermaid
flowchart LR
    subgraph Raw
        IN[Raw Input<br/>"BMW  X5"]
    end

    subgraph Normalize
        N1[Trim whitespace]
        N2[Normalize unicode]
        N3[Case handling]
    end

    subgraph Expand
        E1[Detect alphanumeric]
        E2[Expand patterns]
        E3["WH-1000XM5" →<br/>"W H one thousand X M five"]
    end

    subgraph Tokenize
        T1[Split into units]
        T2[Identify boundaries]
    end

    IN --> N1 --> N2 --> N3
    N3 --> E1 --> E2 --> E3
    E3 --> T1 --> T2
```

**Alphanumeric expansion examples:**

| Input | Expanded |
|-------|----------|
| BMW X5 | B M W X five |
| WH-1000XM5 | W H one thousand X M five |
| iPhone 15 | iPhone fifteen |
| A4 | A four |

### Stage 3: Resolution

Two-tier resolution with fallback:

```mermaid
flowchart TB
    subgraph Input
        ENT[Entity Token]
    end

    subgraph Tier1["Tier 1: CMUdict"]
        CMU[CMUdict<br/>Lookup]
        HIT1{Found?}
    end

    subgraph Tier2["Tier 2: Phonemizer"]
        PHON[Phonemizer<br/>ML Model]
    end

    subgraph Override
        OVR[Override<br/>Check]
        CUSTOM{Custom<br/>exists?}
    end

    subgraph Output
        IPA[IPA Phoneme]
    end

    ENT --> CMU
    CMU --> HIT1
    HIT1 -->|yes| OVR
    HIT1 -->|no| PHON
    PHON --> OVR
    OVR --> CUSTOM
    CUSTOM -->|yes| IPA
    CUSTOM -->|no| IPA
```

**Resolution sources:**

| Source | Speed | Accuracy | Coverage |
|--------|-------|----------|----------|
| CMUdict | Fast (<10ms) | High | Standard English |
| Phonemizer | Slower (~100ms) | Good | Novel entities |
| Override | Instant | Perfect | Manual entries |

### Stage 4: Export

Engine-specific dictionary generation:

```mermaid
flowchart LR
    subgraph Source
        DB[(Resolved<br/>Phonemes)]
    end

    subgraph Transform
        T1[Format<br/>Converter]
    end

    subgraph Formats
        EL[ElevenLabs<br/>.pls]
        AWS[AWS Polly<br/>.pls]
        VAPI[Vapi<br/>.json]
    end

    DB --> T1
    T1 --> EL
    T1 --> AWS
    T1 --> VAPI
```

**Export format examples:**

ElevenLabs/Polly (W3C PLS):
```xml
<lexicon>
  <lexeme>
    <grapheme>BMW</grapheme>
    <phoneme>biː ɛm ˈdʌbəljuː</phoneme>
  </lexeme>
</lexicon>
```

Vapi (JSON):
```json
{
  "words": [
    {
      "word": "BMW",
      "pronunciation": "biː ɛm ˈdʌbəljuː"
    }
  ]
}
```

## Vertical Pack Architecture

```mermaid
flowchart TB
    subgraph Core["Ninolex Core"]
        PIPE[Resolution<br/>Pipeline]
    end

    subgraph Verticals["Vertical Packs"]
        AUTO[AutoLex<br/>Automotive]
        DINE[DineLex<br/>Restaurant]
        ID[IdentityLex<br/>Names]
    end

    subgraph Data["Curated Data"]
        A_DATA[Makes, Models,<br/>Trims]
        D_DATA[Cuisines, Dishes,<br/>Restaurants]
        I_DATA[Cultural Names]
    end

    PIPE --> AUTO
    PIPE --> DINE
    PIPE --> ID

    AUTO --> A_DATA
    DINE --> D_DATA
    ID --> I_DATA
```

**Vertical isolation:** Each pack operates independently, enabling parallel development.

## API Contract

```yaml
# POST /api/v1/resolve
Request:
  entities:
    - "BMW X5"
    - "Mercedes-Benz"
    - "WH-1000XM5"
  format: "elevenlabs"

Response:
  results:
    - grapheme: "BMW X5"
      phoneme: "biː ɛm ˈdʌbəljuː ɛks faɪv"
      source: "cmudict"
      confidence: 0.95
    - grapheme: "Mercedes-Benz"
      phoneme: "mərˈseɪdiz bɛnz"
      source: "cmudict"
      confidence: 0.92
    - grapheme: "WH-1000XM5"
      phoneme: "ˈdʌbəljuː eɪtʃ wʌn ˈθaʊzənd ɛks ɛm faɪv"
      source: "expansion+cmudict"
      confidence: 0.88
  export:
    format: "elevenlabs"
    download_url: "/exports/req_xxx.pls"
```

## Related Documents

- [Ninolex Case Study](../case-studies/ninolex.md)
- [ADR-003: API-First Surface](../adrs/003-api-first-surface.md)
- [Ninolex-GH Repository](https://github.com/iamnortey/ninolex-gh)
