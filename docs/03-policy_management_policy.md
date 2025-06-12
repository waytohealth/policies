# 3. Policy Management Policy

W2H implements policies and procedures to maintain compliance and integrity of data. The designated Security Officer and Privacy Officer are responsible for maintaining policies and procedures and assuring all W2H workforce members, business associates, customers, and partners are adherent to all applicable policies. Previous versions of policies are retained to assure ease of finding policies at specific historic dates in time.

## 3.1 Applicable Standards

### 3.1.1 Applicable Standards from the HITRUST Common Security Framework

* 12.c - Developing and Implementing Continuity Plans Including Information Security

### 3.1.2 Applicable Standards from the HIPAA Security Rule

* 164.316(a) - Policies and Procedures
* 164.316(b)(1)(i) - Documentation

## 3.2 Maintenance of Policies

1. All policies are stored and updated to maintain W2H compliance with relevant standards. Updates and version control are done similarly to source code control.
2. Policy suggestions can be made by any workforce member at any time. Furthermore, all policies are reviewed annually by the Security and Privacy Officer or their designees to assure they are accurate and up-to-date.
3. W2H employees may request changes to policies using the following process:
  1. The W2H employee initiates a policy change request by creating an Issue in the JIRA. The change request may optionally include a pull request from a separate branch or repository containing the desired changes.
  2. The Security Officer or the Privacy Officer is assigned to review the policy change request.
  3. Once the review is completed, the Security Officer or Privacy Officer approves or rejects the Issue. Only the Security Officer and the Privacy Officer are granted the access permissions to merge policy change requests. If the Issue is rejected, it goes back for further review and documentation.
  4. If the review is approved, the Security Officer or Privacy Officer then marks the Issue as Done, adding any pertinent notes required.
  5. If the policy change requires technical modifications to production systems, those changes are carried out by authorized personnel using W2H's [change management process (§9.4)](./09-configuration_management_policy.md#94-changing-existing-systems).
4. All policies are made accessible to all W2H workforce members. The current master policies are published at [https://policy.waytohealth.org](https://policy.waytohealth.org).
   * The Security Officer also communicates policy changes to all employees via email. These emails include a high-level description of the policy change using terminology appropriate for the target audience.
5. All policies, and associated documentation, are retained for 2 (two) years from the date of its creation or the date when it last was in effect, whichever is later.
   1. Version history of all W2H policies is managed via a Git repository.
6. The policies and information security policies are reviewed and audited annually, or after significant changes occur to W2H's organizational environment. Issues that come up as part of this process are reviewed by W2H management to assure all risks and potential gaps are mitigated and/or fully addressed. The process for reviewing polices is outlined below:
  1. The Security Officer initiates the policy review by creating an Issue in the JIRA.
  2. The Security Officer or the Privacy Officer is assigned to review the current W2H policies (<https://policy.waytohealth.org>).
  3. If changes are made, the process described in (§3.3) above is followed. All changes are documented in the Issue.
  4. Once the review is completed, the Security Officer or Privacy Officer approves or rejects the Issue. If the Issue is rejected, it goes back for further review and documentation.
  5. If the review is approved, the Security Officer or Privacy Officer then marks the Issue as Done, adding any pertinent notes required.
  6. Policy review is monitored on a quarterly basis using the JIRA reporting to assess compliance with above policy.

Additional documentation related to maintenance of policies is outlined in [§5.3.1 - Security Officer](./05-roles_policy.md#53-security-officer)
