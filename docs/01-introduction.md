# 1. Introduction

[Penn Medicine Way To Health](https://waytohealth.upenn.edu), Inc ("W2H") is committed to ensuring the confidentiality, privacy, integrity, and availability of all electronic protected health information (ePHI) it receives, maintains, processes and/or transmits on behalf of its Customers. As a patient engagement and health research technology organization, W2H strives to maintain compliance, proactively address information security, mitigate risk for its Customers, and assure known breaches are completely and effectively communicated in a timely manner. The following documents address core policies used by W2H to maintain compliance and assure the proper protections of infrastructure used to store, process, and transmit ePHI for W2H Customers.

W2H provides secure and compliant software to administer behavioral change and patient engagement programs. Customers utilize the hosted software and infrastructure from W2H to research and deploy evidence-based approches to engage patients in their health. W2H makes every effort to reduce the risk of unauthorized disclosure, access, and/or breach of Customer data through network (firewalls, dedicated IP spaces, etc), server settings (encryption at rest and in transit etc), and application security requirements (password strength rules, account roles/privileges, etc).

W2H signs business associate agreements (BAAs) with its Customers. These BAAs outline W2H obligations and Customer obligations, as well as liability in the case of a breach. In providing infrastructure and managing security configurations that are a part of the technology requirements that exist in HIPAA and HITRUST, as well as future compliance frameworks, W2H manages various aspects of compliance for Customers. The aspects of compliance that W2H manages for Customers are inherited by Customers, and W2H assumes the risk associated with those aspects of compliance as defined in the BAA. In doing so, W2H achieves and maintains compliance, while mitigating Customer risk.

W2H does not act as a covered entity but rather as a provider of services to covered entities and other organizations. Certain aspects of our compliance are inherited from our hosting provider, Azure or [Penn Medicine Academic Compute Services](https://www.med.upenn.edu/pmacs/), part of Penn Medicine Corporate IS as appropriate. More details about Azure's HITRUST and HIPAA compliance posture is available for review [here](https://www.microsoft.com/en-us/trustcenter/Compliance/HITRUST). Penn Medicine's policies and procedures are also incorporated into this document as relevant given that W2H operates within the Penn Medicine umbrella.  

Mappings of HIPAA Rules to W2H controls are covered in [§2](./02-hipaa_inheritance.md).

## 1.1 W2H Organizational Concepts

The physical infrastructure environment is hosted at [Microsoft Azure](https://azure.microsoft.com/) or on PMACS. In either case, the network components and supporting network infrastructure are contained within the relevant infrastructure and is managed by the provider. W2H does not have physical access into the network components. The W2H environment consists of Fortinet FortiGate firewalls and CentOS-based Virtual servers operating on VMWare running Apache web servers; PHP and Node.js application servers; MariaDB and PostgreSQL database servers; Docker containers; logging servers; Ansible configuration management servers; Fortigate IDS /IPS always-on services; Crowdstrike Falcon for NextGen AV/EDR; Nessus vulnerability scanning services; Illumio application segmentation; and developer tool servers.

Within the W2H Platform, all data transmission is encrypted and all hard drives are encrypted so data at rest is also encrypted; this applies to all servers - those hosting Docker containers, databases, APIs, log servers, etc. W2H assumes all data *may* contain ePHI, even though our Risk Assessment does not indicate this is the case, and provides appropriate protections based on that assumption.

W2H additionally restricts, secures, and assures the privacy of all ePHI data at the Application Level.

W2H has implemented strict logical access controls so that only authorized personnel are given access to the internal management servers. 

Once the data is received from the application server, a series of Application Programming Interface (API) calls or SQL queries is made to the database servers where the ePHI resides.

The VPN server and Apache web server are externally facing and accessible via the Internet. The application and database servers, where the ePHI resides, are located on the internal PMACS network and can only be accessed through a bastion host over a VPN connection. Access to the internal database is restricted to a limited number of personnel and strictly controlled to only those personnel with a business-justified reason.

Application, database and operating systems are tested end-to-end for usability, security, and impact prior to deployment to production.

## 1.2 Requesting Audit and Compliance Reports

W2H, at its sole discretion, can share audit reports, including its planned HITRUST reports and Corrective Action Plans (CAPs), with customers on a case by case basis. All audit reports are shared under explicit NDA in Penn Medicine's format between Penn Medicine and party to receive materials. Audit reports can be requested by W2H workforce members for Customers or directly by W2H Customers.

The following process is used to request audit reports:

1. Email is sent to your implementation lead. In the email, please specify the type of report being requested and any required timelines for the report.
2. W2H staff will log an issue with the details of the request into the W2H Ticketing System (JIRA) which is Atlassian's JIRA solution. JIRA is used to track requests' status and outcomes.
3. W2H will confirm if a current NDA is in place with the party requesting the audit report. If there is no NDA in place, W2H will send one for execution.
4. Once it has been confirmed that an NDA is executed, W2H staff will move the issue to "Under Review".
5. The W2H / PennMedicine Security Officer or Privacy Officer must Approve or Reject the Issue. If the Issue is rejected, W2H will notify the requesting party that we cannot share the requested report.
6. If the issue has been Approved, W2H will send the customer the requested audit report and close the JIRA issue for the request.

## 1.3 Version Control

These policies are managed in a private Gitlab repository managed within the University of Pennsylvania network for source control. The most recent version of the policies is available at <https://policy.waytohealth.org>.

These policies were last updated on June 6, 2025.
