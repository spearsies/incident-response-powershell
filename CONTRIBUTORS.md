# Contributors

This project thrives thanks to the contributions of security professionals who believe in open-source incident response tools. We're grateful for everyone who has contributed code, documentation, bug reports, and ideas.

## 🏆 Core Contributors

### Original Author
**[Bert-JanP](https://github.com/Bert-JanP)**  
*Creator of the original Incident Response PowerShell toolkit*

Bert-JanP developed the foundational DFIR scripts and established the modular architecture that makes this toolkit so effective. The original repository can be found at [Bert-JanP/Incident-Response-Powershell](https://github.com/Bert-JanP/Incident-Response-Powershell).

**Key Contributions:**
- Initial DFIR-Script.ps1 implementation
- CSV export functionality for SIEM integration
- Microsoft Defender for Endpoint Live Response integration
- Comprehensive documentation and usage guides
- Blog series on leveraging Live Response for incident response

### Maintainer
**[Stanley Spears](https://github.com/spearsies)**  
*Cybersecurity Professional | Threat Intelligence Analyst*  
🌐 [stanley.spears.org](https://stanley.spears.org)

Maintaining and enhancing this fork with additional features, documentation improvements, and real-world testing in enterprise environments.

**Focus Areas:**
- Documentation enhancement and clarity
- Testing across various Windows environments
- Integration with modern SIEM platforms
- Threat hunting use case development
- Community support and issue resolution

---

## 🤝 How to Become a Contributor

We welcome contributions from security professionals at all skill levels! Here's how you can help:

### Types of Contributions

#### 🔧 Code Contributions
- **New Collection Scripts**: Add artifacts or improve existing collection methods
- **Analysis Modules**: Contribute scripts for analyzing collected data
- **Containment Actions**: Develop safe containment scripts
- **Bug Fixes**: Fix issues identified by the community
- **Performance Improvements**: Optimize script execution time

#### 📚 Documentation Contributions
- **Usage Examples**: Share real-world incident response scenarios
- **Integration Guides**: Document integration with security tools
- **Translations**: Help make documentation accessible globally
- **Video Tutorials**: Create walkthrough videos

#### 🐛 Issue Reporting
- **Bug Reports**: Identify and document issues
- **Feature Requests**: Suggest new capabilities
- **Security Vulnerabilities**: Responsibly disclose security concerns

### Contribution Process

1. **Fork the Repository**
   ```bash
   git clone https://github.com/spearsies/incident-response-powershell.git
   cd incident-response-powershell
   ```

2. **Create a Branch**
   ```bash
   git checkout -b feature/your-contribution
   ```

3. **Make Your Changes**
   - Follow PowerShell best practices
   - Test on Windows 10/11 and Server 2019/2022
   - Add comments for complex logic
   - Update documentation as needed

4. **Submit a Pull Request**
   - Describe your changes clearly
   - Reference related issues
   - Include testing details
   - Sign off on your commits

### Coding Standards

#### PowerShell Style Guide
```powershell
# Use approved verbs for functions
Function Get-ForensicArtifact { }  # ✅ Good
Function Grab-Evidence { }         # ❌ Avoid

# Use PascalCase for function names
Function Invoke-ThreatHunt { }     # ✅ Good
Function invoke_threat_hunt { }    # ❌ Avoid

# Include comment-based help
<#
.SYNOPSIS
    Brief description of function
.DESCRIPTION
    Detailed description
.EXAMPLE
    Example usage
#>

# Use proper parameter attributes
Param(
    [Parameter(Mandatory=$true)]
    [string]$ComputerName,
    
    [Parameter(Mandatory=$false)]
    [int]$DaysBack = 7
)

# Add error handling
try {
    # Your code here
}
catch {
    Write-Error "Operation failed: $_"
}
```

#### Documentation Standards
- **Clear and Concise**: Use simple language
- **Examples**: Provide practical usage examples
- **Testing Notes**: Include testing methodology
- **Security Considerations**: Document any security implications

### Testing Requirements

Before submitting, ensure your code:
- ✅ Runs on Windows 10/11 (latest patches)
- ✅ Runs on Windows Server 2019/2022
- ✅ Works with standard user privileges (where applicable)
- ✅ Works with administrative privileges
- ✅ Handles errors gracefully
- ✅ Exports data in CSV format (for collection scripts)
- ✅ Doesn't contain hardcoded credentials or sensitive data

## 🌟 Hall of Fame

Contributors who have made significant impacts:

| Contributor | Contributions | Area |
|------------|---------------|------|
| [Bert-JanP](https://github.com/Bert-JanP) | Original toolkit architecture, core scripts, documentation | All |
| *Your name here* | *Your contributions* | *Your area* |

## 📋 Contributor Guidelines

### Code of Conduct
- **Be Respectful**: Treat all contributors with respect
- **Be Collaborative**: Work together to solve problems
- **Be Inclusive**: Welcome diverse perspectives
- **Be Professional**: Maintain professionalism in all interactions

### Security Considerations
- **No Credentials**: Never commit API keys, passwords, or tokens
- **Safe Defaults**: Scripts should be safe by default
- **Clear Warnings**: Warn users about potentially destructive actions
- **Responsible Disclosure**: Report security issues privately

### Licensing
By contributing, you agree that your contributions will be licensed under the BSD 3-Clause License, matching the project's license.

## 🎖️ Recognition

Contributors will be:
- Listed in this CONTRIBUTORS.md file
- Mentioned in release notes for their contributions
- Tagged in relevant commits and pull requests
- Credited in documentation they help create

## 📞 Contact

**Project Maintainer**: Stanley Spears  
- GitHub: [@spearsies](https://github.com/spearsies)
- Website: [stanley.spears.org](https://stanley.spears.org)

**Original Author**: Bert-JanP  
- GitHub: [@Bert-JanP](https://github.com/Bert-JanP)
- Blog: [kqlquery.com](https://kqlquery.com)

## 📜 Contribution Statistics

<!-- This section can be automatically updated -->

- **Total Contributors**: 2
- **Total Commits**: 114+
- **Total Stars**: Growing!
- **Total Forks**: 106+ (upstream)

---

## Thank You! 🙏

Every contribution, no matter how small, helps make incident response more effective for security teams worldwide. Your work directly impacts the ability of organizations to detect, respond to, and recover from security incidents.

**Special thanks to:**
- The PowerShell community for creating such a powerful automation platform
- The DFIR community for sharing knowledge and best practices
- Microsoft Defender for Endpoint team for Live Response capabilities
- Everyone who has used these scripts and provided feedback

---

**Want to see your name here?** Start contributing today!

Check out our [open issues](https://github.com/spearsies/incident-response-powershell/issues) or [start a discussion](https://github.com/spearsies/incident-response-powershell/discussions) to get started.
