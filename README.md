# renovate-config

Shared Renovate configuration preset for consistent dependency management across repositories.

## Usage

To use this shared configuration in your repository, add the following to your `renovate.json`:

```json
{
  "extends": ["local>asakatida/renovate-config"]
}
```

Or if using `renovate.json5` or `.renovaterc.json`, you can use the same syntax.

## Features

This preset includes:

- **Best Practices**: Extends Renovate's recommended best practices
- **Dependency Dashboard**: Creates an issue with an overview of all dependencies
- **Semantic Commits**: Uses semantic commit messages (e.g., `chore(deps): update ...`)
- **Scheduled Updates**: Runs before 6am on Mondays (UTC)
- **Automerge**: Automatically merges non-major updates after passing checks
- **Grouped Updates**: Groups related dependencies (linters, test frameworks, build tools, etc.)
- **Security**: Enables vulnerability alerts with special labeling
- **Lock File Maintenance**: Monthly lock file updates
- **Rate Limiting**: Maximum 10 concurrent PRs to avoid overwhelming reviewers

## Package Rules

### Automerge Rules
- **Non-major updates** (minor, patch, digest, pin): Automatically merged
- **Major updates**: Require manual approval and review

### Grouping
Dependencies are intelligently grouped by category:
- **Linters & Formatters**: ESLint, Prettier, Ruff, Black, etc.
- **Test Frameworks**: Jest, Vitest, Pytest, RSpec, etc.
- **Build Tools**: Webpack, Vite, Rollup, esbuild, etc.
- **Type Definitions**: All `@types/*` packages
- **GitHub Actions**: CI/CD workflow dependencies

### Special Handling
- **Docker Images**: Pin digests for reproducibility
- **Security Patches**: Processed at any time, regardless of schedule
- **GitHub Actions**: Labeled as `ci` with appropriate commit prefix

## Customization

Individual repositories can override any of these settings by adding additional configuration after extending this preset:

```json
{
  "extends": ["local>asakatida/renovate-config"],
  "schedule": ["before 6am on Friday"],
  "automerge": false
}
```

## Ignored Paths

The following paths are ignored by default:
- `**/node_modules/**`
- `**/vendor/**`
- `**/__fixtures__/**`
- `**/examples/**`

## License

See [LICENSE](LICENSE) file for details.