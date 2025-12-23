# GitHub Actions Workflows

This directory contains automated workflows for the Incident Response PowerShell repository. These workflows ensure code quality, security, and streamlined development processes.

## 📋 Available Workflows

### 1. PowerShell Script Testing (`powershell-test.yml`)
**Trigger**: Push/PR to main or develop branches (when .ps1 files change)

**Purpose**: Validates PowerShell scripts for syntax errors and code quality issues

**What it does**:
- Installs PSScriptAnalyzer (PowerShell linting tool)
- Runs PSScriptAnalyzer on all .ps1 files
- Checks syntax validity
- Tests compatibility on Windows Server 2019 and 2022
- Fails build if critical errors found

**When to use manually**: Click "Actions" → "PowerShell Script Testing" → "Run workflow"

---

### 2. Security Scanning (`security-scan.yml`)
**Trigger**: Push/PR to main or develop, weekly schedule (Mondays at 9 AM UTC)

**Purpose**: Scans for security vulnerabilities, secrets, and malware

**What it does**:
- **TruffleHog**: Scans for hardcoded secrets and credentials
- **CodeQL**: Performs static security analysis
- **ClamAV**: Scans for malware
- **Secret Detection**: Checks for API keys, passwords, tokens
- **Security Policy Check**: Validates SECURITY.md exists
- **License Compliance**: Verifies LICENSE file
- **PowerShell Security**: Checks for dangerous cmdlets

**When to use manually**: Before releases or after major changes

---

### 3. Documentation Quality (`docs-validation.yml`)
**Trigger**: Push/PR when .md files change

**Purpose**: Ensures documentation quality and completeness

**What it does**:
- **Markdown Linting**: Validates markdown syntax
- **Link Checking**: Verifies all links work
- **Structure Validation**: Ensures required docs exist
- **Spell Checking**: Catches typos (non-blocking)
- **Code Block Validation**: Checks formatting
- **Documentation Metrics**: Generates statistics

**When to use manually**: After documentation updates

---

### 4. CI/CD Pipeline (`ci.yml`)
**Trigger**: Push/PR to main or develop

**Purpose**: Continuous integration and quality assurance

**What it does**:
- **Code Quality**: Runs PSScriptAnalyzer
- **Build Test**: Tests on multiple Windows versions
- **Integration Test**: Validates DFIR-Script.ps1
- **Performance Test**: Measures parse times
- **Generate Report**: Creates build summary
- **Update Badges**: Updates README badges (main branch only)

**When to use manually**: For comprehensive pre-release testing

---

### 5. Release Automation (`release.yml`)
**Trigger**: Push tags matching `v*.*.*` pattern (e.g., v2.5.0)

**Purpose**: Automates release creation and packaging

**What it does**:
- **Generate Changelog**: Creates automatic changelog from commits
- **Create Release**: Publishes GitHub release
- **Package Scripts**: Creates distribution ZIP
- **Upload Assets**: Attaches files to release
- **Notify**: Generates release summary

**How to trigger**:
```bash
# Create and push a tag
git tag -a v2.5.0 -m "Release version 2.5.0"
git push origin v2.5.0
```

Or use workflow_dispatch from Actions tab.

---

## 🎯 Workflow Status Badges

Add these badges to your README.md to show workflow status:

```markdown
![PowerShell Tests](https://github.com/spearsies/incident-response-powershell/actions/workflows/powershell-test.yml/badge.svg)
![Security Scan](https://github.com/spearsies/incident-response-powershell/actions/workflows/security-scan.yml/badge.svg)
![Documentation](https://github.com/spearsies/incident-response-powershell/actions/workflows/docs-validation.yml/badge.svg)
![CI/CD](https://github.com/spearsies/incident-response-powershell/actions/workflows/ci.yml/badge.svg)
```

## 🔧 Configuration Files

### `.markdownlint.json`
Configures markdown linting rules:
- ATX-style headers (`#` instead of underlines)
- Dash-style lists (`-` instead of `*`)
- No line length limits (MD013 disabled)
- Allows HTML tags (MD033 disabled)

### `.markdown-link-check.json`
Configures link checking:
- 20-second timeout per link
- 3 retry attempts
- Ignores localhost URLs
- Handles GitHub rate limiting

### `.spellcheck.yml`
Configures spell checking:
- Checks all `.md` files
- Ignores code blocks and pre-formatted text
- Uses English dictionary

## 🚀 Best Practices

### Before Committing
1. **Run locally if possible**:
   ```powershell
   # Install PSScriptAnalyzer
   Install-Module -Name PSScriptAnalyzer -Force
   
   # Run analysis
   Invoke-ScriptAnalyzer -Path . -Recurse
   ```

2. **Check for secrets**:
   ```bash
   # Search for common secret patterns
   grep -r "password\s*=" .
   grep -r "api_key\s*=" .
   ```

3. **Validate markdown**:
   - Use VS Code with markdownlint extension
   - Preview files before committing

### During Pull Requests
1. Wait for all CI checks to pass
2. Review security scan results
3. Fix any PSScriptAnalyzer warnings
4. Update documentation if needed

### Before Releases
1. Run security scan manually
2. Verify all tests pass
3. Update ROADMAP.md with completed items
4. Update version numbers
5. Create release tag

## 📊 Workflow Triggers Summary

| Workflow | Push (main) | Push (develop) | PR | Schedule | Manual |
|----------|-------------|----------------|-----|----------|--------|
| PowerShell Test | ✅ (.ps1) | ✅ (.ps1) | ✅ | ❌ | ✅ |
| Security Scan | ✅ | ✅ | ✅ | ✅ (Weekly) | ✅ |
| Docs Validation | ✅ (.md) | ✅ (.md) | ✅ | ❌ | ✅ |
| CI/CD | ✅ | ✅ | ✅ | ❌ | ✅ |
| Release | ✅ (tags only) | ❌ | ❌ | ❌ | ✅ |

## 🛠️ Troubleshooting

### Workflow Failed - PSScriptAnalyzer Errors
**Solution**: 
```powershell
# Fix the specific issues mentioned in the log
# Common fixes:
# - Add proper parameter validation
# - Use approved verbs (Get-, Set-, etc.)
# - Add comment-based help
```

### Workflow Failed - Security Scan
**Solution**:
- Review the detected secrets
- Remove any hardcoded credentials
- Use environment variables or secure vaults instead

### Workflow Failed - Link Check
**Solution**:
- Fix broken links in markdown files
- Update URLs that have changed
- Add to ignore list in `.markdown-link-check.json` if intentional

### Workflow Stuck or Slow
**Possible causes**:
- GitHub Actions queue is busy
- Large file uploads taking time
- External dependencies timing out

**Solution**: Wait or re-run the workflow

## 🔐 Security Considerations

### Secrets Management
- Never commit secrets to the repository
- Use GitHub Secrets for sensitive data
- Access secrets in workflows via `${{ secrets.SECRET_NAME }}`

### Permissions
Workflows have minimal permissions by default:
- `contents: read` - Read repository contents
- `contents: write` - Only for release workflow
- `security-events: write` - Only for CodeQL

### Third-Party Actions
All actions are from trusted sources:
- `actions/*` - Official GitHub actions
- `github/*` - Official GitHub actions
- `trufflesecurity/*` - Verified security tool

## 📈 Monitoring

### View Workflow Runs
1. Go to repository → "Actions" tab
2. Select specific workflow
3. Click on a run to see details
4. View logs for each step

### Artifacts
Some workflows generate artifacts:
- `pssa-results` - PSScriptAnalyzer output
- `docs-report` - Documentation statistics
- `ci-report` - CI build report
- `distribution-package` - Release packages

**Download artifacts**:
1. Go to workflow run
2. Scroll to "Artifacts" section
3. Click to download

## 🎓 Learning Resources

### GitHub Actions
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Workflow syntax](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)

### PowerShell Testing
- [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer)
- [Pester Testing Framework](https://pester.dev/)

### Security Tools
- [TruffleHog](https://github.com/trufflesecurity/trufflehog)
- [CodeQL](https://codeql.github.com/)
- [ClamAV](https://www.clamav.net/)

---

## 📞 Support

If you encounter issues with workflows:

1. **Check workflow logs** for specific error messages
2. **Search existing issues** in the repository
3. **Open a new issue** using the bug report template
4. **Contact maintainer** [@spearsies](https://github.com/spearsies)

---

**Last Updated**: December 2024  
**Maintained by**: [@spearsies](https://github.com/spearsies)
