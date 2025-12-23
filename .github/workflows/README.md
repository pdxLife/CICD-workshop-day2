# CI/CD Workshop Phases - GitHub Actions

This directory contains GitHub Actions workflows that demonstrate progressive CI/CD pipeline implementation.

## Workflow Phases

### Phase 1: Basic Checkout
**File:** `phase1-basic-checkout.yml`
- Checkout source code from repository
- Display basic repository information
- Trigger on push and pull requests

### Phase 2: Add Go Environment
**File:** `phase2-add-go-environment.yml`
- Setup Go 1.21.5 environment
- Download and verify dependencies
- Cache Go modules for faster builds

### Phase 3: Add Build
**File:** `phase3-add-build.yml`
- Build Go application with version metadata
- Inject commit SHA and build time into binary
- Verify binary is created successfully

### Phase 4: Add Tests
**File:** `phase4-add-tests.yml`
- Run unit tests with coverage
- Generate coverage reports (text and HTML)
- Upload coverage artifacts
- Optional: Upload to Codecov

### Phase 5: Add Static Analysis
**File:** `phase5-add-static-analysis.yml`
- Run golangci-lint for code quality checks
- Run go vet for potential issues
- Check code formatting with gofmt
- Run tests with coverage

### Phase 6: Add Artifacts
**File:** `phase6-add-artifacts.yml`
- Full CI/CD pipeline with all quality checks
- Create deployable artifacts (tarball)
- Generate build metadata (JSON)
- Upload artifacts with build number
- Multiple artifact retention periods

## Triggers

All workflows can be triggered by:
- **Push** to main or phase-specific branches
- **Pull requests** to main branch
- **Manual trigger** via workflow_dispatch

## Artifacts

Artifacts are automatically uploaded and available for download:
- **Build artifacts**: Binary, scripts, metadata (90 days retention)
- **Coverage reports**: HTML and raw coverage data (30 days retention)

## Usage

### View Workflows
1. Go to your GitHub repository
2. Click on "Actions" tab
3. Select a workflow from the left sidebar

### Trigger Manually
1. Go to Actions → Select workflow
2. Click "Run workflow" button
3. Choose branch and click "Run workflow"

### Download Artifacts
1. Open a completed workflow run
2. Scroll to "Artifacts" section at the bottom
3. Click artifact name to download

## Environment Variables

Workflows use these environment variables:
- `PROJECT_NAME`: GoWebApp (defined in env section)
- `github.run_number`: Unique build number
- `github.sha`: Commit SHA
- `github.actor`: User who triggered the workflow

## Caching

Go module caching is enabled in all workflows using `actions/setup-go@v5` with `cache: true`. This significantly speeds up builds by caching:
- Go modules (`go.mod`)
- Build cache

## Best Practices Demonstrated

1. **Progressive Enhancement**: Each phase builds upon the previous
2. **Artifact Management**: Proper retention policies
3. **Build Metadata**: Complete traceability
4. **Code Quality**: Multiple quality gates
5. **Caching**: Faster builds with dependency caching
6. **Flexibility**: Manual and automatic triggers
7. **Visibility**: Clear job names and step descriptions

## Comparison with Jenkins

| Feature | Jenkins | GitHub Actions |
|---------|---------|----------------|
| Environment | Self-hosted / Cloud | GitHub-hosted |
| Configuration | Groovy (Jenkinsfile) | YAML |
| Artifacts | Jenkins archive | GitHub artifacts |
| Caching | Manual setup | Built-in |
| Triggers | Webhook / Poll | Events-based |
| Matrix builds | Pipeline stages | Matrix strategy |
| Secrets | Credentials plugin | GitHub Secrets |

## Next Steps

After completing all phases, consider:
- Adding matrix builds for multiple Go versions
- Implementing deployment stages
- Adding security scanning (SAST/DAST)
- Creating reusable workflows
- Setting up branch protection rules
- Configuring required status checks
