# Contributing to MyClaudeSkills

Thank you for your interest in contributing to MyClaudeSkills! This document provides guidelines for contributing to this project.

## How to Contribute

### Reporting Issues

If you find a bug or have a suggestion:

1. Check if the issue already exists in [GitHub Issues](https://github.com/duynguyen71/MyClaudeSkills/issues)
2. If not, create a new issue with:
   - Clear title and description
   - Steps to reproduce (for bugs)
   - Expected vs actual behavior
   - Your environment (OS, Claude Code version, etc.)
   - Relevant logs or screenshots

### Suggesting New Skills

We welcome skill suggestions! Please:

1. Open an issue with the `skill-request` label
2. Describe the skill's purpose and use cases
3. Provide example workflows
4. Explain why it would be valuable

### Contributing Code

#### Getting Started

1. Fork the repository
2. Clone your fork:
   ```bash
   git clone git@github.com:YOUR_USERNAME/MyClaudeSkills.git
   cd MyClaudeSkills
   ```
3. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```

#### Making Changes

**For Skill Improvements:**

1. Navigate to the skill directory: `.agents/skills/skill-name/`
2. Make your changes to `SKILL.md` or related files
3. Test the skill thoroughly with Claude Code
4. Document your changes

**For New Skills:**

1. Create a new directory: `.agents/skills/your-skill-name/`
2. Add `SKILL.md` with proper frontmatter:
   ```markdown
   ---
   name: your-skill-name
   description: Clear description of when and how to use this skill
   ---
   ```
3. Add any supporting files (scripts, data, references)
4. Test extensively with various prompts
5. Update README.md to include your skill

#### Code Standards

- Use clear, descriptive variable and function names
- Add comments for complex logic
- Follow existing code style and structure
- Keep skills focused and single-purpose
- Include examples in skill documentation

#### Testing

Before submitting:

1. Test the skill with multiple realistic prompts
2. Verify it triggers correctly
3. Check for edge cases
4. Ensure no conflicts with existing skills
5. Test on different platforms if possible

#### Commit Guidelines

Use clear, descriptive commit messages:

```bash
# Good
git commit -m "Add pagination optimization examples to sql-optimization skill"

# Bad
git commit -m "update stuff"
```

Follow this format:
```
<type>: <subject>

<body>

Co-Authored-By: Your Name <your.email@example.com>
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

#### Submitting Pull Requests

1. Push your changes to your fork:
   ```bash
   git push origin feature/your-feature-name
   ```

2. Create a Pull Request with:
   - Clear title describing the change
   - Detailed description of what and why
   - Reference any related issues
   - Screenshots/examples if applicable
   - Checklist of what was tested

3. Wait for review and address feedback

### Pull Request Checklist

- [ ] Code follows existing style and conventions
- [ ] Skill has been tested with multiple prompts
- [ ] Documentation is updated (README, CHANGELOG)
- [ ] Commit messages are clear and descriptive
- [ ] No merge conflicts with main branch
- [ ] All files are properly formatted
- [ ] Skill description is clear and accurate

## Skill Development Guidelines

### Skill Structure

```
skill-name/
├── SKILL.md          # Main skill file (required)
├── scripts/          # Helper scripts (optional)
├── data/             # Data files (optional)
├── references/       # Reference documentation (optional)
└── agents/           # Sub-agents (optional)
```

### Skill Frontmatter

```yaml
---
name: skill-name
description: When to use this skill and what it does. Be specific about triggers.
compatibility: # Optional - list required tools or dependencies
  - tool-name
  - dependency-name
---
```

### Writing Effective Skills

1. **Clear Triggers**: Describe exactly when the skill should activate
2. **Focused Purpose**: One skill, one job
3. **Good Examples**: Include before/after examples
4. **Progressive Disclosure**: Start simple, add complexity as needed
5. **Error Handling**: Guide users when things go wrong
6. **Testing**: Include test cases and validation

### Skill Quality Standards

- Skill description must clearly state when to use it
- Include at least 3 realistic usage examples
- Provide clear, actionable instructions
- Use proper markdown formatting
- Test with edge cases
- Consider accessibility and inclusivity

## Documentation

When updating documentation:

- Keep language clear and concise
- Use examples liberally
- Update all relevant files (README, CHANGELOG, etc.)
- Check for broken links
- Ensure code blocks are properly formatted

## Community Guidelines

- Be respectful and constructive
- Help others learn and grow
- Share knowledge and best practices
- Give credit where due
- Focus on the work, not the person

## Questions?

- Open a [GitHub Discussion](https://github.com/duynguyen71/MyClaudeSkills/discussions)
- Check existing issues and discussions
- Read the [README](README.md) and [IMPROVEMENTS](IMPROVEMENTS.md)

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

Thank you for contributing to MyClaudeSkills! 🎉
