# RHEL 9 STIG Exceptions Summary

## Overview
This document summarizes the modifications made to the RHEL 9 STIG Ansible playbook to exclude 28 known failing rules from the compliance scan results.

## Changes Made

### 1. Disabled Rules in defaults/main.yml
A total of 27 rules have been disabled by setting their corresponding variables to `false` in the `defaults/main.yml` file. Each disabled rule includes a comment indicating it was disabled due to known compliance scan failures.

### 2. Missing Rules
Two rules identified in the compliance scan (RHEL-09-672030 and RHEL-09-672045) were not found in the current version of the playbook and may have been removed or renamed in this STIG revision.

### 3. Documentation Updates
- Updated `Changelog.md` with detailed information about all disabled rules
- Created this summary document for reference

## How to Use the Modified Playbook

1. **Running the playbook**: No changes are needed to how you run the playbook. The disabled rules will simply be skipped during execution.

   ```bash
   ansible-playbook -i inventory site.yml
   ```

2. **Re-enabling specific rules**: If you need to re-enable any of the disabled rules, edit `defaults/main.yml` and change the value from `false` back to `true`:

   ```yaml
   # Example: Re-enable RHEL-09-211020
   rhel_09_211020: true  # Remove or update the comment
   ```

3. **Verifying disabled rules**: You can check which rules are disabled by running:

   ```bash
   grep "false  # Disabled - Known to fail" defaults/main.yml
   ```

## Categories of Disabled Rules

1. **Account and Authentication** (9 rules) - Related to user account management, PAM configuration, and authentication settings
2. **System Security** (9 rules) - File system permissions, ownership, and integrity checks
3. **Network and Service** (3 rules) - Firewall and SSH configuration
4. **Auditing and Logging** (5 rules) - AIDE, rsyslog, and audit subsystem configuration
5. **Cryptography** (1 rule) - FIPS mode configuration

## Important Notes

- These rules were disabled because they consistently fail in the compliance scan environment
- The underlying security controls may still be important for your organization
- Consider implementing alternative compensating controls if these rules address critical security requirements
- Always test in a non-production environment before deploying to production systems

## Backup
A backup of the original `defaults/main.yml` file was created as `defaults/main.yml.backup` before making changes.