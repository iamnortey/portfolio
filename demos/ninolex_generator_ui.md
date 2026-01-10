# Ninolex Dictionary Generator UI Demo

## Web Interface (Next.js)

This demo shows the dictionary generation workflow in the Ninolex web application.

### Screen 1: Entity Input

```
┌─────────────────────────────────────────────────────────────┐
│  Ninolex                                   [Docs] [API]     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Dictionary Generator                                       │
│  Create pronunciation dictionaries for TTS engines          │
│                                                             │
│  ─────────────────────────────────────────────────────────  │
│                                                             │
│  Enter entities (one per line):                             │
│  ┌─────────────────────────────────────────────────────────┐│
│  │ BMW X5                                                  ││
│  │ Mercedes-Benz E-Class                                   ││
│  │ WH-1000XM5                                              ││
│  │ Kwame Asante                                            ││
│  │ Jollof Rice                                             ││
│  │                                                         ││
│  │                                                         ││
│  │                                                         ││
│  └─────────────────────────────────────────────────────────┘│
│                                                             │
│  Export format:                                             │
│  ┌─────────────────────────┐                                │
│  │ ElevenLabs (.pls)     ▼│                                │
│  └─────────────────────────┘                                │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐│
│  │              Generate Dictionary                        ││
│  └─────────────────────────────────────────────────────────┘│
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Screen 2: Processing

```
┌─────────────────────────────────────────────────────────────┐
│  Ninolex                                   [Docs] [API]     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Processing...                                              │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐│
│  │                                                         ││
│  │  ████████████████░░░░░░░░░░░░░░░░░░░░  60%              ││
│  │                                                         ││
│  │  Resolving: Mercedes-Benz E-Class                       ││
│  │                                                         ││
│  │  ✓ BMW X5              → biː ɛm ˈdʌbəljuː ɛks faɪv     ││
│  │  ⟳ Mercedes-Benz E-Class                                ││
│  │  ○ WH-1000XM5                                           ││
│  │  ○ Kwame Asante                                         ││
│  │  ○ Jollof Rice                                          ││
│  │                                                         ││
│  └─────────────────────────────────────────────────────────┘│
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Screen 3: Results

```
┌─────────────────────────────────────────────────────────────┐
│  Ninolex                                   [Docs] [API]     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ✓ Dictionary Generated                                     │
│                                                             │
│  5 entities resolved | Format: ElevenLabs                   │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐│
│  │ Entity              Phoneme                   Source    ││
│  │ ─────────────────────────────────────────────────────── ││
│  │ BMW X5              biː ɛm ˈdʌbəljuː ɛks faɪv CMUdict  ││
│  │ Mercedes-Benz       mərˈseɪdiz bɛnz iː klæs   CMUdict  ││
│  │ E-Class                                                 ││
│  │ WH-1000XM5          ˈdʌbəljuː eɪtʃ wʌn        Expansion││
│  │                     ˈθaʊzənd ɛks ɛm faɪv      +CMUdict ││
│  │ Kwame Asante        ˈkwɑːmeɪ əˈsænteɪ         Phonemizer│
│  │ Jollof Rice         ˈdʒɒlɒf raɪs              Phonemizer│
│  └─────────────────────────────────────────────────────────┘│
│                                                             │
│  ┌────────────────────┐  ┌────────────────────┐             │
│  │  Download .pls     │  │  Copy to Clipboard │             │
│  └────────────────────┘  └────────────────────┘             │
│                                                             │
│  ─────────────────────────────────────────────────────────  │
│                                                             │
│  Preview (ElevenLabs PLS format):                           │
│  ┌─────────────────────────────────────────────────────────┐│
│  │ <?xml version="1.0" encoding="UTF-8"?>                  ││
│  │ <lexicon version="1.0"                                  ││
│  │          xmlns="http://www.w3.org/2005/01/              ││
│  │          pronunciation-lexicon">                        ││
│  │   <lexeme>                                              ││
│  │     <grapheme>BMW X5</grapheme>                         ││
│  │     <phoneme>biː ɛm ˈdʌbəljuː ɛks faɪv</phoneme>       ││
│  │   </lexeme>                                             ││
│  │   ...                                                   ││
│  │ </lexicon>                                              ││
│  └─────────────────────────────────────────────────────────┘│
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Key UI Features

| Feature | Description |
|---------|-------------|
| Multi-line input | Batch entity entry |
| Format selector | ElevenLabs, AWS Polly, Vapi |
| Progress indicator | Real-time resolution status |
| Source attribution | Shows CMUdict vs Phonemizer |
| Preview pane | View output before download |

## Resolution Sources Explained

| Source | Icon | Meaning |
|--------|------|---------|
| CMUdict | ✓ | High-confidence dictionary lookup |
| Phonemizer | ~ | ML-based pronunciation |
| Expansion | + | Alphanumeric expansion applied |
| Override | ★ | Manual correction applied |

---

*All data shown is synthetic. See [Redaction Policy](../docs/REDACTION_POLICY.md).*
