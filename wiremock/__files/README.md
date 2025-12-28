# WireMock Response Files

This directory contains static response body files that can be referenced from WireMock mappings.

For complex responses or large payloads, create JSON files here and reference them in mappings using:

```json
{
  "response": {
    "bodyFileName": "example-response.json"
  }
}
```
