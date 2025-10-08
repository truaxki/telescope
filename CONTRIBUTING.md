# Contributing to Telescope 🔭

Thank you for your interest in contributing to Telescope! This document provides guidelines for contributing to make the process smooth and effective.

---

## 🎯 Ways to Contribute

### 1. New Focus Modes
Add specialized analysis patterns for specific domains.

**Example:** E-commerce focus mode
- File: Create new focus mode in `telescope.md`
- Agents: Define which agents are activated
- Emphasis: What aspects to analyze
- Documentation: Update README with new focus mode

### 2. Agent Specializations
Create new agent types for domain-specific analysis.

**Example:** Security Specialist Agent
- Define expertise area
- Create prompt template
- Document output requirements
- Add to agent assignment configuration

### 3. Template Improvements
Enhance existing prompts for better analysis quality.

**Areas to improve:**
- More specific analysis requirements
- Better output structure
- Additional examples
- Clearer success criteria

### 4. Documentation
Help others use Telescope effectively.

**Documentation needs:**
- More use case examples
- Tutorial videos
- Integration guides
- Best practices

### 5. Bug Reports
Report issues, edge cases, or unexpected behavior.

**Good bug reports include:**
- What you tried to analyze
- Command used
- Expected vs. actual behavior
- Relevant error messages
- Telescope version

---

## 🚀 Getting Started

### 1. Fork the Repository
```bash
# Fork on GitHub, then clone your fork
git clone https://github.com/YOUR_USERNAME/telescope.git
cd telescope
```

### 2. Create Feature Branch
```bash
git checkout -b feature/your-feature-name

# Examples:
# git checkout -b feature/ecommerce-focus-mode
# git checkout -b feature/security-agent
# git checkout -b docs/tutorial-videos
```

### 3. Make Changes
Edit `telescope.md` or documentation files.

### 4. Test Your Changes
Run Telescope with your changes on real codebases:
```bash
# Test on small project first
"Telescope analyze /path/to/small-project"

# Then test on larger/complex project
"Telescope analyze /path/to/large-project"

# Test focus mode if applicable
"Telescope focus on [your-new-mode]"
```

### 5. Commit Changes
```bash
git add .
git commit -m "feat: add e-commerce focus mode

- Activated agents: 2, 3, 5
- Focus on checkout flow, payment integration, inventory
- Includes example output
"
```

**Commit Message Format:**
```
<type>: <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance

### 6. Push Changes
```bash
git push origin feature/your-feature-name
```

### 7. Create Pull Request
- Go to GitHub
- Click "New Pull Request"
- Fill out PR template
- Request review

---

## 📋 Contribution Guidelines

### Code Quality
- **Clear prompts:** Agent prompts should be specific and actionable
- **Consistent format:** Follow existing template structure
- **Examples included:** Provide output examples for new features
- **Tested:** Verify changes work on real codebases

### Documentation
- **Update README:** If adding features, update README
- **Inline comments:** Explain complex logic in prompts
- **Examples:** Include before/after examples
- **Use cases:** Document when to use new features

### Pull Request Requirements
- [ ] Feature branch created
- [ ] Changes tested on real codebase
- [ ] Documentation updated
- [ ] Examples included
- [ ] Commit messages follow format
- [ ] No merge conflicts

---

## 🎨 Prompt Engineering Best Practices

When contributing new prompts or improving existing ones:

### 1. Be Specific
```markdown
# Bad:
"Analyze the code"

# Good:
"Analyze ADK agent hierarchies:
1. Map agent relationships (visual diagram)
2. Document session state keys (type, structure, usage)
3. Identify callback patterns (before/after agent/tool/model)
4. Assess against ADK best practices"
```

### 2. Provide Structure
```markdown
# Include:
- Required sections (numbered list)
- Output format (markdown, location, naming)
- Success criteria (what makes it complete)
- Examples (show expected output format)
```

### 3. Include Context
```markdown
# Give agent context:
- What specialization they have
- What files/directories to focus on
- What depth of analysis required
- What other agents are doing (avoid overlap)
```

### 4. Define Success
```markdown
# Clear completion criteria:
- "Analysis complete when:"
  ✅ All assigned files reviewed
  ✅ Pain points identified with severity
  ✅ Recommendations prioritized
  ✅ Examples provided for key findings
```

### 5. Show Examples
```markdown
# Include example output:
"Example Pain Point:
❌ Pain Point 1: Missing State Documentation
- Problem: [specific issue]
- Location: [file:line]
- Impact: [effect on system]
- Severity: [Critical/High/Medium/Low]
- Recommendation: [how to fix]"
```

---

## 🧪 Testing

### Manual Testing Checklist

When testing changes:

- [ ] **Small Project** (< 1k lines)
  - Runs without errors
  - Output structure correct
  - Findings relevant

- [ ] **Medium Project** (1k-10k lines)
  - Completes in reasonable time
  - All agents finish
  - Synthesis coherent

- [ ] **Large Project** (> 10k lines)
  - Doesn't timeout
  - Findings comprehensive
  - No duplicate analysis

- [ ] **Different Tech Stacks**
  - JavaScript/TypeScript
  - Python
  - Other languages

- [ ] **Focus Modes**
  - Each focus mode works
  - Right agents activated
  - Appropriate depth

### Test Cases

Create test cases for new features:

```markdown
# Test Case: E-commerce Focus Mode

Input:
- Codebase: E-commerce platform (Next.js + Stripe)
- Command: "Telescope focus on e-commerce"

Expected Output:
- Agents activated: 2 (Backend), 3 (Frontend), 5 (Quality)
- Analysis includes:
  ✓ Checkout flow analysis
  ✓ Payment integration review
  ✓ Inventory management patterns
  ✓ Order processing architecture
- Pain points identified for e-commerce specific issues
- Recommendations relevant to online retail

Actual Output:
[Record what actually happened]

Pass/Fail: [Result]
```

---

## 📝 Documentation Standards

### README Updates

When adding features, update README sections:

1. **Features** - Add to feature list
2. **Focus Modes** - Add to reference table
3. **Examples** - Provide usage example
4. **Use Cases** - Add relevant use case

### Code Comments

Add comments to complex template sections:

```markdown
<!-- Template Configuration: ADK Architecture Focus -->
<!-- This section defines which agents analyze ADK patterns -->
<!-- Agents 1 & 2 are activated for deep agent hierarchy analysis -->
```

### CHANGELOG

Update CHANGELOG.md for all changes:

```markdown
## [Unreleased]

### Added
- E-commerce focus mode for retail platform analysis
- Security specialist agent for vulnerability detection

### Changed
- Improved ADK architecture analysis depth
- Enhanced session state documentation requirements

### Fixed
- Fixed agent overlap in database focus mode
```

---

## 🤝 Community

### Getting Help

- **Questions:** Open a [Discussion](https://github.com/yourusername/telescope/discussions)
- **Bugs:** Open an [Issue](https://github.com/yourusername/telescope/issues)
- **Ideas:** Start a [Discussion](https://github.com/yourusername/telescope/discussions)

### Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Focus on improving Telescope
- Help others learn prompt engineering
- Share knowledge and examples

---

## 🎓 Learning Resources

### Prompt Engineering
- [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/claude/docs)
- [OpenAI Best Practices](https://platform.openai.com/docs/guides/prompt-engineering)
- [Google ADK Documentation](https://cloud.google.com/vertex-ai/docs/agent-engine)

### Multi-Agent Systems
- Study `telescope.md` orchestration patterns
- Review agent specialization examples
- Analyze synthesis agent prompts

### Template Design
- Examine existing focus modes
- Compare agent prompt variations
- Study output structure requirements

---

## 🏆 Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Recognized in README (significant contributions)

---

## ❓ FAQ

### Q: How do I add a new focus mode?
1. Edit `telescope.md` Section 1.2 (Focus Mode Configuration)
2. Define which agents are activated
3. Specify analysis emphasis areas
4. Create example output
5. Update README focus modes table
6. Test on real codebase

### Q: Can I add more than 5 agents?
Yes! You can add specialized agents:
1. Define agent in Section 1.4 (Agent Specialization)
2. Create agent prompt template in Section 2.5
3. Add to orchestration document template
4. Update README

### Q: How do I test changes?
1. Copy modified `telescope.md` to test project
2. Run Telescope with your changes
3. Verify outputs in `ai_docs/documentation/`
4. Check quality of analysis
5. Iterate on prompts

### Q: What makes a good prompt?
- Specific requirements
- Clear structure
- Success criteria
- Examples included
- Context provided
- Testable outputs

---

**Thank you for contributing to Telescope! 🔭**

Together we're making codebase analysis better through the power of prompt templates.
