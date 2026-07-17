# Episode 02 – Azure Virtual Network (VNet)

## Objective

Understand Azure Virtual Networks and create the first VNet for our Azure SRE lab.

---

## Lab Details

| Property | Value |
|----------|-------|
| Resource Group | azure-sre-lab-rg |
| Virtual Network | azure-sre-vnet |
| Location | South India |
| Address Space | 10.10.0.0/16 |
| Subnet | web-subnet |
| Subnet Address | 10.10.1.0/24 |

---

## Why do we need a VNet?

- Provides a private network in Azure.
- Isolates cloud resources.
- Enables secure communication.
- Supports subnet segmentation.
- Forms the foundation for Azure networking.

---

## AWS Comparison

| AWS | Azure |
|------|--------|
| VPC | Virtual Network (VNet) |
| CIDR Block | Address Space |
| Subnet | Subnet |

---

## Lessons Learned

- A VNet is the networking foundation in Azure.
- Address planning is important for future scalability.
- Azure prevents overlapping subnets within the same VNet.
- Resources in a VNet communicate privately.

---

## Interview Questions

1. What is Azure VNet?
Ans:- Azure Virtual Network (VNet) is a logically isolated private network in Microsoft Azure that enables Azure resources such as Virtual Machines, Load Balancers, and Databases to communicate securely with each other, with on-premises environments, and with the internet in a controlled manner. It provides network isolation, IP address management, routing, subnetting, and integration with security services like Network Security Groups (NSGs) and Azure Firewall.

Azure VNet is a private network in Azure that allows secure communication between Azure resources while providing isolation, routing, and security controls.

I consider VNet as the networking foundation of every Azure deployment. Without a properly designed VNet, it's difficult to build secure, scalable, and highly available applications.

3. Difference between VNet and VPC?
Ans:-
| AWS VPC                     | Azure VNet                   |
| --------------------------- | ---------------------------- |
| AWS networking service      | Azure networking service     |
| Uses CIDR Block             | Uses Address Space           |
| Supports Subnets            | Supports Subnets             |
| Uses Security Groups        | Uses NSGs                    |
| Uses Route Tables           | Uses Route Tables            |
| Connected using VPC Peering | Connected using VNet Peering |

Functionally, Azure VNet and AWS VPC serve the same purpose—they provide isolated private networks in the cloud. The main differences are in terminology, implementation details, and integration with other cloud-native services

If you understand AWS VPC well, learning Azure VNet is straightforward because the networking principles remain the same. The biggest difference is how Azure integrates networking with its native services and management model.

3. Why is CIDR planning important?
Interview Answer

CIDR planning is essential because it defines the IP address space available for Azure resources. Proper planning ensures enough IP addresses for current and future workloads, prevents overlapping address spaces, supports subnet segmentation, and simplifies hybrid connectivity with on-premises networks or other cloud environments.

Practical Example

Suppose:

Azure VNet

10.10.0.0/16

Later you need:

Web
Application
Database
Kubernetes
Bastion
VPN Gateway

If you initially chose:

10.10.0.0/24

you'll quickly run out of address space.

Good planning avoids future redesign.

SRE Perspective

Poor CIDR planning becomes a major problem during cloud expansion, VNet peering, VPN connections, and mergers with other organizations. As an SRE, I always reserve sufficient address space for future growth.

4. Can a VNet have multiple subnets?
Interview Answer

Yes. A VNet can contain multiple subnets. Each subnet represents a logical network segment with its own IP range and can have different security rules, routing policies, and workloads.

Example
Azure VNet
10.10.0.0/16

│

├── Web Subnet
10.10.1.0/24

├── App Subnet
10.10.2.0/24

├── Database Subnet
10.10.3.0/24

├── AKS Subnet
10.10.4.0/24

└── Bastion Subnet
10.10.5.0/26
Why?

Different workloads require different security and network policies.

For example:

Web servers receive internet traffic.
Application servers communicate only with the web tier.
Databases accept connections only from the application tier.
SRE Perspective

I avoid placing all resources in one subnet because network segmentation improves security, simplifies management, and reduces the attack surface.

5. Can the address space be modified after deployment?
Interview Answer

Yes. Azure allows modifying the VNet address space after deployment, provided the changes do not conflict with existing subnets, peered VNets, VPN connections, or deployed resources. Any new address range must be carefully planned to avoid overlapping IP ranges.

Practical Example

Initially:

10.10.0.0/16

Later you expand:

10.10.0.0/16

+

10.20.0.0/16

Azure supports this expansion if there are no conflicts.

Important Interview Point

You cannot create overlapping subnets inside the same VNet.

Example:

Subnet A

10.10.1.0/24

and

Subnet B

10.10.1.128/25

❌ Azure will reject this because the IP ranges overlap.

SRE Perspective

Although Azure allows address space modification, I prefer designing the address space correctly from the beginning because changes in production environments can affect routing, peering, VPNs, and dependent services.

⭐ Bonus Question (Very Common in Interviews)
### Why do we create separate subnets instead of keeping everything in one subnet?

Separate subnets provide logical isolation between workloads such as web, application, and database tiers. They allow different Network Security Groups, routing policies, and access controls to be applied to each layer, improving security, scalability, and manageability. This follows the principle of least privilege and reduces the attack surface.

🎯 Interview Tip

From now on, I want you to prepare every Azure topic in three levels:

Level 1 – Beginner (Definition)

"What is VNet?"

Level 2 – Intermediate (Working)

"How do you create and configure a VNet?"

Level 3 – Senior SRE (Design)

"How would you design the networking for a production banking application deployed across multiple Azure regions with disaster recovery, hybrid connectivity, and strict security requirements?"

Senior SRE interviews are usually won at Level 3. Given your 18+ years in infrastructure and operations, that's the level we're targeting. We'll still learn the basics thoroughly, but every lesson will gradually move toward production design, troubleshooting, and architecture so you're fully prepared for the roles you're aiming for in Hyderabad.

### 5. Why is CIDR planning important?
Ans:- CIDR planning is essential because it defines the IP address space available for Azure resources. Proper planning ensures enough IP addresses for current and future workloads, prevents overlapping address spaces, supports subnet segmentation, and simplifies hybrid connectivity with on-premises networks or other cloud environments.

Practical Example

Suppose:

Azure VNet

10.10.0.0/16

Later you need:

Web
Application
Database
Kubernetes
Bastion
VPN Gateway

If you initially chose:

10.10.0.0/24

you'll quickly run out of address space.

Good planning avoids future redesign.

SRE Perspective

Poor CIDR planning becomes a major problem during cloud expansion, VNet peering, VPN connections, and mergers with other organizations. As an SRE, I always reserve sufficient address space for future growth.

### 7. Can a VNet have multiple subnets?
Ans:- Yes. A VNet can contain multiple subnets. Each subnet represents a logical network segment with its own IP range and can have different security rules, routing policies, and workloads.

Example
Azure VNet
10.10.0.0/16

│

├── Web Subnet
10.10.1.0/24

├── App Subnet
10.10.2.0/24

├── Database Subnet
10.10.3.0/24

├── AKS Subnet
10.10.4.0/24

└── Bastion Subnet
10.10.5.0/26
Why?

Different workloads require different security and network policies.

For example:

Web servers receive internet traffic.
Application servers communicate only with the web tier.
Databases accept connections only from the application tier.
SRE Perspective

I avoid placing all resources in one subnet because network segmentation improves security, simplifies management, and reduces the attack surface.


### 9. Can the address space be modified after deployment?
Ans:- Yes. Azure allows modifying the VNet address space after deployment, provided the changes do not conflict with existing subnets, peered VNets, VPN connections, or deployed resources. Any new address range must be carefully planned to avoid overlapping IP ranges.

Practical Example

Initially:

10.10.0.0/16

Later you expand:

10.10.0.0/16

+

10.20.0.0/16

Azure supports this expansion if there are no conflicts.

Important Interview Point

You cannot create overlapping subnets inside the same VNet.

Example:

Subnet A

10.10.1.0/24

and

Subnet B

10.10.1.128/25

❌ Azure will reject this because the IP ranges overlap.

SRE Perspective

Although Azure allows address space modification, I prefer designing the address space correctly from the beginning because changes in production environments can affect routing, peering, VPNs, and dependent services.

### Why do we create separate subnets instead of keeping everything in one subnet?

Separate subnets provide logical isolation between workloads such as web, application, and database tiers. They allow different Network Security Groups, routing policies, and access controls to be applied to each layer, improving security, scalability, and manageability. This follows the principle of least privilege and reduces the attack surface.
---

## Next Episode

Network Security Groups (NSGs)
