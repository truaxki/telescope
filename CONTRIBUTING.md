# Contributing to Telescope 🔭

Thank you for contributing to Telescope! This guide will help you get started.

---

## Ways to Contribute

### 1. New Focus Modes
Add specialized analysis patterns for specific domains.

**Steps:**
1. Add focus mode to `telescope-prompts/focus-modes/`
2. Define which agents activate and emphasis areas
3. Update README focus modes table
4. Test on real codebase

### 2. Agent Specializations
Create new agent types for domain-specific analysis.

**Steps:**
1. Add agent template to `telescope-prompts/agents/`
2. Define expertise area and output requirements
3. Update orchestration configuration
4. Test and document

### 3. Template Improvements
Enhance existing prompts for better analysis quality.

**Focus areas:**
- More specific requirements
- Better output structure
- Additional examples
- Clearer success criteria

### 4. Bug Reports
Report issues with detailed reproduction steps.

**Include:**
- Command used
- Expected vs actual behavior
- Error messages
- Telescope version

---

## Quick Start

### 1. Fork & Clone
```bash
git clone https://github.com/YOUR_USERNAME/telescope.git
cd telescope
```

### 2. Create Branch
```bash
git checkout -b feature/your-feature-name
# Examples: feature/ecommerce-focus, docs/tutorial
```

### 3. Make Changes
Edit files in `telescope-prompts/` or documentation.

### 4. Test Changes
```bash
# Test on small project first
"Telescope analyze /path/to/small-project"

# Test on larger project
"Telescope analyze /path/to/large-project"

# Test new focus mode
"Telescope focus on [your-new-mode]"
```

### 5. Commit
```bash
git commit -m "feat: add e-commerce focus mode

- Activated agents: 2, 3, 5
- Focus: checkout flow, payment, inventory
- Includes example output"
```

**Commit types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `refactor`: Code refactoring
- `test`: Tests
- `chore`: Maintenance

### 6. Submit PR
Push changes and create pull request on GitHub.

---

## Prompt Engineering Best Practices

### Be Specific
```markdown
# Bad:
"Analyze the code"

# Good:
"Analyze ADK agent hierarchies:
1. Map agent relationships (visual)
2. Document state keys (type, structure)
3. Identify callback patterns
4. Assess vs best practices"
```

### Provide Structure
Include required sections, output format, success criteria, and examples.

### Include Context
Give agents their specialization, focus files/directories, analysis depth, and coordination with other agents.

### Define Success
```markdown
Analysis complete when:
✅ All assigned files reviewed
✅ Pain points identified with severity
✅ Recommendations prioritized
✅ Examples provided
```

### Show Examples
Include example outputs for pain points, recommendations, and findings.

---

## Testing Checklist

- [ ] **Small Project** (< 1k lines) - Runs without errors, correct output
- [ ] **Medium Project** (1k-10k lines) - Completes in reasonable time
- [ ] **Large Project** (> 10k lines) - Doesn't timeout, comprehensive
- [ ] **Different Stacks** - JS/TS, Python, etc.
- [ ] **Focus Modes** - Each mode activates correct agents

---

## PR Requirements

- [ ] Feature branch created
- [ ] Changes tested on real codebase
- [ ] Documentation updated (README, focus modes table)
- [ ] Examples included
- [ ] Commit messages follow format
- [ ] No merge conflicts

---

## Community

- **Questions:** [Discussions](https://github.com/yourusername/telescope/discussions)
- **Bugs:** [Issues](https://github.com/yourusername/telescope/issues)

**Code of Conduct:**
- Be respectful and inclusive
- Provide constructive feedback
- Share knowledge and examples

---

## FAQ

**Q: How do I add a new focus mode?**
1. Create file in `telescope-prompts/focus-modes/`
2. Define agent activation and emphasis
3. Update README focus modes table
4. Test on real codebase

**Q: Can I add more agents?**
Yes! Add to `telescope-prompts/agents/` and update orchestration.

**Q: What makes a good prompt?**
- Specific requirements
- Clear structure
- Success criteria
- Examples included
- Context provided

---

**Thank you for contributing to Telescope!** 🔭
