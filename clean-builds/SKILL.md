---
name: clean-builds
description: This skill guides developers through achieving zero-warning builds, consistent code style, and NuGet package version consistency. It provides a comprehensive workflow combining Roslynator analyzer integration (200+ code analyzers), code formatting (format-code.ps1), build quality checks (build_and_group_errors_and_warnings.ps1), and package version validation (validate-package-versions.ps1). This skill should be used when preparing code for commit, validating build quality, fixing code style issues, ensuring all warnings are addressed, or consolidating package versions before merging.
---

# Clean Builds Skill

## Purpose

This skill enables developers to achieve **zero-warning builds**, **consistent code style**, and **NuGet package version consistency** through a proven three-step workflow:

1. **Format Code** - Automatically fix code style and apply code analysis
2. **Build & Check** - Verify the build is clean with no errors or warnings
3. **Validate Packages** - Ensure NuGet package versions are consistent across projects

Use this skill to:
- Prepare code for commit with confidence
- Fix all build warnings and errors systematically
- Maintain consistent code style across the project
- Identify and fix NuGet package version inconsistencies
- Validate quality before merging pull requests

## When to Use This Skill

Invoke this skill when you need to:
- Format and validate code changes before committing
- Fix build warnings that are blocking progress
- Check for NuGet package version inconsistencies
- Perform comprehensive pre-commit quality checks
- Achieve zero-warning builds for release preparation

## Quick Start

### Prerequisites (One-Time Setup)

Before first use, complete the one-time setup:

```pwsh
# Step 1: Enable code style enforcement
pwsh <clean_builds_skill_base_dir>/scripts/validate-code-style-enforcement.ps1 -Enforce

# Step 2: Enable Roslynator analyzers
pwsh <clean_builds_skill_base_dir>/scripts/enable-roslynator-analyzers.ps1 -ExcludeSubmodules

# Step 3: Configure .editorconfig
pwsh <clean_builds_skill_base_dir>/scripts/configure-roslynator-editorconfig.ps1 -Severity warning

# Step 4: Validate package versions
pwsh <clean_builds_skill_base_dir>/scripts/validate-package-versions.ps1
```

**📖 Detailed Guide**: [One-Time Setup Guide](references/one-time-setup-guide.md)

### Regular Workflow

Execute before every commit:

```pwsh
# 1. Validate packages
pwsh <clean_builds_skill_base_dir>/scripts/validate-package-versions.ps1

# 2. Format code
pwsh <clean_builds_skill_base_dir>/scripts/format-code.ps1

# 3. Build and check
pwsh <clean_builds_skill_base_dir>/scripts/build_and_group_errors_and_warnings.ps1

# 4. Fix warnings (if any)
# 5. Repeat 2-3 until clean
```

**📖 Detailed Guide**: [Complete Workflow Example](examples/complete-workflow.md)

## Available Scripts

| Script | Purpose | Documentation |
|--------|---------|---------------|
| `validate-package-versions.ps1` | Detect NuGet version mismatches | [→ Details](references/scripts/validate-package-versions.md) |
| `format-code.ps1` | Auto-fix code style issues | [→ Details](references/scripts/format-code.md) |
| `build_and_group_errors_and_warnings.ps1` | Build & group warnings by code | [→ Details](references/scripts/build-and-group-errors.md) |
| `enable-roslynator-analyzers.ps1` | Add Roslynator to all projects | [→ Details](references/scripts/enable-roslynator-analyzers.md) |
| `configure-roslynator-editorconfig.ps1` | Configure .editorconfig rules | [→ Details](references/scripts/configure-roslynator-editorconfig.md) |
| `validate-code-style-enforcement.ps1` | Enable code style during build | [→ Details](references/scripts/validate-code-style-enforcement.md) |

## Handling Issues

### Build Warnings

Warnings are grouped by code for efficient batch fixing.

**Common warnings**:
- **IDE0005**: Unused imports → Auto-fixed by `format-code.ps1`
- **CA1826**: Use property instead of LINQ → Manual fix required
- **CA1859**: Use concrete types → Manual or auto-fix
- **RCS1036**: Remove blank lines → Auto-fixed by Roslynator

**📖 Detailed Guide**: [Warning Codes Guide](references/warning-codes-guide.md)

### Package Version Issues

**🔴 CRITICAL** (must fix immediately):
- Orleans framework version mismatches
- Major version differences

**🟡 WARNING** (should review):
- Minor/patch version variations

**📖 Detailed Guide**: [Package Version Management](references/package-version-management.md)

### Troubleshooting

Common issues and solutions:

- **Tool not found** → Install missing tools
- **IDE0005 not detected** → Enable `EnforceCodeStyleInBuild`
- **Too many Roslynator warnings** → Start with lower severity
- **Build time increased** → Exclude submodules from analysis

**📖 Detailed Guide**: [Troubleshooting Guide](references/troubleshooting.md)

## Best Practices

**Core Principles**:

1. ✅ **Complete one-time setup first** - Configure all tools before using
2. ✅ **Format frequently** - Don't accumulate style issues
3. ✅ **Fix warnings immediately** - Don't let them pile up
4. ✅ **Never suppress warnings** - Fix root causes, not symptoms
5. ✅ **Understand each warning** - Learn from the messages
6. ✅ **Validate packages regularly** - Catch version drift early
7. ✅ **Pre-commit validation** - Always run full workflow before commit
8. ✅ **Enable Roslynator** - Get 200+ code quality rules
9. ✅ **Team consistency** - Commit .editorconfig and .csproj changes

**📖 Detailed Guide**: [Best Practices](references/best-practices.md)

## Roslynator Analyzers (Optional but Recommended)

Roslynator provides 200+ code analyzers that run during every build.

**Benefits**:
- 🎯 Build-time enforcement of code quality
- 💡 Real-time IDE feedback
- 📋 Consistent team standards
- ⚡ Catch issues early

**Setup** (one-time):

```pwsh
# Add analyzers
pwsh <clean_builds_skill_base_dir>/scripts/enable-roslynator-analyzers.ps1 -ExcludeSubmodules

# Configure severity
pwsh <clean_builds_skill_base_dir>/scripts/configure-roslynator-editorconfig.ps1 -Severity warning

# Auto-fix issues
roslynator fix DOC_Project_2025.sln --ignore-compiler-errors --format
```

**Expected impact**:
- Build time: +10-30%
- Initial warnings: 100s
- Auto-fixable: 200-300+

**📖 Detailed Guide**: [Roslynator Setup Guide](references/roslynator-setup.md)

## Examples

- **[Complete Workflow](examples/complete-workflow.md)** - Full workflow from start to commit
- **[First-Time Setup](examples/first-time-setup.md)** - Initial configuration walkthrough
- **[Fixing Warnings in Bulk](examples/fixing-warnings-bulk.md)** - Batch fixing strategies
- **[Package Version Fixes](examples/package-version-fixes.md)** - Step-by-step package fixes
- **[Roslynator Auto-Fix](examples/roslynator-auto-fix.md)** - Using `roslynator fix` command

## References

- **[One-Time Setup Guide](references/one-time-setup-guide.md)** - Complete setup checklist
- **[Warning Codes Guide](references/warning-codes-guide.md)** - Detailed warning explanations
- **[Package Version Management](references/package-version-management.md)** - NuGet version guide
- **[Roslynator Setup](references/roslynator-setup.md)** - Comprehensive Roslynator guide
- **[Best Practices](references/best-practices.md)** - Zero-warning build strategies
- **[Troubleshooting](references/troubleshooting.md)** - Common issues and solutions

### Script Documentation

- **[format-code.ps1](references/scripts/format-code.md)** - Code formatting
- **[build_and_group_errors_and_warnings.ps1](references/scripts/build-and-group-errors.md)** - Build validation
- **[validate-package-versions.ps1](references/scripts/validate-package-versions.md)** - Package validation
- **[enable-roslynator-analyzers.ps1](references/scripts/enable-roslynator-analyzers.md)** - Enable analyzers
- **[configure-roslynator-editorconfig.ps1](references/scripts/configure-roslynator-editorconfig.md)** - Configure rules
- **[validate-code-style-enforcement.ps1](references/scripts/validate-code-style-enforcement.md)** - Style enforcement

## Next Steps

After achieving a clean build:

1. Review changes: `git diff`
2. Commit your changes
3. Create a pull request
4. Ensure CI/CD pipeline passes

**Remember**: Zero warnings before commit is the goal!
