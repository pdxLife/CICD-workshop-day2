# CI/CD Workshop - Day 2: GitHub Actions

This workshop demonstrates progressive CI/CD pipeline implementation using GitHub Actions.

## Project Structure

```
.
├── .github/
│   └── workflows/
│       ├── phase1-basic-checkout.yml
│       ├── phase2-add-go-environment.yml
│       ├── phase3-add-build.yml
│       ├── phase4-add-tests.yml
│       ├── phase5-add-static-analysis.yml
│       └── phase6-add-artifacts.yml
├── cmd/
│   └── webapp/
│       ├── main.go
│       └── main_test.go
├── go.mod
└── README.md
```

## Phases

### Phase 1: Basic Checkout
- Checkout source code
- Trigger on push and pull requests

### Phase 2: Add Go Environment
- Setup Go environment (version 1.21.5)
- Install dependencies

### Phase 3: Add Build
- Build Go application
- Create binary

### Phase 4: Add Tests
- Run unit tests with coverage
- Generate test reports

### Phase 5: Add Static Analysis
- Run golangci-lint
- Run go vet
- Check code formatting

### Phase 6: Add Artifacts
- Create deployable artifacts
- Upload artifacts to GitHub

## Running Locally

```bash
# Build
go build -o bin/app ./cmd/webapp

# Test
go test -v ./cmd/...

# Run
./bin/app
# or
PORT=8090 ./bin/app
```

## GitHub Actions

All workflows are located in `.github/workflows/` directory. Each phase builds upon the previous one, demonstrating progressive CI/CD implementation.

To use a specific phase:
1. Enable the desired workflow
2. Push changes to trigger the workflow
3. View results in GitHub Actions tab

## Environment Variables

- `PORT` - Server port (default: 8090)

## Endpoints

- `/` - Home page
- `/health` - Health check endpoint
- `/version` - Version information
