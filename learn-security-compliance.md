---

copyright:
  years: 2018, 2025
lastupdated: "2025-01-29"

keywords: rabbitmq, databases, soc, hipaa, gdpr, terms, rabbitmq security compliance, pci dss

subcollection: messages-for-rabbitmq

---

{{site.data.keyword.attribute-definition-list}}

# Security and compliance
{: #security-compliance}

## Protection against unauthorized access
{: #protection-unauth}

{{site.data.keyword.messages-for-rabbitmq_full}} use the following methods to protect data in transit or in storage.
- All {{site.data.keyword.messages-for-rabbitmq}} connections use TLS/SSL encryption for data in transit. The current supported version of this encryption is TLS 1.2.
- Access to the Account, Management Console UI, and API is secured via [Identity and Access Management (IAM)](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-iam).
- Access to the database is secured through the standard access controls provided by the database. These access controls are configured to require valid database-level credentials that are obtainable only through prior access to the database or through our Management Console UI or API.
- All {{site.data.keyword.messages-for-rabbitmq}} disk is provided on storage encrypted with LUKS using AES-256. The default keys are managed by [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-about). Bring-your-own-key (BYOK) for encryption is also available through [Key Protect Integration](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-key-protect).
- IP allowlisting - All deployments support [allowlisting IP addresses](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-allowlisting) to restrict access to the service.
- Public and Private Networking - {{site.data.keyword.messages-for-rabbitmq}} is integrated with [Service Endpoints](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-service-endpoints). You can select whether to use connections over the public network, the {{site.data.keyword.cloud_notm}} internal network, or both.
- Dedicated Cores - Allocating dedicated cores to your deployment introduces hypervisor-level isolation to your database instance, using isolated virtual machines to ensure your data processing remains separated from other customers. It also provides a guaranteed minimum number of CPUs to your deployment. Deployments with dedicated cores in the same Resource Group and {{site.data.keyword.cloud_notm}} Region can share a virtual machine.

## Data resilience
{: #data-resilience}

- [Backups](/docs/cloud-databases?topic=cloud-databases-dashboard-backups) are included in the service. {{site.data.keyword.messages-for-rabbitmq}} backups reside in [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage&cloud-object-storage-about-cloud-object-storage) and are also [encrypted](/docs/cloud-object-storage?topic=cloud-object-storage-security).
- RabbitMQ backups contain only definitions, topology, and metadata. Messages are not stored in backups.
- All {{site.data.keyword.messages-for-rabbitmq}} deployments are configured with replication. Deployments contain a cluster with three nodes where all three nodes are equal peers. Queues are mirrored on all three nodes.
- If you deploy to an {{site.data.keyword.cloud_notm}} Single-Zone Region (SZR), each database node resides on a different host in the data center.
- If you deploy to an {{site.data.keyword.cloud_notm}} Multi-Zone Region (MZR), the nodes are spread over the region's availability zone locations.

## SOC 2 Type 2 Certification
{: #soc2-type2-cert}

{{site.data.keyword.IBM_notm}} provides a Service Organization Controls (SOC) 2 Type 2 report for {{site.data.keyword.messages-for-rabbitmq}}. The reports evaluate IBM's operational controls according to the criteria set by the American Institute of Certified Public Accountants (AICPA) Trust Services Principles. The Trust Services Principles define adequate control systems and establish industry standards for service providers such as {{site.data.keyword.cloud_notm}} to safeguard their customers' data and information.

You can request an SOC 2 Type 2 report from the customer portal or contact your sales representative. Alternatively, you can open a support ticket with [{{site.data.keyword.cloud_notm}} support](https://cloud.ibm.com/unifiedsupport/supportcenter){: .external}

## ISO 27017, ISO 27018
{: #iso-27017-iso-27018}

{{site.data.keyword.messages-for-rabbitmq}} conforms to the guidelines for information security controls applicable to the provision and use of cloud services that are defined in [ISO 27017](https://www.iso.org/standard/43757.html){: .external} and [ISO 27018](https://www.iso.org/standard/76559.html){: .external}.

## General Data Protection Regulation (GDPR)
{: #-gdpr}

If you have an account with {{site.data.keyword.cloud_notm}}, your personal data is held by {{site.data.keyword.cloud_notm}}. The {{site.data.keyword.IBM_notm}} Data Processing Addendum (Addendum) applies to the processing of client's personal data by {{site.data.keyword.IBM_notm}} on behalf of client in order to provide {{site.data.keyword.IBM_notm}} standard services.

{{site.data.keyword.messages-for-rabbitmq}} processes limited client Personal Information (PI) in the course of running the service and optimizing the user experience.

{{site.data.keyword.messages-for-rabbitmq}} provides a [Data Sheet Addendum (DSA)](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=040987F07A6111E89D57EFEED3CB8BE9){: .external} with its policies as a Data Processor regarding content and data protection.

## HIPAA
{: #hipaa}

{{site.data.keyword.messages-for-rabbitmq}} meets the required {{site.data.keyword.IBM_notm}} controls that are commensurate with the Health Insurance Portability and Accountability Act of 1996 (HIPAA) Security and Privacy Rule requirements. These requirements include the appropriate administrative, physical, and technical safeguards required of Business Associates in 45 CFR Part 160 and Subparts A and C of Part 164. HIPAA must be requested at the time of provisioning and requires a representative to sign a Business Associate Addendum (BAA) agreement with {{site.data.keyword.IBM_notm}}.

## PCI DSS
{: #pci-dss}

{{site.data.keyword.databases-for-rabbitmq}} are compliant with the Payment Card Industry Data Security Standard (PCI DSS). {{site.data.keyword.cloud_notm}} completes annual PCI DSS assessments by using an approved Qualified Security Assessor (QSA), and the resulting Attestations of Compliance (AOCs) and Service Responsibility Matrix (SRM) guides are available upon customer request. Auditors reviewed {{site.data.keyword.databases-for-rabbitmq}} for compliance under PCI DSS version 3.2.1 at Service Provider Level 1.

Customers are responsible for the storing, processing, and transmission of their cardholder data, and can create cardholder data environments (CDEs) that can store, transmit, or process cardholder data by using {{site.data.keyword.databases-for-rabbitmq}}. Customers can request and use the {{site.data.keyword.cloud_notm}} AOCs and SRM guides when they seek their own PCI DSS certifications. It is the responsibility of the customer to document and operate CDEs and applications that are built by using {{site.data.keyword.cloud_notm}} Platform services in a PCI DSS-compliant manner.

It is the customer’s responsibility to familiarize themselves with these processes and to manage data retention and removal from the service according to the customer’s policies.

A full list of PCI DSS-ready {{site.data.keyword.cloud_notm}} Platform services, and options to request a PCI DSS AOC and SRM guide, can be found at the [{{site.data.keyword.cloud_notm}} compliance page](https://www.ibm.com/cloud/compliance/industry).

## Terms
{: #terms}

- [The IBM Privacy Policy](https://www.ibm.com/privacy/us/en/)
- [The {{site.data.keyword.cloud_notm}} Notices and Terms of Use](/docs/overview/terms-of-use?topic=overview-terms)
