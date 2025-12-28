# shadcn-admin-kit-template
Baker template to scaffold new shadcn-admin-kit projects.

## E2E Testing

### With Real Backend

Run e2e tests against the real backend:

```bash
docker-compose -f docker-compose.e2e.yml up --build
```

### With Mock Server (WireMock)

Run e2e tests against WireMock mock server (faster, no database required):

```bash
docker-compose -f docker-compose.e2e.mock.yml up --build
```

The mock server uses WireMock with pre-configured stubs for all API endpoints. See [wiremock/README.md](wiremock/README.md) for details.

### Running Tests Manually

```bash
# Install dependencies
pnpm install

# Run Playwright tests
pnpm test:e2e

# Run with UI mode
pnpm test:e2e:ui
```
