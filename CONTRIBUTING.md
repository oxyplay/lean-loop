# Contributing to Lean Loop

Thanks for your interest in contributing! Lean Loop is a lightweight methodology — contributions should keep it simple.

## How to Contribute

### Report Issues

- Use [GitHub Issues](../../issues) for bugs, feature requests, and questions
- Check existing issues before creating a new one
- Include steps to reproduce for bug reports

### Submit Changes

1. Fork the repository
2. Create a feature branch: `git checkout -b my-improvement`
3. Make your changes
4. Test that the skill installs and initializes correctly: `npx skills add ./lean-loop -g`
5. Submit a pull request

### What to Contribute

**Welcome:**
- Template improvements (better structure, clearer language)
- Documentation fixes and clarifications
- New examples in `examples/`
- Translations of README
- Anti-pattern additions to SKILL.md

**Discuss first (open an issue):**
- Changes to the core PLAN → APPLY → UNIFY cycle
- New phases or sub-phases
- Changes to TDD_RULES.md templates
- Adding dependencies or tooling

### Style Guidelines

- Keep it simple. Lean Loop's value is in its minimalism.
- Markdown files: use consistent heading levels and formatting
- Templates: keep emoji/formatting consistent with existing files
- No code — this is a methodology, not a framework

### Pull Request Checklist

- [ ] Changes are minimal and focused
- [ ] README updated if behavior changes
- [ ] Templates updated if structure changes
- [ ] No breaking changes to existing `.system/` file formats

## License

By contributing, you agree your contributions will be licensed under the MIT License.
