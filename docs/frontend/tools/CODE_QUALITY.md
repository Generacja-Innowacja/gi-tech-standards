# Code Quality

## Linting

**Biome**

Biome is a fast, all-in-one toolchain for JavaScript, TypeScript, and JSON. It combines a linter and formatter in a single tool, providing:

- **Speed**: Written in Rust, Biome is significantly faster than ESLint
- **Simplicity**: One tool instead of multiple (ESLint + Prettier + more)
- **Zero configuration**: Works out of the box with sensible defaults
- **Unicorn ruleset**: Additional rules for catching common bugs and enforcing best practices

We use Biome's base ruleset along with the unicorn overrides to ensure code quality and
consistency across all projects.

- [Biome documentation](https://biomejs.dev/)
- [Biome GitHub repository](https://github.com/biomejs/biome)
- [Biome rules reference](https://biomejs.dev/linter/rules/)
- [Unicorn ruleset](https://github.com/sindresorhus/eslint-plugin-unicorn)

## Automation

We implement automated quality checks through CI/CD pipelines:

- **Automated linting**: Code is automatically linted on every commit
- **Job checks**: Automated checks run in CI/CD for build, lint, test, and e2e to ensure code quality and detect issues early

This ensures that code quality issues and security vulnerabilities are caught early in the development process, not after deployment.
