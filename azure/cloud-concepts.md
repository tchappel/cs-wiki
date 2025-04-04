## Shared Responsibility Model

The shared responsibility model in cloud computing varies depending on the cloud service type being used.

**on-premises** datacenter, the company is responsible for everything, including the physical space, security, servers, infrastructure, software, patching, and updates.

### Infrastructure as a Service (IaaS)

- The cloud provider is responsible for maintaining:
    - hardware, network connectivity (to the internet), and physical security. 
- You’re responsible for everything else.

## Platform as a Service (PaaS)

- The cloud provider is responsible for maintaining:
    - hardware, network connectivity (to the internet), and physical security;
    - operating systems, middleware, development tools, and business intelligence services
- You’re responsible for everything else.

**Software as a Service (SaaS)**

With SaaS, you’re essentially renting or using a fully developed application.

In a SaaS environment you’re responsible for the data that you put into the system, the devices that you allow to connect to the system, and the users that have access. Nearly everything else falls to the cloud provider.

## Cloud models 

define the deployment type of cloud resources.

The three main cloud models are private, public, and hybrid.

A **private cloud** is used by a single entity, offering greater control but potentially higher costs and fewer benefits than public clouds. It can be hosted on-site or in a dedicated offsite datacenter. Organizations have complete control over resources and security, and their data is not collocated with others. However, they are responsible for hardware purchase and maintenance.

A **public cloud** is built, controlled, and maintained by a third-party provider, with resources available to anyone who wants to purchase cloud services. A key difference is its general public availability. There are no capital expenditures to scale up, applications can be quickly provisioned and deprovisioned, and organizations pay only for what they use. However, organizations don't have complete control over resources and security.

A **hybrid cloud** uses both public and private clouds in an interconnected environment. It can be used for handling temporary demand surges from a private cloud using public resources and provides an extra layer of security by allowing users to choose where to deploy services. It offers the most flexibility, allowing organizations to determine where to run their applications and control security and compliance.

A **multi-cloud** scenario involves using multiple public cloud providers, potentially leveraging different features or during a migration process. In this environment, organizations manage resources and security across multiple providers.

**Azure Arc** helps manage cloud environments across public, private, hybrid, and multi-cloud deployments.

**Azure VMware Solution** allows running VMware workloads in Azure for those migrating from a private VMware environment to public or hybrid clouds.

## Consumption-based model

2 types of expenses

- Capital expenditure (CapEx)
- Operational expenditure (OpEx)

Cloud computing falls under OpEx because cloud computing operates on a consumption-based model. With cloud computing, you don’t pay for the physical infrastructure, the electricity, the security, or anything else associated with maintaining a datacenter. Instead, you pay for the IT resources you use. If you don’t use any IT resources this month, you don’t pay for any IT resources.

## Service Level Agreement (SLA)

Agreement of state of service between the cloud service provider (Azure) and the customer

## Availability

- Expressed as a **% Up Time**, Opposed to **% Down Time**
- common SLA availability levels in Azure are 99.9% (three nines), 99.95%, 99.99% (four nines).

## Scalability

Scalability refers to the ability to adjust resources to meet demand.

- **Vertical scaling (scale up/down)**: increasing the size of a single resource (e.g., adding more CPU or memory to a virtual machine)
- **Horizontal scaling (scale out/in)**: adding more resources of the same type (e.g., adding more virtual machines to a load balancer)

## Reliability

Reliability is the ability of applications and services to remain available to users, even in the face of hardware failures, network issues, or other disruptions. The cloud, by virtue of its decentralized design, naturally supports a reliable and resilient infrastructure.

## Predictability

Predictability is the ability to forecast the performance and cost of cloud services.

## Global Azure vs. Azure Government

Microsoft Global Azure and Azure Government are both cloud offerings from Microsoft, but they serve different audiences and have distinct compliance requirements.

1. Microsoft Global Azure
	•	The standard, public cloud available to businesses, individuals, and organizations worldwide.
	•	Operates in multiple regions across the globe, providing a broad range of services (compute, storage, networking, AI, etc.).
	•	Shared infrastructure with other Azure customers, but with security measures like virtual network isolation.
	•	Supports global compliance standards such as ISO, GDPR, HIPAA, and SOC.

2. Azure Government
	•	A separate cloud designed specifically for U.S. government agencies and their partners.
	•	Operates in physically isolated data centers within the U.S.
	•	Complies with strict U.S. government regulations, including FedRAMP High, DoD IL5, and CJIS.
	•	Only U.S. federal, state, local governments, and approved contractors can access it.
	•	Offers additional security and compliance for classified and sensitive data.