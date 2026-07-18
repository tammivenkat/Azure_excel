## Default NSG Rules

| Priority | Rule | Action |
|----------|------|--------|
| 65000 | AllowVnetInBound | Allow |
| 65001 | AllowAzureLoadBalancerInBound | Allow |
| 65500 | DenyAllInBound | Deny |

### Observation

Azure automatically creates default security rules.
Custom rules with a lower priority number (higher precedence) are evaluated first.
