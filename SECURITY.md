# Security Policy

## Supported Versions

We release patches for security vulnerabilities. Currently supported versions:

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

We take security seriously. If you discover a security vulnerability, please follow these steps:

### 1. Do Not Open a Public Issue

Please do not open a public GitHub issue for security vulnerabilities. This could put users at risk.

### 2. Report Privately

Send a detailed report to: **duynguyen71@github.com** (or create a private security advisory on GitHub)

Include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if any)
- Your contact information

### 3. Response Timeline

- **24 hours**: Initial acknowledgment
- **7 days**: Detailed response with assessment
- **30 days**: Fix released (for confirmed vulnerabilities)

## Security Considerations for Skills

### Skill Execution

Skills run with full agent permissions. Users should:

- Review skill code before installation
- Only install skills from trusted sources
- Check the security risk assessment on skills.sh
- Keep skills updated

### Data Privacy

Skills may:
- Read files in your project
- Execute commands
- Access environment variables
- Make network requests

**Never include sensitive data in skill files:**
- API keys
- Passwords
- Personal information
- Proprietary code

### Safe Skill Development

When creating skills:

1. **Input Validation**: Validate all user inputs
2. **Command Injection**: Avoid executing arbitrary commands
3. **File Access**: Limit file system access to necessary paths
4. **Network Requests**: Only make necessary external requests
5. **Dependencies**: Keep dependencies minimal and audited

### Code Review

All skills should be reviewed for:
- Malicious code
- Unintended side effects
- Data leakage risks
- Command injection vulnerabilities
- Path traversal issues

## Known Security Considerations

### sql-optimization
- Reads SQL files and queries
- Does not execute queries
- Does not modify databases
- Safe for code review

### skill-creator
- Creates and modifies files
- Executes Python scripts for evaluation
- Spawns subagents
- Review generated code before use

### ui-ux-pro-max
- Reads design files
- Executes Python scripts for data processing
- Does not make external network requests
- Safe for design work

## Security Best Practices

### For Users

1. **Review Before Install**: Check skill code on GitHub
2. **Use Auto-Update**: Keep skills current with security patches
3. **Limit Permissions**: Use Claude Code permission modes
4. **Report Issues**: Report suspicious behavior immediately
5. **Backup Data**: Regular backups before using new skills

### For Contributors

1. **Code Review**: All PRs require review
2. **Dependency Scanning**: Check for vulnerable dependencies
3. **Static Analysis**: Use linters and security scanners
4. **Test Security**: Include security test cases
5. **Document Risks**: Clearly document any security considerations

## Vulnerability Disclosure

When a vulnerability is confirmed:

1. We'll develop and test a fix
2. Release a security patch
3. Update CHANGELOG.md
4. Notify users via GitHub Security Advisory
5. Credit the reporter (if desired)

## Security Updates

Subscribe to security updates:
- Watch this repository on GitHub
- Enable GitHub Security Advisories
- Check CHANGELOG.md regularly

## Third-Party Dependencies

We regularly audit dependencies for:
- Known vulnerabilities (CVEs)
- Outdated packages
- Malicious code
- License compliance

## Scope

This security policy covers:
- All skills in this repository
- Supporting scripts and tools
- Documentation and examples

Out of scope:
- Claude Code platform itself
- Third-party integrations
- User's local environment

## Contact

For security concerns: **duynguyen71@github.com**

For general issues: [GitHub Issues](https://github.com/duynguyen71/MyClaudeSkills/issues)

## Acknowledgments

We appreciate responsible disclosure and will acknowledge security researchers who help improve our security.

---

Last updated: 2026-04-16
