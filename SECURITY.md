# Security Policy

## 🔒 Reporting Security Vulnerabilities

The security of this incident response toolkit is a top priority. If you discover a security vulnerability, we appreciate your help in disclosing it to us responsibly.

### Reporting Process

**Please DO NOT report security vulnerabilities through public GitHub issues.**

Instead, please report security vulnerabilities by:

1. **Email**: Contact the maintainer at the email associated with the [@spearsies](https://github.com/spearsies) GitHub account
2. **Subject Line**: Use "SECURITY: [Brief Description]"
3. **Include**:
   - Description of the vulnerability
   - Steps to reproduce the issue
   - Potential impact assessment
   - Any suggested fixes (if available)

### What to Expect

- **Acknowledgment**: You'll receive a response within 48 hours
- **Assessment**: We'll assess the vulnerability and determine severity
- **Updates**: You'll receive regular updates on our progress
- **Credit**: You'll be credited in the fix (unless you prefer to remain anonymous)

### Response Timeline

- **Critical Vulnerabilities**: Addressed within 7 days
- **High Severity**: Addressed within 14 days
- **Medium/Low Severity**: Addressed within 30 days

## 🛡️ Security Considerations for Users

### Safe Usage Practices

#### When Running Scripts

1. **Review Before Execution**
   - Always review scripts before running them
   - Understand what data will be collected
   - Verify the script source and integrity

2. **Use Appropriate Privileges**
   ```powershell
   # Prefer standard execution when possible
   .\DFIR-Script.ps1
   
   # Only elevate when necessary
   # Right-click PowerShell → "Run as Administrator"
   ```

3. **Test in Non-Production First**
   - Validate scripts in a lab environment
   - Verify output and behavior
   - Check for unintended side effects

#### Data Protection

1. **Collected Artifacts Contain Sensitive Data**
   - Browser history and credentials
   - PowerShell command history
   - Network connection details
   - User account information
   - Security event logs

2. **Secure Storage**
   ```powershell
   # Encrypt collected evidence
   Compress-Archive -Path "DFIR-*" -DestinationPath "Evidence.zip"
   
   # Store in secure location
   # - Encrypted file share
   # - Secure evidence management system
   # - Air-gapped storage for critical incidents
   ```

3. **Secure Transmission**
   - Use encrypted channels (HTTPS, SFTP, encrypted email)
   - Verify recipient identity before sending
   - Delete temporary copies after transmission

4. **Data Retention**
   - Follow your organization's retention policies
   - Securely delete evidence when no longer needed
   - Maintain audit logs of access

### Execution Policy Considerations

```powershell
# Review current execution policy
Get-ExecutionPolicy

# If needed, bypass for this session only
PowerShell.exe -ExecutionPolicy Bypass -File .\DFIR-Script.ps1

# Avoid permanently setting unrestricted policy
# Set-ExecutionPolicy Unrestricted  # ❌ Don't do this
```

### Network Security

When using with Microsoft Defender for Endpoint:
- Ensure Live Response sessions are properly authenticated
- Verify you're connected to the correct tenant
- Review all commands before execution
- Monitor for unauthorized access attempts

## 🔐 Security Features

### Built-In Protections

1. **No Network Transmission**
   - Scripts only collect local data
   - No automatic upload to external services
   - Manual transfer under user control

2. **Read-Only Operations**
   - Collection scripts don't modify system state
   - Containment scripts clearly marked and require confirmation
   - No destructive operations without explicit user action

3. **Minimal Permissions**
   - Most artifacts collectible without admin rights
   - Clear documentation of required privileges
   - Graceful degradation when permissions insufficient

4. **Audit Trail**
   - All collected artifacts timestamped
   - Output paths clearly documented
   - Actions logged when used with Defender for Endpoint

### What This Project Does NOT Do

❌ **Never**:
- Automatically transmit data to external servers
- Modify system configuration without explicit action
- Require internet connectivity for core functionality
- Store credentials in plaintext
- Execute code from untrusted sources
- Bypass security controls silently

## 🔍 Known Limitations

### By Design

1. **Requires Local Execution**
   - Scripts must be run on the target system
   - Cannot collect artifacts remotely (except via Defender Live Response)

2. **Windows-Only**
   - Designed for Windows operating systems
   - PowerShell 5.1+ required

3. **Snapshot in Time**
   - Collects current state only
   - No continuous monitoring
   - Volatile data may be lost if not collected immediately

### Security Considerations

1. **Anti-Malware Detection**
   - Some security tools may flag PowerShell scripts
   - Scripts may trigger behavioral detection
   - Test in your environment and whitelist if appropriate

2. **Privilege Escalation**
   - Scripts don't attempt to elevate privileges
   - Limited artifacts when running without admin rights
   - Users must manually elevate if needed

3. **Evidence Integrity**
   - No cryptographic signing of collected artifacts
   - Users should implement hash verification
   - Consider implementing chain of custody procedures

## 📋 Security Best Practices

### For Repository Maintainers

- ✅ Review all pull requests for security implications
- ✅ Test contributed code in isolated environments
- ✅ Maintain dependencies and update as needed
- ✅ Document security-relevant changes in release notes
- ✅ Respond promptly to security reports

### For Contributors

- ✅ Never commit credentials or API keys
- ✅ Avoid hardcoding file paths or system details
- ✅ Include error handling for all operations
- ✅ Document security implications of new features
- ✅ Test with multiple privilege levels

### For Users

- ✅ Verify script integrity before execution
- ✅ Run in test environment first
- ✅ Secure collected evidence appropriately
- ✅ Follow organizational policies and procedures
- ✅ Document script usage in incident reports

## 🔄 Security Updates

### Staying Informed

- **Watch this Repository**: Click "Watch" → "Custom" → "Security alerts"
- **Check Releases**: Review release notes for security fixes
- **Subscribe to Notifications**: Enable GitHub notifications for security advisories

### Update Recommendations

```powershell
# Check for updates regularly
git fetch origin
git status

# Review changes before pulling
git log origin/main..main

# Update to latest version
git pull origin main
```

## 🎯 Scope

This security policy applies to:
- All scripts in this repository
- Documentation and examples
- Integration guides and tutorials
- Community contributions

This policy does NOT cover:
- Third-party tools referenced in documentation
- User's deployment environments
- Microsoft Defender for Endpoint platform
- SIEM platforms used for data ingestion

## 📚 Additional Resources

### Secure DFIR Practices
- [SANS Digital Forensics Resources](https://www.sans.org/digital-forensics-incident-response/)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [Incident Response Best Practices](https://www.cisa.gov/incident-response)

### PowerShell Security
- [PowerShell Security Best Practices](https://docs.microsoft.com/en-us/powershell/scripting/security/powershell-security)
- [PowerShell Execution Policies](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies)

### Evidence Handling
- [Digital Evidence Handling](https://www.nist.gov/itl/ssd/software-quality-group/computer-forensics-tool-testing-program-cftt)
- [Chain of Custody Procedures](https://www.sans.org/reading-room/whitepapers/legal/paper/33190)

## 📞 Contact

**Security Contact**: Stanley Spears  
- GitHub: [@spearsies](https://github.com/spearsies)
- Website: [stanley.spears.org](https://stanley.spears.org)

**PGP Key**: Available upon request for encrypted communications

---

## 🙏 Acknowledgments

Thank you to everyone who helps keep this project secure:
- Security researchers who responsibly disclose vulnerabilities
- Users who report issues and provide feedback
- Contributors who follow secure coding practices
- The broader infosec community for shared knowledge

---

**Last Updated**: December 2024  
**Version**: 1.0
