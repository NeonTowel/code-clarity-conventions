**📚 Documentation Conventions: Code Clarity à la Conventional Commits**  
*Because readable docs > cryptic scrolls.*

## 🚀 **Core Principles**

1. **Brevity** ≠ **vagueness** – say *enough*, not *everything*.
2. **Structure** like git commits – scoped, purposeful, consistent.
3. **Why > What** – document intent, not just mechanics.

## 📦 **Per-Language Rules**

### **Go** (`//` comments)

- **Package File Headers**: Clarify intent at a glance:

  ```go
  // Package cache implements TTL-based object storage
  // [Scope: DATA] [Status: Experimental]
  // Uses SHA-256 for key derivation
  package cache
  ```

  - First Line: Briefly state package purpose.
  - Metadata Tags (optional but useful): Scope, stability, owner.
  - Extended Context: Keep it under three lines.

- **Functions/Structs**: One-liner describing *role*:
  
  ```go
  // CacheUser stores session data with TTL expiry
  // WHY: Avoid DB hits on frequent profile reads  
  func CacheUser(u User) error { ... }  
  ```

- **Interfaces**: Treat like API contracts:
  
  ```go
  // Notifier sends alerts to external systems
  // Implementors: SlackNotifier, EmailNotifier  
  type Notifier interface { Notify(msg string) }  
  ```

### **Scripts/Automation** (`#` comments)

- **Header Block** (top of file):
  
  ```python
  # SCOPE: data-pipeline
  # SYNOPSIS: Transforms CSV → Parquet  
  # RISK: High (modifies prod S3 buckets)
  # SAFETY: Dry-run with --simulate  
  ```

- **Error Guidance**: Tag failures with fixes:
  
  ```bash
  # ERROR: FileNotFound → FIX: Run 'download_deps.sh' first  
  ```

### **IaC (Bicep, Terraform, CloudFormation)**

- **Resource Intent**:
  
  ```bicep
  // PURPOSE: Securely store app secrets
  // SECURITY: Uses Key Vault with RBAC access
  resource kv 'Microsoft.KeyVault/vaults@2022-07-01' = {
    name: 'app-secrets'
    properties: {
      sku: { name: 'standard' }
    }
  }
  ```
  
  ```hcl
  # PURPOSE: Isolate payment processing
  # SECURITY: Restrict ingress to /24 CIDR 
  resource "aws_security_group" "payments" { ... }  
  ```

### **Frontend (Svelte, TypeScript)**

- **Component Purpose**:
  
  ```svelte
  <!-- PURPOSE: Displays user avatar with fallback -->
  <!-- UX: Uses initials if no profile picture -->
  <script>
    export let user;
    let avatar = user.photo || `https://fallback.com/${user.initials}`;
  </script>
  
  <img src={avatar} alt="User Avatar" />
  ```

- **Function Intent**:
  
  ```typescript
  // PURPOSE: Format currency display
  // WHY: Ensures locale-specific formatting  
  export function formatCurrency(amount: number, locale = 'en-US') {
    return new Intl.NumberFormat(locale, { style: 'currency', currency: 'USD' }).format(amount);
  }
  ```

### **Taskfiles (go-task)**

- **Task Purpose**:
  
  ```yaml
  # PURPOSE: Deploys infra with Bicep
  # DEPENDS ON: Azure CLI logged in
  version: '3'
  tasks:
    deploy:
      desc: "Deploy Azure resources with Bicep"
      cmds:
        - az deployment group create --resource-group MyRG --template-file main.bicep
  ```

## 🔗 **Syncing with Git Commits**

Enhance Conventional Commits (see below) with doc impact tags:

```yaml
docs(api): add rate limit examples #doc-impact  
- Added 3 code samples to /docs/api.md  
- WHY: Support ticket #42 cited confusion  
```

*Use `#doc-impact`* to flag changes needing doc updates.

## 🤔 **Why Bother?**

- **Onboard faster** – docs explain *system quirks*, not just syntax.
- **Reduce "Why?" PR comments** – intent is self-documented.
- **Greppable** – search for `// WHY:` or `# RISK` to triage issues.

**🛠 Pro Tip**: Start with *one convention* (e.g., `WHY` comments) – scale as your team goes "Oh, *this* is genius!" 🚀

---

## **Git Commits Style**

**📝 Conventional Commits: Git Commits That Don’t Make Teammates Sigh**  
*Because “Fixed stuff” commits belong in cringe compilations.*

### 🎯 **Core Principles**

1. **Type + Scope** – What *changed* and *where*?
2. **Subject ≤ 50 chars** – Twitter-style, not Tolstoy.
3. **Body Explains *Why*** – Context > minutiae.

### 🚦 **Commit Types (The MVPs)**

| Type    | When to Use                         | Example                          |
| ------- | ----------------------------------- | -------------------------------- |
| `feat`  | New behavior (user-facing) 🎉       | `feat(auth): add SMS 2FA`        |
| `fix`   | Bug squash 🐞→💥                    | `fix(login): timeout on iOS 17`  |
| `docs`  | READMEs, comments, guides 📚        | `docs(api): deprecate /v1/users` |
| `chore` | Grunt work (CI, deps, refactors) 🛠 | `chore(deps): bump React to 19`  |

### 💥 **Breaking Changes**

Flag backward-incompatible changes with `!` and `BREAKING CHANGE:`:

```text
feat(db)!: drop PostgreSQL 11 support   
BREAKING CHANGE: Requires PG ≥ 13.2  
```

### 🛠 **Pro Tip**

Use **commitlint** + **husky** to auto-enforce rules – because willpower is for gyms, not git.

**🌱 Why It Works**:

- `git log --grep=feat` → Instantly find features.
- Release notes write themselves.
- No more “WTF was this commit?” archaeology.

*“Write commits like your future self is debugging prod at 3am.”* 🔍☕

---

*"Documentation is a love letter you write to your future self."* – Some dev who avoided a 3am outage. 🌌
