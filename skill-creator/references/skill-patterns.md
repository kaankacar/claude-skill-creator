# Skill Design Patterns

## Choosing Your Approach: Problem-First vs. Tool-First

- **Problem-first:** User describes an outcome (e.g., "I need to set up a project workspace"). The skill orchestrates the right MCP calls in the right sequence. Users describe outcomes; the skill handles the tools.
- **Tool-first:** User already has tools connected (e.g., "I have Notion MCP connected"). The skill teaches Claude the optimal workflows and best practices. Users have access; the skill provides expertise.

Most skills lean one direction. Knowing which framing fits helps choose the right pattern.

## Pattern 1: Sequential Workflow Orchestration

**Use when:** Users need multi-step processes in a specific order.

Key techniques:
- Explicit step ordering
- Dependencies between steps
- Validation at each stage
- Rollback instructions for failures

Example structure:
```markdown
## Workflow: Onboard New Customer
### Step 1: Create Account
Call MCP tool: `create_customer`
Parameters: name, email, company

### Step 2: Setup Payment
Call MCP tool: `setup_payment_method`
Wait for: payment method verification

### Step 3: Create Subscription
Call MCP tool: `create_subscription`
Parameters: plan_id, customer_id (from Step 1)

### Step 4: Send Welcome Email
Call MCP tool: `send_email`
Template: welcome_email_template
```

## Pattern 2: Multi-MCP Coordination

**Use when:** Workflows span multiple services.

Key techniques:
- Clear phase separation
- Data passing between MCPs
- Validation before moving to next phase
- Centralized error handling

Example: Design-to-development handoff
```markdown
### Phase 1: Design Export (Figma MCP)
1. Export design assets from Figma
2. Generate design specifications
3. Create asset manifest

### Phase 2: Asset Storage (Drive MCP)
1. Create project folder in Drive
2. Upload all assets
3. Generate shareable links

### Phase 3: Task Creation (Linear MCP)
1. Create development tasks
2. Attach asset links to tasks
3. Assign to engineering team

### Phase 4: Notification (Slack MCP)
1. Post handoff summary to #engineering
2. Include asset links and task references
```

## Pattern 3: Iterative Refinement

**Use when:** Output quality improves with iteration.

Key techniques:
- Explicit quality criteria
- Iterative improvement loops
- Validation scripts
- Know when to stop iterating

Example: Report generation
```markdown
### Initial Draft
1. Fetch data via MCP
2. Generate first draft report
3. Save to temporary file

### Quality Check
1. Run validation script: `scripts/check_report.py`
2. Identify issues: missing sections, inconsistent formatting, data errors

### Refinement Loop
1. Address each identified issue
2. Regenerate affected sections
3. Re-validate
4. Repeat until quality threshold met

### Finalization
1. Apply final formatting
2. Generate summary
3. Save final version
```

## Pattern 4: Context-Aware Tool Selection

**Use when:** Same outcome, different tools depending on context.

Key techniques:
- Clear decision criteria
- Fallback options
- Transparency about choices

Example: Smart file storage
```markdown
### Decision Tree
1. Check file type and size
2. Determine best storage location:
   - Large files (>10MB): Use cloud storage MCP
   - Collaborative docs: Use Notion/Docs MCP
   - Code files: Use GitHub MCP
   - Temporary files: Use local storage

### Execute Storage
Based on decision:
- Call appropriate MCP tool
- Apply service-specific metadata
- Generate access link

### Provide Context to User
Explain why that storage was chosen
```

## Pattern 5: Domain-Specific Intelligence

**Use when:** Skill adds specialized knowledge beyond tool access.

Key techniques:
- Domain expertise embedded in logic
- Compliance/validation before action
- Comprehensive documentation
- Clear governance

Example: Financial compliance
```markdown
### Before Processing (Compliance Check)
1. Fetch transaction details via MCP
2. Apply compliance rules:
   - Check sanctions lists
   - Verify jurisdiction allowances
   - Assess risk level
3. Document compliance decision

### Processing
IF compliance passed:
- Call payment processing MCP tool
- Apply appropriate fraud checks
- Process transaction
ELSE:
- Flag for review
- Create compliance case

### Audit Trail
- Log all compliance checks
- Record processing decisions
- Generate audit report
```

## Skill Categories

| Category | Description | Key Techniques | Example |
|---|---|---|---|
| Document & Asset Creation | Creating consistent output | Style guides, templates, quality checklists | frontend-design, report-generator |
| Workflow Automation | Multi-step processes | Validation gates, templates, refinement loops | skill-creator, sprint-planner |
| MCP Enhancement | Workflow guidance for MCP tools | MCP coordination, domain expertise, error handling | sentry-code-review |
