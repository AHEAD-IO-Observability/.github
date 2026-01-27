# AHEAD Tanium Projects - AI Assistant Requirements

## 🚨 MANDATORY POLICY: All AI Assistants

**This policy applies to ALL AI assistants working on Tanium projects within AHEAD-IO-Observability.**

### Required for ALL Tanium Work:

1. ✅ **Clone Repository**: https://github.com/AHEAD-IO-Observability/tanium-docs-rag
2. ✅ **Search FIRST**: Run `python src/rag_search.py "your query"` before providing answers
3. ✅ **Read Rules**: Review `.github/copilot-instructions.md` in the RAG repository (116 lines)
4. ✅ **Cite Sources**: All Tanium facts MUST include documentation URLs
5. ✅ **Acknowledge Gaps**: If documentation doesn't contain information, state this explicitly

### Why This Matters

Without consulting the RAG system, AI assistants hallucinate dangerous information:

- ❌ **Fake default group names** - Assuming "All Servers" or "All Workstations" exist when they may not
- ❌ **Non-existent permissions** - Providing incomplete permission lists as if they're complete
- ❌ **Invalid configuration patterns** - Assuming naming conventions (e.g., "servers start with SRV")
- ❌ **Imaginary API endpoints** - Creating example endpoints that don't exist
- ❌ **Made-up default values** - Inventing configuration values not in documentation

### Real Examples of Hallucination Damage

**Bad Answer (Without RAG):**
> "Create computer groups using `Computer Name starts with 'SRV'` for servers..."

**Why Dangerous:** Customer's servers don't follow this pattern → RBAC fails → Security breach

**Good Answer (With RAG):**
> "According to [help.tanium.com/console_rbac_overview.html], computer groups can use filters. The documentation doesn't specify default naming patterns. Check Administration > Permissions > Computer Groups in your Tanium console for your organization's existing groups."

### Enforcement Mechanism

**How This Is Enforced:**

- **GitHub Copilot**: Automatically reads `.github/copilot-instructions.md` in RAG repo
- **Pull Requests**: Automated validation checks for RAG evidence (Phase 4B)
- **Code Reviews**: Reviewers verify RAG consultation before approval
- **Repository Badges**: All Tanium repos display mandatory notice at top of README

**Consequences of Non-Compliance:**

- ❌ Pull requests without RAG evidence will be **BLOCKED**
- ❌ AI-generated code without source citations will be **REJECTED**
- ❌ Contributions that contradict documentation will be **REVERTED**

### How to Comply

#### For AI Assistants (GitHub Copilot, Claude, ChatGPT, etc.)

**BEFORE answering ANY Tanium question:**

```bash
# 1. Clone RAG repository (one-time setup)
git clone https://github.com/AHEAD-IO-Observability/tanium-docs-rag.git

# 2. Search for relevant information (3-5 queries for complex topics)
cd tanium-docs-rag
python src/rag_search.py "RBAC roles configuration"
python src/rag_search.py "computer groups permissions"
python src/rag_search.py "deny roles example"

# 3. Use results to answer, citing URLs
# 4. If no relevant docs found, say "Documentation doesn't cover this"
```

#### For Human Developers

**When submitting PRs with Tanium-related changes:**

```markdown
## RAG Consultation Evidence

- Searched: `python src/rag_search.py "Tanium Connect configuration"`
- Searched: `python src/rag_search.py "Connect API authentication"`
- Sources: 
  - https://help.tanium.com/bundle/ug_connect_cloud/page/connect/overview.html
  - https://developer.tanium.com/site/global/apis/rest/index.gsp

## Changes Made

[Describe changes, referencing documentation]
```

### Documentation Coverage

The RAG system contains:

- **293 documentation pages**
  - 206 pages from help.tanium.com (product documentation)
  - 87 pages from developer.tanium.com (API/SDK documentation)
- **9,762 embedded chunks** for semantic search
- **100% citation rate** in RBAC testing (25 questions)
- **Automatic updates** every Monday at 2 AM UTC

### Quick Reference

| Resource | Purpose | URL |
|----------|---------|-----|
| **RAG Repository** | Source of truth | https://github.com/AHEAD-IO-Observability/tanium-docs-rag |
| **Copilot Instructions** | Anti-hallucination rules | [.github/copilot-instructions.md](https://github.com/AHEAD-IO-Observability/tanium-docs-rag/blob/main/.github/copilot-instructions.md) |
| **Search Tool** | Query documentation | `python src/rag_search.py "query"` |
| **Documentation Schedule** | Auto-update timing | Every Monday 2 AM UTC |

### Verification

To verify a repository has enforcement active:

1. Visit the repository on GitHub
2. Look for 🚨 **AI Assistant Policy** notice at top of README
3. Verify notice links to this organization policy
4. Check for `.github/workflows/ai-rag-validation.yml` (automated checks)

### Support

- **Questions about this policy:** Open issue in [tanium-docs-rag](https://github.com/AHEAD-IO-Observability/tanium-docs-rag/issues)
- **Report hallucinations:** Document in issue with "hallucination" label
- **Request documentation updates:** Tag issue with "documentation" label

---

**Policy Version:** 1.0  
**Last Updated:** January 26, 2026  
**Applies To:** All AHEAD-IO-Observability Tanium repositories  
**Enforcement Level:** Mandatory - No exceptions without explicit approval
