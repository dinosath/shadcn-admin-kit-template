# WireMock for E2E Testing

This directory contains WireMock stub mappings for e2e/integration testing.

## Structure

```
wiremock/
├── mappings.json       # WireMock stub mappings for all entities
├── __files/           # Static response body files (optional)
└── README.md          # This file
```

## Usage

### Running with Docker Compose

Use the mock-based docker-compose configuration for testing without the real backend:

```bash
docker-compose -f docker-compose.e2e.mock.yml up
```

### Running WireMock Standalone

```bash
docker run -d --name wiremock \
  -p 8080:8080 \
  -v $(pwd)/wiremock/mappings.json:/home/wiremock/mappings/mappings.json \
  -v $(pwd)/wiremock/__files:/home/wiremock/__files \
  wiremock/wiremock:3.13.0
```

### Testing the Stubs

After starting WireMock, test the stubs:

```bash
# List all entities
curl http://localhost:8080/api/profiles

# Get single entity
curl http://localhost:8080/api/profiles/1

# Create entity
curl -X POST http://localhost:8080/api/profiles \
  -H "Content-Type: application/json" \
  -d '{"name": "Test"}'
```

## Customization

### Adding Custom Stubs

Edit `mappings.json` to add or modify stub mappings. Each mapping has:
- `name`: Descriptive name for the stub
- `request`: Request matching criteria
- `response`: Mock response to return

### Request Matching

WireMock supports various request matchers:
- `urlPath`: Exact URL path
- `urlPathPattern`: Regex URL path pattern
- `url`: Full URL with query string
- `method`: HTTP method

### Response Templating

Enable response templating for dynamic responses:

```json
{
  "response": {
    "transformers": ["response-template"],
    "body": "{ \"id\": \"{{request.pathSegments.[2]}}\" }"
  }
}
```

## Resources

- [WireMock Documentation](https://wiremock.org/docs/)
- [Request Matching](https://wiremock.org/docs/request-matching/)
- [Response Templating](https://wiremock.org/docs/response-templating/)
