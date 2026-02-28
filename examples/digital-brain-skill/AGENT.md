# Digital Brain - Claude Instructions

This is a Digital Brain personal operating system. When working in this project:

## Core Rules

1. **Always read identity/voice.md before writing any content** - Match the user's authentic voice
2. **Append to JSONL files, never overwrite** - Preserve history
3. **Update timestamps** when modifying tracked data
4. **Cross-reference modules** - Knowledge informs content, network informs operations
5. **Extend the system** - Use the module toolkit in `module-toolkit/` to create new modules when needed

## Quick Reference

- **Writing content**: Read `identity/voice.md` first, then use templates in `content/templates/`
- **Looking up contacts**: Search `network/contacts.jsonl`, check `interactions.jsonl` for history
- **Content ideas**: Check `content/ideas.jsonl`, run `agents/scripts/content_ideas.py`
- **Task management**: Use `operations/todos.md`, align with `operations/goals.yaml`
- **Weekly review**: Run `agents/scripts/weekly_review.py`
- **Creating modules**: Read `module-toolkit/MODULE_CREATION_GUIDE.md`, follow 6 phases
- **Verifying integration**: Run `python module-toolkit/check_module_integration.py <module> <keyword>`

## File Conventions

- `.jsonl` files: One JSON object per line, append-only
- `.md` files: Human-readable, freely editable
- `.yaml` files: Configuration and structured data
- `_template.md` or `_schema` entries: Reference formats, don't modify

## Module Toolkit

The `module-toolkit/` directory (at project root) provides tools for extending the Digital Brain system:

- **MODULE_CREATION_GUIDE.md**: Complete 6-phase guide (requirements → core files → documentation → integration → cross-module → QA)
- **MODULE-TOOLKIT.md**: Quick start and toolkit overview
- **check_module_integration.py**: Automated checker that verifies proper integration into all required system files

When a user wants to add a new capability (projects, courses, habits, etc.), guide them through the module creation process using these toolkit resources.

## When User Asks To...

| Request | Action |
|---------|--------|
| "Write a post about X" | Read voice.md → Draft → Match voice patterns |
| "Prepare for meeting with Y" | Look up contact → Get interactions → Summarize |
| "What should I create?" | Run content_ideas.py → Check calendar |
| "Add contact Z" | Append to contacts.jsonl with full schema |
| "Weekly review" | Run weekly_review.py → Present insights |
| "Create a new module" | Read module-toolkit/MODULE_CREATION_GUIDE.md → Guide through 6 phases → Verify integration |
| "Check module integration" | Run check_module_integration.py → Report status |
