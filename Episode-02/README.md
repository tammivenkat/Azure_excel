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
2. Difference between VNet and VPC?
3. Why is CIDR planning important?
4. Can a VNet have multiple subnets?
5. Can the address space be modified after deployment?

---

## Next Episode

Network Security Groups (NSGs)
