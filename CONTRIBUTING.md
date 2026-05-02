# Contributing to Tier 1 Support Knowledge Base

Thank you for your interest in contributing. This document outlines the standards and process for adding or modifying articles.

---

## Article Format (Required)

All troubleshooting guides must follow this 5-section structure:

1. **Symptoms** — What the user reports seeing or experiencing
2. **Quick Checks (30 seconds)** — 5 rapid preliminary checks
3. **Step-by-Step Resolution** — 5-7 numbered steps with clear instructions
4. **Root Cause** — 7-9 common causes ordered by likelihood
5. **Escalation Criteria** — Clear triggers for Tier 2 escalation

Each article must also include a **Commands Quick Reference** table at the end.

---

## Style Guide

| Rule | Example |
|------|---------|
| Use bold for UI elements | **Settings** > **Network & Internet** |
| Use backticks for commands | `ipconfig /flushdns` |
| Use bullet lists for symptoms | - Network icon shows yellow triangle |
| Number resolution steps | 1. Go to **Settings** |
| Include OS versions | **Applies To:** Windows 10, Windows 11 |
| Add notes with hyphens | - *This clears any saved network profile corruption.* |
| Write cross-links to related articles | see: [Article Name](./article-name.md) |

---

## Article Template

```markdown
# Article Title

**Category:** [Category Name]
**Last Updated:** [Date]
**Applies To:** Windows 10, Windows 11

---

## Symptoms

- Symptom 1
- Symptom 2
- If related, see: [Related Article](./related-article.md)

---

## Quick Checks (30 seconds)

1. Check 1
2. Check 2
3. Check 3
4. Check 4
5. Check 5

---

## Step-by-Step Resolution

### Step 1: Title
1. Instruction
   - Note or tip

### Step 2: Title
1. Instruction
   - Note or tip

---

## Root Cause

Common causes in order of likelihood:

- Cause 1 (most common)
- Cause 2
- Cause 3

---

## Escalation Criteria

Escalate to Tier 2 if:

- Condition 1
- Condition 2

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| `command` | Description |

---

For internal use. Follow your organization's policies.
