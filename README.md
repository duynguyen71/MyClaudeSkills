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

### Quick Install (Recommended)

Install all skills at once:

```bash
# Install both skills with one command
claude skill install duynguyen71/MyClaudeSkills/sql-optimization duynguyen71/MyClaudeSkills/skill-creator
```

Or install individually:

```bash
# Install sql-optimization only
claude skill install duynguyen71/MyClaudeSkills/sql-optimization

# Install skill-creator only
claude skill install duynguyen71/MyClaudeSkills/skill-creator
```

### Auto-Update Setup

Enable automatic updates to always get the latest improvements:

```bash
# Enable auto-update for all skills
claude skill auto-update enable

# Or enable for specific skills
claude skill auto-update enable sql-optimization skill-creator

# Check auto-update status
claude skill auto-update status
```

**Manual update when needed:**
```bash
# Update all skills
claude skill update

# Update specific skill
claude skill update sql-optimization
```

### Fast Installation Script

Create a quick install script for easy setup:

```bash
# Create install script
cat > install-skills.sh << 'EOF'
#!/bin/bash
echo "Installing MyClaudeSkills..."
claude skill install duynguyen71/MyClaudeSkills/sql-optimization
claude skill install duynguyen71/MyClaudeSkills/skill-creator
claude skill auto-update enable sql-optimization skill-creator
echo "✓ Installation complete!"
claude skill list
EOF

chmod +x install-skills.sh
./install-skills.sh
```

### Manual Installation (Alternative)

If you prefer manual control:

1. Clone this repository:
```bash
git clone git@github.com:duynguyen71/MyClaudeSkills.git
cd MyClaudeSkills
```

2. Copy skills to your Claude skills directory:
```bash
cp -r .agents/skills/* ~/.claude/skills/
```

3. Verify installation:
```bash
claude skill list
```

## Usage

Skills in Claude Code are automatically triggered based on your task context. Once installed, Claude will invoke them when relevant.

### sql-optimization

**When it triggers:**
- Working with SQL queries or database optimization
- Analyzing query performance
- Designing database indexes
- Reviewing execution plans

**Example prompts:**

```bash
# Query optimization
"Help me optimize this slow query in users.sql"

# Index recommendations
"What indexes should I add for better performance on the orders table?"

# Execution plan analysis
"Analyze the execution plan for this query and suggest improvements"

# Pagination optimization
"Convert this OFFSET-based pagination to cursor-based"

# Anti-pattern detection
"Review my SQL code for performance anti-patterns"
```

**Working with files:**
```bash
# Optimize a specific SQL file
claude "Optimize the queries in database/migrations/001_create_users.sql"

# Review entire project
claude "Review all SQL files in this project for performance issues"
```

**Example workflow:**
1. Open a SQL file or paste a query
2. Ask Claude to optimize it
3. The skill provides:
   - Optimized query version
   - Index recommendations with CREATE INDEX statements
   - Explanation of improvements
   - Performance impact analysis

### skill-creator

**When it triggers:**
- Creating new skills from scratch
- Improving existing skills
- Running skill evaluations
- Optimizing skill descriptions

**Example prompts:**

```bash
# Create a new skill
"Create a new skill for processing PDF documents"

# Improve existing skill
"Improve my existing skill at ~/.claude/skills/my-skill with better test cases"

# Run evaluations
"Run benchmarks on the pdf-processor skill"

# Optimize description
"Optimize the description for my skill to improve triggering accuracy"
```

**Complete workflow example:**

```bash
# 1. Start skill creation
claude "Create a skill that helps with Docker configuration"

# 2. Claude will:
#    - Interview you about requirements
#    - Draft the SKILL.md
#    - Create test cases
#    - Run evaluations

# 3. Review and iterate
#    - Claude opens a browser with test results
#    - You provide feedback
#    - Claude improves the skill

# 4. Package and install
#    - Claude packages the skill as .skill file
#    - Install: claude skill install ./my-skill.skill
```

**Advanced usage:**

```bash
# Create skill from existing workflow
"Turn this conversation into a skill"

# Benchmark with variance analysis
"Run 10 iterations of benchmarks on my-skill to measure consistency"

# Description optimization
"Optimize the trigger description for better accuracy"
```

### Using Skills in Different Environments

**Claude Code CLI:**
```bash
# Skills trigger automatically
claude "optimize this query: SELECT * FROM users WHERE created_at > '2024-01-01'"
```

**Claude Code Desktop/Web:**
- Skills trigger automatically in conversations
- Use `/skill-name` to explicitly invoke a skill
- Check available skills with `/skills`

**VS Code / JetBrains Extensions:**
- Skills work in the Claude Code panel
- Right-click files and select "Ask Claude" for context-aware help

## Tips for Best Results

**For sql-optimization:**
- Provide the full query context (tables, indexes, data volume)
- Share execution plans when available
- Mention your database system (MySQL, PostgreSQL, etc.)
- Include performance metrics if you have them

**For skill-creator:**
- Be specific about what the skill should do
- Provide example inputs and expected outputs
- Test with realistic scenarios
- Iterate based on evaluation feedback

## Troubleshooting

**Skill not triggering?**
- Check installation: `claude skill list`
- Try explicit invocation: `/sql-optimization` or `/skill-creator`
- Verify skill description matches your use case
- Update skills: `claude skill update`

**Installation issues?**
- Verify Claude Code is installed: `claude --version`
- Check network connection for GitHub access
- Try manual installation method
- Clear skill cache: `rm -rf ~/.claude/skills/.cache`

**Update not working?**
- Check auto-update status: `claude skill auto-update status`
- Manually update: `claude skill update --force`
- Reinstall if needed: `claude skill uninstall skill-name && claude skill install ...`

**Need help?**
- Check Claude Code docs: `claude help`
- View skill details: `claude skill info skill-name`
- Report issues on GitHub: https://github.com/duynguyen71/MyClaudeSkills/issues

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
