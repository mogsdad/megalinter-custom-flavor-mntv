# MegaLinter Custom Flavor: mntv

This custom MegaLinter aims to have an optimized Docker image size.

It is built from official MegaLinter images, but is maintained on https://github.com/mogsdad/megalinter-custom-flavor-mntv by David Bingham

## Embedded linters

  - [ACTION_ACTIONLINT](https://megalinter.io/latest/descriptors/action_actionlint/)
  - [BASH_EXEC](https://megalinter.io/latest/descriptors/bash_exec/)
  - [BASH_SHELLCHECK](https://megalinter.io/latest/descriptors/bash_shellcheck/)
  - [BASH_SHFMT](https://megalinter.io/latest/descriptors/bash_shfmt/)
  - [GRAPHQL_GRAPHQL_SCHEMA_LINTER](https://megalinter.io/latest/descriptors/graphql_graphql_schema_linter/)
  - [JSON_JSONLINT](https://megalinter.io/latest/descriptors/json_jsonlint/)
  - [JSON_PRETTIER](https://megalinter.io/latest/descriptors/json_prettier/)
  - [JSON_V8R](https://megalinter.io/latest/descriptors/json_v8r/)
  - [KUBERNETES_HELM](https://megalinter.io/latest/descriptors/kubernetes_helm/)
  - [MARKDOWN_MARKDOWNLINT](https://megalinter.io/latest/descriptors/markdown_markdownlint/)
  - [MARKDOWN_MARKDOWN_LINK_CHECK](https://megalinter.io/latest/descriptors/markdown_markdown_link_check/)
  - [PYTHON_PYLINT](https://megalinter.io/latest/descriptors/python_pylint/)
  - [PYTHON_RUFF](https://megalinter.io/latest/descriptors/python_ruff/)
  - [PYTHON_RUFF_FORMAT](https://megalinter.io/latest/descriptors/python_ruff_format/)
  - [REPOSITORY_CHECKOV](https://megalinter.io/latest/descriptors/repository_checkov/)
  - [REPOSITORY_GITLEAKS](https://megalinter.io/latest/descriptors/repository_gitleaks/)
  - [YAML_YAMLLINT](https://megalinter.io/latest/descriptors/yaml_yamllint/)

## How to use the custom flavor

Follow [MegaLinter installation guide](https://megalinter.io/latest/install-assisted/), and replace related elements in the workflow.

- GitHub Action: On MegaLinter step in .github/workflows/mega-linter.yml, define `uses: mogsdad/megalinter-custom-flavor-mntv@main`
- Docker image: Replace official MegaLinter image with `ghcr.io/mogsdad/megalinter-custom-flavor-mntv/megalinter-custom-flavor:latest`

## How the flavor is generated and updated

This custom flavor is automatically kept up to date with MegaLinter releases:

1. **Automatic version sync**: The `check-new-megalinter-version` workflow runs daily, checks for new MegaLinter releases, and automatically creates matching releases in this repository.

2. **Automated builds**: Each release triggers the `megalinter-custom-flavor-builder` workflow, which:
   - Builds a Docker image with only the selected linters
   - Publishes to GitHub Container Registry (ghcr.io)
   - Optionally publishes to Docker Hub (if credentials are configured)

3. **Available image tags**:
   - Release tags (e.g., `v9.0.0`): Built from MegaLinter releases
   - `beta` tag: Built from non-main branch pushes for testing
   - `latest` tag: Points to the most recent release

## Configuration requirements

### Required: Personal Access Token

For automatic version checking to work, a `PAT_TOKEN` secret must be configured as a **repository-scoped fine-grained token** with:
- **Repository access**: Only select repositories (select this repository)
- **Repository permissions**:
  - Contents: Read and write
  - Actions: Read and write

See the [Custom Flavors documentation](https://megalinter.io/beta/custom-flavors/) for detailed setup instructions.

### Optional: Docker Hub publishing

To publish to Docker Hub in addition to ghcr.io, configure:
- `DOCKERHUB_REPO` variable (e.g., your Docker Hub username)
- `DOCKERHUB_USERNAME` secret
- `DOCKERHUB_PASSWORD` secret

## How to generate the flavor manually

If you need to manually trigger a build:

1. **Create a GitHub release**: Creates a versioned build matching the tag name (e.g., `v9.0.0`)
2. **Push to any branch** (except main): Builds a `beta` tagged image for testing
3. **Manually run the workflow**: Go to Actions > Build & Push MegaLinter Custom Flavor > Run workflow

See [full Custom Flavors documentation](https://megalinter.io/beta/custom-flavors/).

## How to use the custom flavor

Follow [MegaLinter installation guide](https://megalinter.io/latest/install-assisted/), and replace related elements in the workflow.

- **GitHub Action**: On MegaLinter step in `.github/workflows/mega-linter.yml`, define `uses: mogsdad/megalinter-custom-flavor-mntv@main`
- **Docker image**: Replace official MegaLinter image with `ghcr.io/mogsdad/megalinter-custom-flavor-mntv/megalinter-custom-flavor:latest`

[![MegaLinter is graciously provided by OX Security](https://raw.githubusercontent.com/oxsecurity/megalinter/main/docs/assets/images/ox-banner.png)](https://www.ox.security/?ref=megalinter)
