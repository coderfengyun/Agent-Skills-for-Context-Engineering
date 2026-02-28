---
name: module-toolkit
description: System extension tools - guides and automation for creating new Digital Brain modules. Use when adding new capabilities to the system.
---

# Module Toolkit

Tools for extending the Digital Brain system with custom modules.

## Files in This Module

| File | Type | Purpose |
|------|------|---------|
| `MODULE_CREATION_GUIDE.md` | Guide | Complete 6-phase process for creating new modules |
| `check_module_integration.py` | Script | Automated integration verification tool |

## When to Use

- **Creating a new module**: Read `MODULE_CREATION_GUIDE.md` for complete workflow
- **Verifying integration**: Run `check_module_integration.py` after creating a module

## Module Creation Overview

Creating a new module follows a **6-phase process** (see `MODULE_CREATION_GUIDE.md` for details):

1. **Requirements Analysis** (30 min) - Define purpose, design data schema
2. **Core Files Creation** (2-3 hours) - Create `<MODULE>.md`, data files, scripts
3. **Documentation** (2-3 hours) - Write schemas, workflows, examples
4. **System Integration** (1-2 hours) ⭐ **Critical** - Update SKILL.md, AGENT.md, README.md, etc.
5. **Cross-Module Integration** (1-2 hours) - Design data flows between modules
6. **Quality Assurance** (1 hour) - Test, validate, verify integration

**Total time**: ~7-10 hours for a complete module

## Integration Checker

Verify that your new module is properly integrated into all system files.

**Usage**:
```bash
python module-toolkit/check_module_integration.py <module_name> <keyword>
```

**Example**:
```bash
python module-toolkit/check_module_integration.py projects project
```

**Reports**:
- ✅/❌ Status for each required file
- Keyword occurrence counts
- Integration percentage
- Missing updates

## Agent Instructions

<instructions>
When a user wants to create a new module:

1. **Read the guide first**: Open `MODULE_CREATION_GUIDE.md` to understand the complete process
2. **Guide through phases**: Walk user through all 6 phases systematically
3. **Enforce standard format**: Module entry file MUST follow the standard format (see MODULE_CREATION_GUIDE.md for details)
4. **Focus on Phase 4**: System integration is the most critical and frequently missed step
5. **Verify with checker**: Run `check_module_integration.py` before declaring completion
6. **Format validation**: Ensure entry file format matches existing modules (identity/IDENTITY.md, content/CONTENT.md)
7. **Don't skip steps**: Each phase builds on the previous one

Critical constraints (detailed in MODULE_CREATION_GUIDE.md):
- Module entry file MUST be named `<MODULE>.md` (uppercase)
- MUST include YAML frontmatter (name + description)
- MUST include standard sections (Files, When to Use, Workflows, Agent Instructions)
- MUST include `<instructions>` tags
- Entry file should be 100-200 lines
- MUST match style of other modules

Common pitfalls to avoid:
- Skipping system integration (Phase 4)
- Using README.md instead of <MODULE>.md
- Missing YAML frontmatter or `<instructions>` tags
- Creating entry file without standard sections
- Not running the integration checker
- Not validating format against existing modules

Before declaring completion:
- [ ] Entry file named `<MODULE>.md` (uppercase)
- [ ] YAML frontmatter exists
- [ ] All standard sections present
- [ ] `<instructions>` tags included
- [ ] Format matches identity/IDENTITY.md style
- [ ] Integration checker passes (100%)
</instructions>

## Self-Extension Capability

The Digital Brain system can extend itself through AI assistance:

**User**: "I want to create a projects module"

**AI Agent Process**:
1. Opens `MODULE_CREATION_GUIDE.md`
2. Guides through 6-phase workflow
3. Creates all necessary files
4. Updates system integration files
5. Runs `check_module_integration.py`
6. Verifies 100% completion

**Result**: Fully integrated, documented, and tested new module.

## Quick Commands

```bash
# View creation guide
cat module-toolkit/MODULE_CREATION_GUIDE.md

# Create a new module (via AI assistant)
"Create a projects module to track my side projects"

# Check integration after creation
python module-toolkit/check_module_integration.py projects project

# Compare format with existing modules
diff <(head -30 your-module/YOUR-MODULE.md) <(head -30 identity/IDENTITY.md)
```

## Related Documentation

- [Module Creation Guide](./MODULE_CREATION_GUIDE.md) - Complete 6-phase workflow with detailed specifications
- [Example: Module Creation](../examples/module-creation.md) - Step-by-step example walkthrough
- [Content Module](../content/CONTENT.md) - Reference for standard module format
- [Identity Module](../identity/IDENTITY.md) - Reference for standard module format

---

**Last Updated**: 2026-02-28
**Version**: 2.0.0
