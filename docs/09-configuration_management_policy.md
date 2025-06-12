# 9. Configuration Management Policy

W2H standardizes and automates configuration management through the use of Ansible scripts as well as documentation of all changes to production systems and networks. Ansible automatically configures all W2H systems according to established and tested policies, and are used as part of our Disaster Recovery plan and process.

## 9.1 Applicable Standards

### 9.1.1 Applicable Standards from the HITRUST Common Security Framework

* 06 - Configuration Management

### 9.1.2 Applicable Standards from the HIPAA Security Rule

* 164.310(a)(2)(iii) Access Control & Validation Procedures

## 9.2 Configuration Management Policies

1. Ansible is used to standardize and automate configuration management.
2. No systems are deployed into W2H environments without approval of the W2H Engineering Lead.
3. All changes to production systems are approved by the W2H Engineering Lead before they are implemented to assure they comply with business and security requirements.
4. All changes to production systems are tested before they are implemented in production.
5. Implementation of approved changes are only performed by authorized personnel.
6. An up-to-date inventory of systems, including corresponding architecture diagrams for related products and services, is maintained by PMACS and available on request.
   * All systems are categorized as production, test, staging, and utility to differentiate based on criticality.
   * These reports are used to generate and / or maintain the diagrams and asset lists required by the Risk Assessment phase of W2H's Risk Management procedures ([§4.3.1](./04-risk_management_policy.md#431-risk-assessment)).
7. All frontend functionality (admin dashboards and portals) is separated from backend (database and app servers) systems by being deployed on separate virtual or physical servers or containers.
8. All software and systems are tested using unit tests and end to end tests.
9. All committed code is reviewed using pull requests to assure software code quality and proactively detect potential security issues in development.
10. W2H utilizes test (development) and staging environments that mirror production to assure proper function.
11. W2H also deploys environments locally to assure functionality before moving to staging or production.
12. All change requests must be formally filed and authorized before implementation.
13. W2H uses a modified version of [Security Technical Implementation Guides (STIGs)](https://public.cyber.mil/stigs/) published by the Defense Information Systems Agency as a baseline for hardening systems.
14. Clocks are continuously synchronized to an authoritative source across all systems using NTP or a platform-specific equivalent. Modifying time data on systems is restricted.

## 9.3 Provisioning Production Systems

1. Provisioning systems is managed fully by the PMACS infrastucture team. W2H requests are put in as a ticket in their ticketing system and after necessary approvals, the (virtual) servers are commissioned. 
2. The infrastructure team member must configure the new system according to the standard baseline chosen for the system's role.
   * For Linux systems, this means adding the appropriate configurations to the Ansible configuration file.
3. Since W2H assumes that all servers are likely to contain PHI, the configuration must encrypt the associated data volume of the VM during provisioning.
4. The default set up configurations (which cannot be changed unless approved by the relevant Security Officer) and maintained with version control on Gitlab ensure the following items are always implemented on every new system provisioned:
   * Removal of default users used during provisioning.
   * Network configuration for system.
   * Data volume encryption settings.
   * Antivirus/antimalware protection.
   * Server is added to vulnerability scanning service (Nessus Security Center)
   * Server is added to IPS service (Fortigate on Fortinet firewalls) 
   * All items listed below in the operating system-specific subsections below.
5. Once the Engineering Lead has verified the new system is correctly configured, the team member must add that system to the security scanner configuration.
6. The new system may be rotated into production once the infrastructure lead verifies all the provisioning steps listed above have been correctly followed.

### 9.3.1 Provisioning Linux Systems

1. Linux systems have their baseline security configuration applied via Ansible states. These baseline Ansible states cover:
   * Ensuring that the machine is up-to-date with security patches and is configured to apply patches in accordance with our policies.
   * Stopping and disabling any unnecessary OS services.
   * Configuring 15-minute session inactivity timeouts.
   * Installing and configuring the NTP daemon, including ensuring that modifying system time cannot be performed by unprivileged users.
   * Configuring IDS and antivirus/antimalware agents.
   * Configuring authentication to the centralized LDAP servers.
   * Configuring audit logging as described in the [Auditing Policy section](./08-auditing_policy.md).
2. Any additional Ansible states applied to the Linux system must be clearly documented by the engineering team member in the request by specifying the purpose of the new system.

### 9.3.2 Provisioning Management Systems

1. Provisioning management systems is maintained fully by the PMACS infrastucture team and follow Penn Medicine guidelines. 
2. Critical infrastructure services such as logging, monitoring and LDAP servers must be configured with appropriate Ansible states.
   * These Ansible states have been reviewed by the Engineering Lead, or an authorized delegate of the Engineering Lead or by the underlying hosting providers Infrastructure team, to be in accordance with all W2H policies, including setting appropriate:
     * Audit logging requirements.
     * Password size, strength, and expiration requirements.
     * Transmission encryption requirements.
     * Network connectivity timeouts.

## 9.4 Changing Existing Systems

1. Subsequent changes to already-provisioned systems are managed fully by the PMACS infrastucture team and follow Penn Medicine guidelines and would include documentation around:
   * Changes to Ansible states.
   * For configuration changes that cannot be handled by Ansible, a runbook describing exactly what changes will be made and by whom.
2. Configuration changes to Ansible states is managed via PMACS version control tools.
3. In all cases, before rolling out the change to production, the changes are applied to the Test environment and tested for a week before deploying in the STaging environment and tested again. Once testing passes, only then are the changes deployed to the Production environment.

## 9.5 Patch Management Procedures

1. W2H uses a combination of manual processes and automated tooling to ensure systems are up-to-date with the latest security patches.
2. On CentOS Linux systems, security patches are applied in phases.
   * The security team maintains a mirrored snapshot of security patches from the upstream OS vendor. This mirror is synchronized bi-weekly and applied to development and staging systems monthly.
   * If the development and staging systems function properly after a one-week testing period, these patches will be applied to all production systems during the next patch run.
   * Patches for critical kernel security vulnerabilities may be applied to production systems using hot-patching tools at the discretion of the Security Officer or designated personnel. These patches must follow the same phased testing process used for non-kernel security patches; this process may be expedited for severe vulnerabilities.

## 9.6 Software Development Procedures

1. All development uses feature branches based on the main branch used for the current release. Any changes required for a new feature or defect fix are committed to that feature branch.
   * These changes must be covered under 1) a unit test where possible, or 2) integration tests.
   * Integration tests are _required_ if unit tests cannot reliably exercise all facets of the change.
2. Developers are strongly encouraged to follow the [commit message conventions suggested by GitHub](https://github.com/blog/926-shiny-new-commit-styles).
   * Commit messages should be wrapped to 72 characters.
   * Commit messages should be written in the present tense. This convention matches up with commit messages generated by commands like git merge and git revert.
3. Once the feature and corresponding tests are complete, a pull request will be created using the GitLab web, IDE or command line interface. The pull request should indicate which feature or defect is being addressed and should provide a high-level description of the changes made.
4. Code reviews are performed as part of the pull request procedure. Once a change is ready for review, the designated technical reviewer will be notified using an appropriate mechanism, typically by assignment or claim within the JIRA system.
   * The designated engineer(s) will review the changes, using the guidelines above.
   * Engineers should note all potential issues with the code; it is the responsibility of the author(s) to address those issues or explain why they are not applicable.
5. If the feature or defect interacts with ePHI, or controls access to data potentially containing ePHI, the code changes must be reviewed as follows before the feature is marked as complete.
   * Perform a security analysis of features to ensure they satisfy W2H's compliance and security commitments.
   * Verify that any actions performed by authenticated users will generate appropriate audit log entries.
6. Once the review process finishes, each reviewer should leave a comment on the pull request saying "looks good to me" (often abbreviated as "LGTM") or similar, at which point the original author(s) may merge their change into the release branch.

## 9.7 Software Release Procedures

1. Software releases are treated as changes to existing systems and thus follow the procedure described in [§9.4](./09-configuration_management_policy.md#94-changing-existing-systems).
