# Skill Creator - A Claude Code Skill for Building Skills

A meta-skill that helps you create well-structured Claude Code skills through an interactive, step-by-step workflow.

## Inspiration

This skill was built based on [Anthropic's Complete Guide to Building Skills for Claude](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf), which covers everything from planning and structure to testing and distribution. The guide defines skills as portable instruction sets that teach Claude how to handle specific tasks and workflows consistently across Claude.ai, Claude Code, and the API.

Rather than re-reading the guide every time you want to build a new skill, this meta-skill encodes all the best practices, validation rules, design patterns, and structural requirements directly into an interactive workflow that Claude follows when you ask it to create a skill.

## What It Does

When you say things like "create a skill", "build a skill", or "help me write a skill", this skill activates and walks you through a 9-step process:

1. **Gather use cases** - Identifies what the skill should do, its category (Document & Asset Creation, Workflow Automation, or MCP Enhancement), and whether it follows a problem-first or tool-first approach
2. **Generate the skill name** - Creates a valid kebab-case name following all naming rules
3. **Write the description** - Crafts a trigger-aware description with what/when/capabilities and negative triggers
4. **Define folder structure** - Proposes the right directories (`scripts/`, `references/`, `assets/`) based on actual needs
5. **Define success criteria** - Sets quantitative and qualitative metrics for measuring the skill's effectiveness
6. **Write the SKILL.md** - Generates the full file with proper YAML frontmatter, progressive disclosure, instructions, examples, and troubleshooting
7. **Create the files** - Writes everything to disk
8. **Validate and test** - Runs through a comprehensive checklist and suggests test queries
9. **Provide next steps** - Installation across all surfaces, iteration guidance, and distribution tips

It also supports **reviewing and improving existing skills** - just ask it to review a skill and it will flag issues, suggest improvements, and identify triggering risks.

## Installation

### Claude Code

Place the `skill-creator/` folder in your Claude Code skills directory:

```bash
# Clone this repo
git clone https://github.com/kaankacar/claude-skill-creator.git

# Copy the skill folder to your Claude Code skills directory
cp -r claude-skill-creator/skill-creator/ ~/.claude/skills/skill-creator/
```

Alternatively, if your project has a `.claude/skills/` directory, place it there for project-scoped usage.

### Claude.ai

1. Zip the `skill-creator/` folder:
   ```bash
   cd skill-creator && zip -r ../skill-creator.zip . && cd ..
   ```
2. Open Claude.ai
3. Go to **Settings > Capabilities > Skills**
4. Click **Upload skill** and select the zip file
5. Toggle the skill on

### API

Skills can be added to Messages API requests via the `container.skills` parameter. The `/v1/skills` endpoint manages skills programmatically. Requires the Code Execution Tool beta.

## Folder Structure

```
skill-creator/
├── SKILL.md                              # Main skill file (frontmatter + instructions)
└── references/
    ├── yaml-frontmatter-spec.md          # Complete YAML field reference
    ├── skill-patterns.md                 # 5 design patterns with full examples
    └── validation-checklist.md           # Pre/post-upload validation checklist
```

Note: The `README.md` you're reading is at the **repo level**, not inside the skill folder (as per Anthropic's guidelines - skill folders should not contain a README.md).

## Usage Examples

Once installed, try these prompts:

- "Create a skill for generating API documentation"
- "Build a skill that manages Linear sprint planning via MCP"
- "Help me write a skill for code review workflows"
- "Review my existing skill and suggest improvements"
- "Make a skill for consistent report generation"

## Design Patterns

The skill guides you toward the most appropriate architecture based on your use case:

| Pattern | Use When |
|---|---|
| **Sequential Workflow** | Multi-step process in a specific order |
| **Multi-MCP Coordination** | Workflow spans multiple services |
| **Iterative Refinement** | Output quality improves with revision loops |
| **Context-Aware Selection** | Same outcome, different tools depending on context |
| **Domain-Specific Intelligence** | Skill adds specialized knowledge beyond tool access |

## Key Concepts from the Guide

- **Progressive Disclosure**: Skills use a three-level system (frontmatter always loaded, SKILL.md body loaded when relevant, linked files discovered as needed) to minimize token usage
- **Composability**: Skills should work well alongside other skills, not assume exclusivity
- **Portability**: Skills work identically across Claude.ai, Claude Code, and the API
- **Trigger-Aware Descriptions**: The description field determines when Claude loads the skill - it must include both what the skill does and when to use it with specific trigger phrases

## Contributing

To improve this skill:

1. Use it to create a few skills and note any friction
2. Bring edge cases or failures back: "Use the issues from this chat to improve how the skill handles [specific case]"
3. Submit a PR with improvements

## Resources

- [Anthropic Skills Documentation](https://docs.anthropic.com/en/docs/agents-and-tools/skills)
- [Anthropic Skills Repository](https://github.com/anthropics/skills)
- [Claude Developers Discord](https://discord.gg/claudedev)
- [Bug Reports: anthropics/skills/issues](https://github.com/anthropics/skills/issues)
