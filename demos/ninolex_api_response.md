# Ninolex API Response Demo

## REST API: `/api/v1/resolve`

This demo shows the API request and response format for the Ninolex pronunciation resolution endpoint.

### Request

```http
POST /api/v1/resolve HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer YOUR_API_KEY_HERE

{
  "entities": [
    "BMW X5",
    "Mercedes-Benz E-Class",
    "WH-1000XM5",
    "Kwame Asante",
    "Jollof Rice"
  ],
  "format": "elevenlabs",
  "options": {
    "include_confidence": true,
    "include_source": true
  }
}
```

### Response

```json
{
  "request_id": "req_demo_001",
  "status": "success",
  "processed_at": "2026-01-10T10:30:00Z",
  "results": [
    {
      "grapheme": "BMW X5",
      "phoneme": "biː ɛm ˈdʌbəljuː ɛks faɪv",
      "source": "cmudict",
      "confidence": 0.95,
      "expansion_applied": false
    },
    {
      "grapheme": "Mercedes-Benz E-Class",
      "phoneme": "mərˈseɪdiz bɛnz iː klæs",
      "source": "cmudict",
      "confidence": 0.92,
      "expansion_applied": false
    },
    {
      "grapheme": "WH-1000XM5",
      "phoneme": "ˈdʌbəljuː eɪtʃ wʌn ˈθaʊzənd ɛks ɛm faɪv",
      "source": "cmudict",
      "confidence": 0.88,
      "expansion_applied": true,
      "expansion_detail": {
        "original": "WH-1000XM5",
        "expanded": "W H one thousand X M five"
      }
    },
    {
      "grapheme": "Kwame Asante",
      "phoneme": "ˈkwɑːmeɪ əˈsænteɪ",
      "source": "phonemizer",
      "confidence": 0.78,
      "expansion_applied": false
    },
    {
      "grapheme": "Jollof Rice",
      "phoneme": "ˈdʒɒlɒf raɪs",
      "source": "phonemizer",
      "confidence": 0.82,
      "expansion_applied": false
    }
  ],
  "export": {
    "format": "elevenlabs",
    "content_type": "application/pls+xml",
    "download_url": "/api/v1/exports/req_demo_001.pls",
    "expires_at": "2026-01-10T11:30:00Z"
  },
  "usage": {
    "entities_processed": 5,
    "cache_hits": 2,
    "cache_misses": 3
  }
}
```

### Export File Content

When you download the export file, you get:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<lexicon version="1.0"
         xmlns="http://www.w3.org/2005/01/pronunciation-lexicon"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.w3.org/2005/01/pronunciation-lexicon
                             http://www.w3.org/TR/pronunciation-lexicon/pls.xsd"
         alphabet="ipa"
         xml:lang="en-US">

  <lexeme>
    <grapheme>BMW X5</grapheme>
    <phoneme>biː ɛm ˈdʌbəljuː ɛks faɪv</phoneme>
  </lexeme>

  <lexeme>
    <grapheme>Mercedes-Benz E-Class</grapheme>
    <phoneme>mərˈseɪdiz bɛnz iː klæs</phoneme>
  </lexeme>

  <lexeme>
    <grapheme>WH-1000XM5</grapheme>
    <phoneme>ˈdʌbəljuː eɪtʃ wʌn ˈθaʊzənd ɛks ɛm faɪv</phoneme>
  </lexeme>

  <lexeme>
    <grapheme>Kwame Asante</grapheme>
    <phoneme>ˈkwɑːmeɪ əˈsænteɪ</phoneme>
  </lexeme>

  <lexeme>
    <grapheme>Jollof Rice</grapheme>
    <phoneme>ˈdʒɒlɒf raɪs</phoneme>
  </lexeme>

</lexicon>
```

## Error Response Example

```json
{
  "request_id": "req_demo_002",
  "status": "error",
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "API rate limit exceeded. Please retry after 60 seconds.",
    "retry_after": 60
  }
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `request_id` | string | Unique identifier for this request |
| `status` | string | `success` or `error` |
| `results` | array | Resolved pronunciations |
| `results[].grapheme` | string | Original text input |
| `results[].phoneme` | string | IPA pronunciation |
| `results[].source` | string | Resolution source (cmudict, phonemizer, override) |
| `results[].confidence` | number | Confidence score (0.0 - 1.0) |
| `export` | object | Download information for dictionary file |
| `usage` | object | Request statistics |

## Rate Limits

| Tier | Requests/min | Entities/request |
|------|-------------|------------------|
| Free | 10 | 50 |
| Basic | 60 | 200 |
| Pro | 300 | 1000 |

---

*All data shown is synthetic. API endpoint is illustrative. See [Redaction Policy](../docs/REDACTION_POLICY.md).*
