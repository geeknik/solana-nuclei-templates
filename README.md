# Solana Security Nuclei Templates

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Nuclei](https://img.shields.io/badge/nuclei-v3.3.10-green.svg)
![Solana](https://img.shields.io/badge/solana-v1.18.x-purple.svg)

A comprehensive collection of Nuclei templates designed to detect common security vulnerabilities in Solana smart contracts.

## Overview

This repository contains 25 specialized Nuclei templates that scan Solana Rust code for potential security flaws and vulnerabilities. These templates implement detection patterns based on the security best practices documented by the SlowMist team and common vulnerabilities found in real-world Solana exploits.

## What is Nuclei?

[Nuclei](https://github.com/projectdiscovery/nuclei) is a fast, template-based vulnerability scanner that allows security researchers to create custom detection rules. While traditionally used for web application security, we've adapted it to scan Solana smart contract source code.

## Installation

```bash
# Install Nuclei
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# Clone this repository
git clone https://github.com/yourusername/solana-nuclei-templates.git
cd solana-nuclei-templates
```

## Usage

```bash
# Scan a single Solana program
nuclei -t solana-nuclei-templates/ -target /path/to/your/solana/program

# Scan multiple programs
nuclei -t solana-nuclei-templates/ -target /path/to/solana/projects/

# Generate HTML report
nuclei -t solana-nuclei-templates/ -target /path/to/solana/project -o report.html -report-formats html
```

## Template Categories

### Critical Vulnerabilities

- **Integer Overflow/Underflow** - Detects arithmetic operations without proper checks
- **Missing Signer Verification** - Identifies functions that don't verify signer authorization
- **Missing Account Owner Check** - Detects when account ownership isn't properly verified
- **Arbitrary CPI Vulnerability** - Finds unverified cross-program invocations

### High Severity Vulnerabilities

- **PDA Substitution Vulnerability** - Identifies potential PDA account manipulation
- **Loss of Precision** - Detects unsafe rounding in financial calculations
- **Division by Zero** - Finds potential program panics due to division operations
- **Uninitialized Account Check** - Detects missing initialization verification
- **Type Cosplay Vulnerability** - Identifies when account types can impersonate others

### Medium Severity Vulnerabilities

- **Missing Writable Account Check** - Detects when account writability isn't verified
- **Non-Canonical Bump Seed** - Identifies improper PDA bump seed validation
- **Duplicate Mutable Accounts** - Detects when the same account could be used for multiple parameters
- **Improper Account Closing** - Finds accounts that aren't properly zeroed when closed

### Informational Vulnerabilities

- **Missing Lamports Check** - Detects when lamports aren't verified before reading account data
- **Sysvar Address Check Missing** - Identifies unverified system accounts
- **Account Reloading Missing** - Detects stale account data usage after CPI calls

## Template List

1. `solana-integer-overflow-underflow.yaml` - Detects unchecked arithmetic operations
2. `solana-missing-signer-verification.yaml` - Identifies missing authorization checks
3. `solana-missing-account-owner-check.yaml` - Detects when account ownership isn't verified
4. `solana-pda-substitution-vulnerability.yaml` - Identifies potential PDA account manipulation
5. `solana-arbitrary-cpi-vulnerability.yaml` - Finds unverified cross-program invocations
6. `solana-loss-of-precision.yaml` - Detects unsafe rounding in financial calculations
7. `solana-division-by-zero.yaml` - Finds potential program panics due to division
8. `solana-saturating-operations-misuse.yaml` - Identifies potentially unsafe saturating operations
9. `solana-uninitialized-account-check.yaml` - Detects missing initialization verification
10. `solana-missing-writable-check.yaml` - Identifies when account writability isn't verified
11. `solana-sysvar-address-check-missing.yaml` - Detects unverified system accounts
12. `solana-non-canonical-bump-seed.yaml` - Identifies improper PDA bump seed validation
13. `solana-duplicate-mutable-accounts.yaml` - Detects potential same-account risks
14. `solana-type-cosplay-vulnerability.yaml` - Identifies account type impersonation risks
15. `solana-improper-account-closing.yaml` - Finds accounts not properly zeroed when closed
16. `solana-account-reloading-missing.yaml` - Detects stale account data usage after CPI calls
17. `solana-pyth-oracle-status-check.yaml` - Identifies missing oracle validity checks
18. `solana-unhandled-cpi-result.yaml` - Detects ignored CPI error results
19. `solana-missing-lamports-check.yaml` - Finds missing account existence validation
20. `solana-pda-sharing-vulnerability.yaml` - Identifies permission issues with shared PDAs
21. `solana-admin-permission-check-missing.yaml` - Detects missing administrator validation
22. `solana-insufficient-token-authority-reset.yaml` - Identifies incomplete authority transfers
23. `solana-unverified-token-program.yaml` - Detects unverified SPL token program usage
24. `solana-result-error-swallowing.yaml` - Finds silently ignored errors
25. `solana-unchecked-account-initialization.yaml` - Identifies reinitialization vulnerabilities

## Common Solana Vulnerabilities

The templates in this repository target common Solana vulnerabilities, including:

- Arithmetic errors (overflow, underflow, precision loss)
- Invalid account validation (ownership, initialization, authorization)
- Improper PDA handling (bump seed canonicalization, PDA sharing)
- Unsafe program invocation (CPI to untrusted programs)
- Inadequate state management (account reloading, closing)

For a detailed explanation of these vulnerabilities, refer to [SlowMist's Solana Smart Contract Security Best Practices](https://github.com/slowmist/solana-smart-contract-security-best-practices).

## Contributing

Contributions are welcome! If you want to add a new template or improve existing ones:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/new-template`)
3. Add your template or make changes
4. Test your template with Nuclei
5. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [SlowMist](https://github.com/slowmist) for their Solana smart contract security documentation
- [ProjectDiscovery](https://github.com/projectdiscovery) for the Nuclei scanner
- Solana developers community for security insights and best practices
