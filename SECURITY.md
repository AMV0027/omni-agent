# Security Policy

## Reporting Security Vulnerabilities

If you discover a security vulnerability in OmniAgent, please **do not** file a public issue. Instead, email the maintainers with:

- Description of the vulnerability
- Steps to reproduce (if applicable)
- Potential impact
- Suggested fix (if you have one)

We will acknowledge your report within 48 hours and keep you informed of the progress.

## Security Best Practices

When using OmniAgent, please follow these security guidelines:

### Environment Variables

- **Never commit .env files** to version control
- Use `.env.example` as a template for configuration
- Keep sensitive API keys (Ollama, Tavily, Telegram, etc.) confidential
- Rotate API keys regularly
- Use different keys for development and production

### Database Security

- Use strong database credentials
- Enable encryption for sensitive data at rest
- Implement proper backup procedures
- Limit database access to authorized services only
- Monitor database access logs

### AI Provider Integration

- **Ollama (Recommended)**: Runs locally—data never leaves your server
- **OpenRouter**: If using external APIs, ensure compliance with your data protection policies
- Review API provider security policies: https://openrouter.ai/docs/security

### API Key Management

The project requires several API keys for optional features:

- **Tavily API**: For product research and web search
- **Telegram Bot Token**: For notification delivery
- **Gmail Credentials**: For customer email communication
- **Pexels API**: For product images

**Never**:

- Commit API keys to version control
- Share API keys in issues or discussions
- Log API keys in error messages or console output

### Deployment Security

- Run OmniAgent in a controlled environment
- Validate and sanitize all user inputs
- Use HTTPS in production
- Implement rate limiting on API endpoints
- Keep dependencies updated

## Dependency Updates

We regularly update dependencies to patch security vulnerabilities. Check for updates with:

```bash
npm audit
npm audit fix
```

## Third-Party Dependencies

OmniAgent relies on several key libraries:

- **@langchain/core**: LLM integration framework
- **@langchain/langgraph**: Agent graph orchestration
- **@prisma/client**: Database ORM
- **Express**: Web framework
- **Socket.io**: Real-time communication

All dependencies are verified and kept up-to-date. Report any concerns about dependencies in security advisories.

## Data Privacy

- All local processing through Ollama keeps data within your infrastructure
- PII should be treated with appropriate access controls
- Implement audit logging for sensitive operations
- Anonymous telemetry is not collected by default
- Users' data belongs to the user running the instance

## Compliance

When deploying OmniAgent for sensitive use cases:

- Ensure compliance with GDPR, CCPA, and local data protection laws
- Implement proper data retention and deletion policies
- Document data access and processing
- Conduct security assessments before production deployment

---

Thank you for helping us keep OmniAgent secure!
