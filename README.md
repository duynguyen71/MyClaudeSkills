# MyClaudeSkills

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/duynguyen71/MyClaudeSkills.svg)](https://github.com/duynguyen71/MyClaudeSkills/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/duynguyen71/MyClaudeSkills.svg)](https://github.com/duynguyen71/MyClaudeSkills/network)
[![GitHub issues](https://img.shields.io/github/issues/duynguyen71/MyClaudeSkills.svg)](https://github.com/duynguyen71/MyClaudeSkills/issues)

A collection of custom skills for Claude Code to enhance SQL optimization and skill development workflows.

## Available Skills

### sql-optimization (v1.0.0)
Universal SQL performance optimization assistant for comprehensive query tuning, indexing strategies, and database performance analysis across all SQL databases (MySQL, PostgreSQL, SQL Server, Oracle).

**Category:** Database  
**Features:**
- Query performance analysis and optimization
- Index strategy recommendations
- Subquery and JOIN optimization
- Pagination optimization techniques
- Aggregation optimization
- Anti-pattern detection
- Database-agnostic best practices

### skill-creator (v1.0.0)
Create new skills, modify and improve existing skills, and measure skill performance.

**Category:** Development  
**Features:**
- Skill creation from scratch
- Iterative skill improvement workflow
- Evaluation and benchmarking system
- Test case generation and validation
- Description optimization for better triggering
- Skill packaging for distribution

### ui-ux-pro-max (v1.0.0)
UI/UX design intelligence for web and mobile applications with comprehensive design systems and guidelines.

**Category:** Design  
**Features:**
- 50+ design styles (glassmorphism, neumorphism, brutalism, minimalism, etc.)
- 161 color palettes with accessibility guidelines
- 57 font pairings for professional typography
- 161 product types with design reasoning
- 99 UX guidelines and best practices
- 25 chart types for data visualization
- Support for 10 tech stacks (React, Next.js, Vue, Svelte, SwiftUI, React Native, Flutter, Tailwind, shadcn/ui, HTML/CSS)
- Component design and review
- Accessibility compliance checking
- Responsive design patterns

### unity-game-studio
Claude Code Game Studios - Turn a single Claude Code session into a full game development studio.

**Category:** Game Development  
**Features:**
- 48 specialized agents (directors, leads, specialists)
- 37 game development workflows
- 8 quality gate hooks
- 11 coding standards rules
- Support for Unity, Unreal Engine, and Godot
- Complete studio hierarchy (creative, technical, production)
- Agents: game designer, programmer, artist, audio, QA, producer, and more
- Skills: brainstorming, prototyping, sprint planning, code review, asset audit, release management
- Collaborative design protocol
- Context management for long sessions

### react
Skills for React application development.

**Category:** Frontend  
**Status:** Coming soon

### springboot
Skills for Spring Boot application development.

**Category:** Backend  
**Status:** Coming soon

### sql
Additional SQL database development and optimization skills.

**Category:** Database  
**Status:** Coming soon

## Installation

### Quick Install (Recommended)

Install all skills at once:

```bash
# Install all skills with one command
claude skill install \
  duynguyen71/MyClaudeSkills/sql-optimization \
  duynguyen71/MyClaudeSkills/skill-creator \
  duynguyen71/MyClaudeSkills/ui-ux-pro-max \
  duynguyen71/MyClaudeSkills/unity-game-studio
```

Or install individually:

```bash
# Database skills
claude skill install duynguyen71/MyClaudeSkills/sql-optimization

# Development skills
claude skill install duynguyen71/MyClaudeSkills/skill-creator

# Design skills
claude skill install duynguyen71/MyClaudeSkills/ui-ux-pro-max

# Game development
claude skill install duynguyen71/MyClaudeSkills/unity-game-studio
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
claude skill install duynguyen71/MyClaudeSkills/ui-ux-pro-max
claude skill install duynguyen71/MyClaudeSkills/unity-game-studio
claude skill auto-update enable sql-optimization skill-creator ui-ux-pro-max unity-game-studio
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
cp -r skills/* ~/.claude/skills/
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
claude "design a modern dashboard with glassmorphism style"
```

**Claude Code Desktop/Web:**
- Skills trigger automatically in conversations
- Use `/skill-name` to explicitly invoke a skill
- Check available skills with `/skills`

**VS Code / JetBrains Extensions:**
- Skills work in the Claude Code panel
- Right-click files and select "Ask Claude" for context-aware help

### ui-ux-pro-max

**When it triggers:**
- Designing new pages or components
- Creating or refactoring UI elements
- Choosing color schemes and typography
- Reviewing UI code for UX quality
- Implementing responsive designs
- Building design systems

**Example prompts:**

```bash
# Design new components
"Create a modern glassmorphism login form with React and Tailwind"

# Color and typography
"Suggest a professional color palette for a SaaS dashboard"
"What font pairings work well for a fintech app?"

# Component review
"Review this button component for accessibility and UX best practices"

# Responsive design
"Make this navbar responsive with mobile-first approach"

# Design systems
"Create a design system for an e-commerce platform using shadcn/ui"
```

**Working with different stacks:**
```bash
# React/Next.js
"Build a bento grid layout with Next.js and Tailwind"

# Vue/Svelte
"Create a minimalist dashboard with Vue 3 and Composition API"

# Mobile
"Design a SwiftUI card component with neumorphism style"
"Build a Flutter bottom sheet with smooth animations"

# Design review
"Review my React component for UX issues and accessibility"
```

**Example workflow:**
1. Describe your design needs
2. The skill provides:
   - Design recommendations with reasoning
   - Code implementation in your chosen stack
   - Color palette and typography suggestions
   - Accessibility guidelines
   - Responsive design patterns
3. Review and iterate on the design

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

**For ui-ux-pro-max:**
- Specify your tech stack (React, Vue, SwiftUI, etc.)
- Mention the product type (dashboard, landing page, mobile app)
- Describe your desired style (minimalism, glassmorphism, etc.)
- Include accessibility requirements
- Share brand colors or design constraints if any

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
├── skills/
│   ├── sql-optimization/      (v1.0.0 - database)
│   ├── skill-creator/         (v1.0.0 - development)
│   ├── ui-ux-pro-max/         (v1.0.0 - design)
│   ├── unity-game-studio/     (game development)
│   ├── react/                 (frontend - coming soon)
│   ├── springboot/            (backend - coming soon)
│   └── sql/                   (database - coming soon)
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── skill_request.md
│   └── PULL_REQUEST_TEMPLATE.md
├── LICENSE
├── README.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── SECURITY.md
├── IMPROVEMENTS.md
├── IMPROVEMENT_SUMMARY.md
├── ANDROID_SKILLS_ANALYSIS.md
├── SESSION_SUMMARY.md
├── .gitignore
└── skills-lock.json
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
