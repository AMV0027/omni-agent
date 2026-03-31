# Contributing to OmniAgent

Thank you for your interest in contributing to OmniAgent! We welcome contributions from the community and are excited to collaborate with you. This document provides guidelines and instructions for contributing.

## Code of Conduct

Please review our [Code of Conduct](CODE_OF_CONDUCT.md) before contributing. We expect all contributors to adhere to these standards.

## How to Contribute

### Reporting Bugs

Before reporting a bug, please check the [existing issues](https://github.com/AMV0027/omni-agent/issues) to avoid duplicates.

When reporting a bug, include:

- **Title**: Clear, concise description of the bug
- **Description**: Detailed explanation of what went wrong
- **Steps to Reproduce**: Clear steps to reproduce the issue
- **Expected Behavior**: What you expected to happen
- **Actual Behavior**: What actually happened
- **Environment**: OS, Node.js version, Ollama version, etc.
- **Screenshots/Logs**: If applicable, attach relevant output or error messages

### Suggesting Enhancements

We welcome feature suggestions! Please provide:

- **Title**: Clear description of the enhancement
- **Current Behavior**: How things work currently
- **Desired Behavior**: What you'd like to see
- **Use Case**: Why this enhancement would be useful
- **Additional Context**: Any other relevant information

### Pull Requests

1. **Fork the Repository**: Create your own fork of the project
2. **Create a Feature Branch**: Use a descriptive branch name
   ```bash
   git checkout -b feature/your-feature-name
   # or for bugfixes
   git checkout -b fix/issue-description
   ```
3. **Make Your Changes**: Implement your feature or fix
4. **Follow Code Standards**:
   - Use TypeScript for type safety
   - Follow existing code style and conventions
   - Write clear, descriptive commit messages
   - Add tests for new functionality when possible
5. **Test Your Changes**:
   ```bash
   npm run build
   npm run dev
   ```
6. **Keep Your Branch Updated**: Rebase against main if needed
7. **Submit a Pull Request**:
   - Reference related issues (closes #123)
   - Provide clear description of changes
   - Explain reasoning behind implementation choices
   - Include any breaking changes prominently

## Development Setup

```bash
# Clone the repository
git clone https://github.com/AMV0027/omni-agent.git
cd omni-agent

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Set up database
npm run db:setup

# Start development server
npm run dev

# In separate terminals, start frontends (optional)
npm run dev:ai-frontend
npm run dev:ecom-frontend

# Or run all together
npm run dev:all
```

## Architecture Overview

OmniAgent uses a multi-agent architecture powered by LangGraph:

- **src/agents/**: Agent definitions and graph orchestration
- **src/routes/**: API endpoints for various features
- **src/services/**: Business logic and agent operations
- **src/config/**: Configuration for LLM and database
- **prisma/**: Database schema and migrations
- **ai-frontend/**: React UI for chat interface
- **ecom-frontend/**: React UI for e-commerce store

See [documentation/](documentation/) for detailed technical design.

## Coding Guidelines

### TypeScript Standards

- Use strict typing; avoid `any` when possible
- Use interfaces for object shapes
- Provide clear JSDoc comments for complex functions
- Export types that are part of the public API

### Commit Messages

Follow conventional commits format:

```
feat: add new feature description
fix: fix bug description
docs: update documentation
refactor: refactor code section
test: add or update tests
chore: dependency updates, tooling changes
```

Example:

```
feat(agents): add proactive alert mechanism for inventory changes

- Implement alert service with configurable thresholds
- Add priority levels for different alert types
- Handle deduplication of similar alerts
```

### Testing

While comprehensive tests are still being developed, please:

- Test your changes manually before submitting PR
- Describe your testing approach in the PR
- Highlight any areas needing additional testing

## Documentation

- Update relevant documentation for new features
- Keep README.md current
- Comment complex code sections
- Add type definitions for new functions
- Update API documentation in code comments

## Release Process

Maintainers will handle versioning and releases following [Semantic Versioning](https://semver.org/):

- Bug fixes: patch version (1.0.x)
- New features: minor version (1.x.0)
- Breaking changes: major version (x.0.0)

## Questions?

Feel free to open a discussion issue or reach out to the maintainers. We're here to help!

---

**Thank you for contributing to OmniAgent! 🎉**
