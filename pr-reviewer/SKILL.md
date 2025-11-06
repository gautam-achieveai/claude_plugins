---
name: pr-reviewer
description: Conduct code reviews of individual pull requests analyzing security (OWASP Top 10), performance, testing coverage, and code quality. Provides structured feedback with file:line references and code examples. Use when asked to "review PR #[number]", "code review pull request", "check PR for issues", or "analyze PR changes". Works with PR numbers, branch names, or Azure DevOps URLs. NOT for developer performance reviews over time.
allowed-tools: Read, Grep, Glob, Bash, WebFetch, mcp__azure-devops__*
---

# Pull Request Code Reviewer

Review individual PRs for code quality, security (OWASP Top 10), performance, and testing adequacy.

## ⚠️ Skill Scope

**This skill is for:**

- Reviewing individual pull requests
- Code review with security, performance, testing analysis
- Providing structured feedback on specific PR changes

**Examples:**

- "Review PR #12345" → Use **pr-reviewer** ✅
- "Code review this pull request" → Use **pr-reviewer** ✅

## Quick Start

**LLM Workflow:**

1. Fetch PR data using MCP:

```
mcp__azure-devops__getPullRequest -repository "MCQdbDEV" -pullRequestId 12345
```

2. Extract source branch from response (e.g., `sourceRefName: "refs/heads/developers/gb/feature"`)

3. Call `pwsh` script with parameters:

```pwsh
<PATH_FOR_PR-REVIEWER_SKILL_ROOT_DIRECTORY>\scripts\Start-PRReview.ps1 `
    -PRNumber 12345 `
    -SourceBranch "developers/gb/feature" `
    -PRTitle "Add bulk upload feature" `
    -PRAuthor "Gautam Bhakar"
```

Creates isolated worktree with analysis templates.

## Essential Workflow

1. **Fetch PR Metadata** (LLM uses MCP)
   - Call `mcp__azure-devops__getPullRequest` to get PR details
   - Extract: sourceRefName, title, author, description

2. **Setup** (automated via script)
   - Create worktree at `worktrees/pr-[number]-review/`
   - Fetch source branch and create isolated checkout
   - Set up review templates

3. **Analyze Code**
   - **Security**: Check OWASP Top 10 vulnerabilities
   - **Performance**: Identify N+1 queries, memory leaks, algorithm efficiency
   - **Code Quality**: Review SOLID principles, code smells, anti-patterns
   - **Testing**: Assess coverage, quality, missing scenarios

4. **Document Findings**
   - Fill templates in `scratchpad/pr_reviews/pr-[number]/analysis/`
   - Use specific file:line references
   - Include code examples (current vs recommended)

5. **Provide Feedback**
   - Create consolidated feedback in `feedback/pr_feedback.md`
   - Structure: Summary → Strengths → Issues → Recommendations
   - Post comments via Azure DevOps MCP tools (optional)

## Critical Principles

**1. Be Specific and Actionable**

- ❌ "This code has issues"
- ✅ "Line 45: Missing null check for `user` parameter can cause NullReferenceException when called from endpoint X"

**2. Include Code Examples**

- Show current problematic code
- Explain why it's problematic
- Show recommended fix

**3. Reference Exact Locations**

- Format: `path/to/file.cs:123` or `UserService.cs:45-67`

**4. Balance Feedback**

- Start with what's done well
- Then address concerns constructively
- End with clear action items

**5. Consider Context**

- PR complexity and scope
- Author experience level
- Business priorities

## Quick Reference Checklist

- [ ] Security: OWASP Top 10 checked
- [ ] Performance: N+1 queries, memory leaks, algorithm efficiency
- [ ] Code Quality: SOLID, code smells, duplication
- [ ] Testing: Coverage, edge cases, integration tests
- [ ] Specific feedback with file:line references
- [ ] Code examples for issues and fixes
- [ ] Balanced positive and constructive feedback

## Detailed Guides

For comprehensive checklists and examples:

- [Security Checklist (OWASP Top 10)](reference/security-checklist.md)
- [Performance Review Guide](reference/performance-guide.md)
- [Code Quality Guide](reference/code-quality-guide.md)
- [Testing Assessment Guide](reference/testing-guide.md)
- [Scripts Documentation](scripts/README.md)

## Integration with Tools

**Azure DevOps MCP:**

- `mcp__azure-devops__getPullRequest` - Fetch PR details
- `mcp__azure-devops__getAllPullRequestChanges` - Get file changes
- `mcp__azure-devops__addPullRequestComment` - Add general comment
- `mcp__azure-devops__addPullRequestInlineComment` - Add line-specific comment
- `mcp__azure-devops__approvePullRequest` - Approve PR

## Output Format

Provide structured feedback:

```markdown
# PR Review: [Title]

## Summary
Overall assessment, files changed, risk level

## Strengths
What was done well (with file:line references)

## Critical Issues (Must Fix)
Blocking issues with code examples

## Important Issues (Should Fix)
Code quality, performance concerns

## Testing Assessment
Coverage gaps, suggested tests

## Security Review
OWASP issues found (if any)

## Recommendations
Specific, actionable improvements
```

## Remember

**Goal:** Catch bugs before production, improve code quality, share knowledge, maintain standards

**Focus on:**

1. **Correctness** (bugs, security)
2. **Maintainability** (future developers)
3. **Performance** (user experience)
4. **Testing** (confidence in changes)

Be thorough but pragmatic. **Be specific, actionable, balanced, and professional.**

---

**Version:** 1.1.0 (2025-11-02) - Optimized for context efficiency with progressive disclosure
