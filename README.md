# MyClaudeSkills

A collection of custom skills for Claude Code to enhance SQL optimization and skill development workflows.

## Available Skills

### sql-optimization
Universal SQL performance optimization assistant for comprehensive query tuning, indexing strategies, and database performance analysis across all SQL databases (MySQL, PostgreSQL, SQL Server, Oracle).

**Features:**
- Query performance analysis and optimization
- Index strategy recommendations
- Subquery and JOIN optimization
- Pagination optimization techniques
- Aggregation optimization
- Anti-pattern detection
- Database-agnostic best practices

### skill-creator
Create new skills, modify and improve existing skills, and measure skill performance.

**Features:**
- Skill creation from scratch
- Iterative skill improvement workflow
- Evaluation and benchmarking system
- Test case generation and validation
- Description optimization for better triggering
- Skill packaging for distribution

## Installation

### Using Claude Code CLI

```bash
# Install from GitHub
claude skill install duynguyen71/MyClaudeSkills/sql-optimization
claude skill install duynguyen71/MyClaudeSkills/skill-creator
```

### Manual Installation

1. Clone this repository:
```bash
git clone git@github.com:duynguyen71/MyClaudeSkills.git
```

2. Copy skills to your Claude skills directory:
```bash
cp -r MyClaudeSkills/.agents/skills/* ~/.claude/skills/
```

## Usage

### sql-optimization

The skill automatically triggers when you work with SQL queries or database optimization tasks:

```
"Help me optimize this slow query"
"Analyze the execution plan for this SQL"
"What indexes should I add for better performance?"
```

### skill-creator

Use when creating or improving skills:

```
"Create a new skill for PDF processing"
"Improve my existing skill with better test cases"
"Run benchmarks on this skill"
```

## Repository Structure

```
MyClaudeSkills/
├── .agents/
│   └── skills/
│       ├── sql-optimization/
│       │   └── SKILL.md
│       └── skill-creator/
│           ├── SKILL.md
│           ├── agents/
│           ├── references/
│           ├── scripts/
│           └── eval-viewer/
├── skills-lock.json
└── README.md
```

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

MIT License - feel free to use and modify these skills for your needs.

## Author

Duy Nguyen

## Support

For issues or questions, please open an issue on GitHub.
