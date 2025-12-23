# GitHub Workflows Setup Guide

This guide helps you deploy all GitHub Actions workflows for the Incident Response PowerShell repository.

## 📦 What's Included

### Workflows (5 total)
1. **powershell-test.yml** - PowerShell script validation and testing
2. **security-scan.yml** - Security vulnerability and secret scanning
3. **docs-validation.yml** - Documentation quality checks
4. **ci.yml** - Continuous integration pipeline
5. **release.yml** - Automated release creation

### Issue Templates (3 total)
1. **bug_report.md** - Bug reporting template
2. **feature_request.md** - Feature request template
3. **documentation.md** - Documentation improvement template
4. **config.yml** - Issue template configuration

### Pull Request Template
- **pull_request_template.md** - PR checklist and guidelines

### Configuration Files
1. **.markdownlint.json** - Markdown linting rules
2. **.markdown-link-check.json** - Link validation config
3. **.spellcheck.yml** - Spell checking configuration

## 🚀 Quick Deployment

### Option 1: Upload to GitHub (Web Interface)

1. **Go to your repository**: https://github.com/spearsies/incident-response-powershell

2. **Create `.github/workflows` directory**:
   - Click "Add file" → "Create new file"
   - Type: `.github/workflows/README.md`
   - Paste the content from `workflows/README.md`
   - Commit the file

3. **Upload workflow files**:
   For each workflow file:
   - Click "Add file" → "Create new file"
   - Type: `.github/workflows/[filename].yml`
   - Paste the content
   - Commit

   Files to upload:
   - `powershell-test.yml`
   - `security-scan.yml`
   - `docs-validation.yml`
   - `ci.yml`
   - `release.yml`

4. **Create `.github/ISSUE_TEMPLATE` directory**:
   - Click "Add file" → "Create new file"
   - Type: `.github/ISSUE_TEMPLATE/bug_report.md`
   - Paste content and commit

5. **Upload issue templates**:
   - `bug_report.md`
   - `feature_request.md`
   - `documentation.md`
   - `config.yml`

6. **Upload PR template**:
   - Click "Add file" → "Create new file"
   - Type: `.github/pull_request_template.md`
   - Paste content and commit

7. **Upload configuration files** (repository root):
   - `.markdownlint.json`
   - `.markdown-link-check.json`
   - `.spellcheck.yml`

### Option 2: Using Git (Command Line)

```bash
# Navigate to your repository
cd ~/incident-response-powershell

# Ensure you're on main branch
git checkout main
git pull origin main

# Create directory structure
mkdir -p .github/workflows
mkdir -p .github/ISSUE_TEMPLATE

# Copy all workflow files
cp /path/to/downloaded/.github/workflows/*.yml .github/workflows/
cp /path/to/downloaded/.github/workflows/README.md .github/workflows/

# Copy issue templates
cp /path/to/downloaded/.github/ISSUE_TEMPLATE/*.md .github/ISSUE_TEMPLATE/
cp /path/to/downloaded/.github/ISSUE_TEMPLATE/config.yml .github/ISSUE_TEMPLATE/

# Copy PR template
cp /path/to/downloaded/.github/pull_request_template.md .github/

# Copy configuration files to repository root
cp /path/to/downloaded/.markdownlint.json .
cp /path/to/downloaded/.markdown-link-check.json .
cp /path/to/downloaded/.spellcheck.yml .

# Stage all files
git add .github/
git add .markdownlint.json .markdown-link-check.json .spellcheck.yml

# Commit
git commit -m "ci: Add GitHub Actions workflows and templates

- Add PowerShell testing workflow
- Add security scanning workflow  
- Add documentation validation workflow
- Add CI/CD pipeline workflow
- Add release automation workflow
- Add issue templates (bug, feature, docs)
- Add pull request template
- Add configuration files for linters"

# Push to GitHub
git push origin main
```

## ✅ Post-Deployment Checklist

### Verify Workflows

1. **Go to Actions tab**: https://github.com/spearsies/incident-response-powershell/actions

2. **Check workflow list**:
   - [ ] PowerShell Script Testing
   - [ ] Security Scanning
   - [ ] Documentation Quality
   - [ ] CI/CD Pipeline
   - [ ] Release Automation

3. **Trigger a test run**:
   - Select "PowerShell Script Testing"
   - Click "Run workflow"
   - Select branch: `main`
   - Click "Run workflow"

4. **Verify it runs successfully**:
   - Wait for workflow to complete
   - Check for green checkmark ✅
   - Review logs if any issues

### Verify Templates

1. **Test issue templates**:
   - Go to Issues → "New issue"
   - Verify all templates appear:
     * 🐛 Bug Report
     * ✨ Feature Request
     * 📚 Documentation Improvement

2. **Test PR template**:
   - Create a test branch
   - Make a small change
   - Open a pull request
   - Verify template loads automatically

### Enable Required Features

1. **Enable GitHub Actions** (if not already):
   - Settings → Actions → General
   - Select "Allow all actions and reusable workflows"
   - Click "Save"

2. **Enable CodeQL** (for security scanning):
   - Security → Code security and analysis
   - Enable "CodeQL analysis"

3. **Configure branch protection** (optional but recommended):
   - Settings → Branches
   - Add rule for `main` branch
   - Enable "Require status checks to pass before merging"
   - Select workflows that must pass:
     * PowerShell Script Testing
     * Security Scanning
     * CI/CD Pipeline

## 🔧 Configuration

### Adjust Workflow Triggers

Edit workflow files to change when they run:

```yaml
# Run only on main branch
on:
  push:
    branches: [ main ]

# Run on schedule (daily at 9 AM)
on:
  schedule:
    - cron: '0 9 * * *'

# Run manually only
on:
  workflow_dispatch:
```

### Customize Issue Templates

Edit templates to add/remove fields:

```yaml
---
name: 🐛 Bug Report
about: Report a bug
title: '[BUG] '
labels: ['bug']
assignees: ['spearsies']
---
```

### Adjust Security Scanning

Edit `security-scan.yml` to change:
- Scanning frequency (default: weekly)
- Secret patterns to detect
- Security tools enabled

## 📊 Monitoring Workflows

### View Workflow Status

```bash
# Check workflow runs via GitHub CLI (optional)
gh run list --limit 10

# View specific workflow
gh run view <run-id>

# Download logs
gh run download <run-id>
```

### Add Status Badges to README

Add these to your README.md:

```markdown
## Build Status

![PowerShell Tests](https://github.com/spearsies/incident-response-powershell/actions/workflows/powershell-test.yml/badge.svg)
![Security Scan](https://github.com/spearsies/incident-response-powershell/actions/workflows/security-scan.yml/badge.svg)
![Documentation](https://github.com/spearsies/incident-response-powershell/actions/workflows/docs-validation.yml/badge.svg)
![CI/CD](https://github.com/spearsies/incident-response-powershell/actions/workflows/ci.yml/badge.svg)
```

## 🐛 Troubleshooting

### Workflow doesn't trigger

**Check**:
1. Actions are enabled (Settings → Actions)
2. File is in correct location (`.github/workflows/`)
3. YAML syntax is valid
4. Trigger conditions match (e.g., correct branch)

### Workflow fails immediately

**Common causes**:
1. YAML syntax error
2. Invalid action version
3. Missing permissions

**Solution**:
- Check workflow logs
- Validate YAML: https://www.yamllint.com/
- Review GitHub Actions documentation

### Security scan finds false positives

**Solution**:
1. Review the findings
2. If legitimate, add to ignore list
3. Update `.markdown-link-check.json` or workflow file

## 🔐 Security Best Practices

### Required Secrets

Some workflows may need secrets configured:

1. Go to Settings → Secrets and variables → Actions
2. Add repository secrets:
   - `GITHUB_TOKEN` (automatically provided)
   - Add others as needed for specific integrations

### Permissions

Workflows use minimal permissions:
- `contents: read` for most workflows
- `contents: write` only for releases
- `security-events: write` for CodeQL

## 📈 Next Steps

After deploying workflows:

1. **Create your first release**:
   ```bash
   git tag -a v2.1.0 -m "Add workflows and documentation"
   git push origin v2.1.0
   ```

2. **Test all workflows**:
   - Make a test commit
   - Open a test PR
   - Watch workflows run

3. **Configure branch protection**:
   - Require workflow checks before merge
   - Prevent force pushes to main

4. **Monitor workflow runs**:
   - Check Actions tab regularly
   - Fix any failing workflows promptly

5. **Iterate and improve**:
   - Add more tests as needed
   - Customize workflows for your needs
   - Update based on feedback

## 📚 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Workflow Syntax Reference](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
- [PSScriptAnalyzer Rules](https://github.com/PowerShell/PSScriptAnalyzer/tree/master/RuleDocumentation)
- [CodeQL Documentation](https://codeql.github.com/docs/)

## 📞 Support

Issues with workflows?
1. Check workflow logs
2. Review this documentation
3. Search GitHub Actions community
4. Open an issue in the repository

---

**Created**: December 2024  
**Last Updated**: December 2024  
**Maintainer**: [@spearsies](https://github.com/spearsies)

🎉 **You're all set! Your repository now has professional CI/CD workflows!**
