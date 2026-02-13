# Skill Validation Checklist

## Before You Start
- [ ] Identified 2-3 concrete use cases
- [ ] Tools identified (built-in or MCP)
- [ ] Reviewed example skills
- [ ] Planned folder structure

## Before Upload

### Structure
- [ ] Folder named in kebab-case
- [ ] SKILL.md file exists (exact spelling, case-sensitive)
- [ ] YAML frontmatter has `---` delimiters (opening and closing)
- [ ] name field: kebab-case, no spaces, no capitals
- [ ] name matches folder name
- [ ] description includes WHAT and WHEN
- [ ] description under 1024 characters
- [ ] No XML tags (< >) anywhere in frontmatter
- [ ] No README.md inside skill folder
- [ ] No "claude" or "anthropic" in skill name

### Content
- [ ] Instructions are clear and actionable
- [ ] Steps are numbered and ordered
- [ ] Error handling included
- [ ] Examples provided
- [ ] References clearly linked (if applicable)
- [ ] SKILL.md under 5,000 words
- [ ] Detailed docs moved to references/ directory
- [ ] Critical instructions appear near the top

### Triggering
- [ ] Triggers on obvious task descriptions
- [ ] Triggers on paraphrased requests
- [ ] Does NOT trigger on unrelated topics
- [ ] Negative triggers included if scope could be confused

## Testing Tiers

### Tier 1: Manual Testing in Claude.ai
- Run queries directly and observe behavior
- Fast iteration, no setup required
- Best for: initial development, quick iterations

### Tier 2: Scripted Testing in Claude Code
- Automate test cases for repeatable validation across changes
- Best for: skills used by teams

### Tier 3: Programmatic Testing via Skills API
- Build evaluation suites that run systematically against defined test sets
- Best for: skills deployed to many users

### Recommended Test Cases

**Triggering tests (run 10-20 queries):**
- 5+ queries that SHOULD trigger the skill
- 3+ queries that should NOT trigger the skill
- Paraphrased versions of trigger phrases

**Functional tests:**
- Valid outputs generated
- API/MCP calls succeed (for MCP skills)
- Error handling works (test failure scenarios)
- Edge cases covered

**Performance comparison (with vs. without skill):**
- Number of back-and-forth messages
- Number of failed API calls
- Total tokens consumed
- Quality of output

**Debugging tip:** Ask Claude "When would you use the [skill name] skill?" to verify triggering behavior.

## After Upload

- [ ] Tested in real conversations
- [ ] Monitored for under/over-triggering
- [ ] Collected user feedback
- [ ] Iterated on description and instructions
- [ ] Updated version in metadata

## Common Issues

### Skill won't upload
- File not named exactly SKILL.md
- YAML formatting issue (missing delimiters, unclosed quotes)
- Invalid skill name (spaces or capitals)

### Skill doesn't trigger
- Description too generic (e.g., "Helps with projects")
- Missing trigger phrases
- Missing file type mentions
- **Fix:** Revise description. Add more keywords, especially technical terms.

### Skill triggers too often
- Description too broad
- Missing negative triggers
- Scope not specific enough
- **Fix:** Add negative triggers (e.g., "Do NOT use for..."), be more specific about scope.

### Instructions not followed
- Instructions too verbose (move to references/)
- Critical instructions buried (move to top)
- Ambiguous language (be specific and actionable)
- **Advanced fix:** Bundle a validation script instead of relying on language instructions. Code is deterministic.

### MCP connection issues
- Verify MCP server is connected (Settings > Extensions)
- Check authentication (API keys valid, permissions granted)
- Test MCP independently (call tools without the skill)
- Verify tool names are correct and case-sensitive

### Large context / slow responses
- SKILL.md too large (keep under 5,000 words)
- Too many skills enabled (evaluate if >20-50 enabled)
- Move detailed docs to references/ directory
