# project1-hardened-azure-landing-zone

# Project 1: Hardened Azure Landing Zone (Zero-Trust Foundation)

**Goal**  
Build a simple, secure Azure landing zone that follows zero-trust principles: private network isolation, deny-all inbound by default, explicit allow for trusted access, controlled outbound, and free posture monitoring with Microsoft Defender for Cloud.

This project proves hands-on cloud security engineering basics: resource organization, network segmentation, traffic filtering, and security visibility — skills directly relevant to junior/mid-level Azure Security Engineer roles.

**Date**: February 2026  
**Tools**: Azure Portal  
**Total cost**: £0 (free tier, no running compute)  
**Resources created**: Subscription, Resource Group, VNet + subnet, NSG with custom rules, Defender for Cloud (free CSPM)

## Architecture Overview
- **Subscription**: New pay-as-you-go with £200 credit  
- **Resource Group**: `proj1-hardened-landing-zone-rg`  
- **VNet**: `proj1-vnet` (10.0.0.0/16 private address space)  
  - Subnet: `default` (10.0.0.0/24)  
- **NSG**: `proj1-nsg` attached to `default` subnet  
  - Inbound: Deny all public traffic except SSH from my IP  
  - Outbound: Allow internet for updates/packages  
- **Defender for Cloud**: Free Foundational CSPM enabled (posture scanning + recommendations)

## Step-by-Step Build

1. **Created new Azure Subscription**  
   - Used pay-as-you-go plan with free £200 credit  
   - Set budget alert at 100% of £200 to monitor spend  
   - Purpose: Isolated environment for this project (no mixing with personal/default sub)

2. **Created Resource Group**  
   - Name: `proj1-hardened-landing-zone-rg`  
   - Region: UK South (lowest latency for London)  
   - Why: Logical container for all project resources — makes cleanup easy and keeps billing/ownership clear

3. **Created Virtual Network (VNet)**  
   - Name: `proj1-vnet`  
   - Address space: `10.0.0.0/16` (65,536 private IPs)  
   - Subnet: `default` (`10.0.0.0/24` – 256 IPs)  
   - Region: UK South  
   - Why: Provides private IP space inside Azure — no public internet exposure by default (zero-trust base layer)

4. **Created & Attached Network Security Group (NSG)**  
   - Name: `proj1-nsg`  
   - Attached to `default` subnet in `proj1-vnet`  
   - Why: NSG acts as network-level firewall — controls inbound/outbound traffic to/from subnet

5. **Configured Inbound Security Rules**  
   - **Priority 100**: Deny-All-Inbound-Internet  
     - Source: Any  
     - Destination: Any  
     - Ports/Protocol: Any  
     - Action: Deny  
     - Purpose: Block all unsolicited public inbound traffic (overrides Azure defaults)

   - **Priority 110**: Allow-SSH-Inbound  
     - Source: My public IP only (148.252.x.x/32)  
     - Destination port: 22  
     - Protocol: TCP  
     - Action: Allow  
     - Purpose: Allow secure remote access for testing (restricted to single trusted IP)

   - Rule order: Lower priority number evaluated first → Deny 100 blocks everything except explicit Allow 110

6. **Configured Outbound Security Rule**  
   - **Priority 120**: Allow-Outbound-Internet  
     - Source: Any  
     - Destination: Any  
     - Ports/Protocol: Any  
     - Action: Allow  
     - Purpose: Permit VMs/containers to reach internet (updates, packages, APIs) while still being explicit

7. **Enabled Microsoft Defender for Cloud (Free Tier)**  
   - Onboarded Foundational CSPM (free posture management)  
   - Subscription scanned: 2 resources assessed (VNet + NSG)  
   - Initial Secure Score: N/A (scan delay on new sub)  
   - Recommendations: 6 items listed (mostly "Not evaluated" during first scan)  
   - Purpose: Automatic posture scanning, secure score, and prioritized recommendations

## Key Learnings & Zero-Trust Principles
- **Never trust, always verify**: Deny all inbound by default, allow only explicit trusted sources (my IP for SSH)  
- **Least privilege & micro-segmentation**: NSG rules restrict traffic to/from subnet  
- **Assume breach**: Outbound allowed but explicit; inbound heavily restricted  
- **Visibility**: Defender CSPM gives posture score + recommendations without extra cost  
- **IP management**: SSH rule tied to public IP — requires update if IP changes (future: Bastion/JIT)

## Challenges & Fixes
- Defender onboarding delay: Took several hours for full scan (common on new subscriptions)  
- IP mistake: Initially used private IP — fixed to public IP for external access  
- Rule priority: Learned lower number = higher priority (overrides defaults)

## Future Enhancements (Project 2+)
- Automate with Terraform (IaC)  
- Deploy secure AKS cluster  
- Add Azure Sentinel + agentic AI threat hunting  
- Implement Just-In-Time VM access & Azure Bastion  
- Address Defender recommendations (encryption, tags, JIT)

This project proves practical cloud security skills: from subscription creation to network hardening and posture monitoring — ready for junior/mid-level Azure Security Engineer interviews.

Open to feedback!  
Connect: [Your LinkedIn / X handle if you want]
