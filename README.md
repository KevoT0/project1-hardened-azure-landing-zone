# project1-hardened-azure-landing-zone

# Project 1: Hardened Azure Landing Zone – Zero-Trust Vibes 🚀🔒

**Goal**  
Build a clean, locked-down Azure landing zone from scratch using real zero-trust principles!  
Deny everything by default, only allow trusted access, control outbound traffic, and turn on free posture monitoring with Defender for Cloud.  

This is my first original security project — no copy-paste labs here 😤

**Date** : February 2026  
**Tools** : Azure Portal only (no Terraform yet – that's Project 2 baby!)  
**Resources created** : Subscription, RG, VNet, NSG + custom rules, Defender for Cloud (free CSPM)

## Architecture at a glance 🗺️
- Subscription: Fresh pay-as-you-go with £200 free credit  
- Resource Group: `proj1-hardened-landing-zone-rg`  
- VNet: `proj1-vnet` (10.0.0.0/16 private IPs) + `default` subnet  
- NSG: `proj1-nsg` attached to subnet  
  → Inbound: Deny all public except SSH from **my IP only**  
  → Outbound: Allow internet for updates & packages  
- Defender for Cloud: Free CSPM enabled (posture scanning + recommendations)

## Step-by-Step Build – Let's go! 🛠️

1. **Created Resource Group** 📁  
   Name: `proj1-hardened-landing-zone-rg` | Region: UK South  
   [Screenshot: RG creation success](screenshots/003-resource-group-created-success.png)

2. **Built Virtual Network (VNet)** 🌐  
   Name: `proj1-vnet` | Address space: 10.0.0.0/16 | Subnet: default (10.0.0.0/24)  
   [Screenshot: VNet deployment success](https://github.com/KevoT0/project1-hardened-azure-landing-zone/blob/main/1%20(zero%20trust).png )  
   [Screenshot: VNet inside RG](screenshots/005-vnet-inside-rg.png)

3. **Created & Attached NSG** 🛡️  
   Name: `proj1-nsg` | Attached to `default` subnet  
   [Screenshot: NSG association success](screenshots/008-nsg-associated-success.png)

4. **Locked Down Inbound Rules** 🚫→✅  
   - Priority 100: **Deny-All-Inbound-Internet** (Any → Deny)  
   - Priority 110: **Allow-SSH-Inbound** (only my public IP → port 22 TCP → Allow)  
   [Screenshot: Inbound rules list with Deny rule](screenshots/011-inbound-rules-list-with-deny.png)  
   [Screenshot: SSH rule with my public IP](screenshots/013-ssh-rule-with-public-ip-updated.png)

5. **Controlled Outbound Traffic** 🌍  
   Priority 120: **Allow-Outbound-Internet** (Any → Allow)  
   [Screenshot: Outbound rules list](screenshots/014-outbound-allow-internet-added.png)

6. **Enabled Microsoft Defender for Cloud (Free CSPM)** 👀  
   Free posture management onboarded → 2 resources scanned, 0 critical alerts, 6 recommendations  
   [Screenshot: Defender Overview](screenshots/015-defender-overview-onboarded.png)  
   [Screenshot: Recommendations list](screenshots/016-defender-recommendations-loaded.png)  
   [Screenshot: Setup page – onboarded](screenshots/017-defender-setup-onboarded.png)

## What I Learned (Zero-Trust Mindset Unlocked) 🧠💡
- **Never trust, always verify** – Deny all inbound first, then allow only what I explicitly trust (my IP for SSH)  
- **Priority is king** – Lower number = checked first (100 Deny beats 65000 defaults)  
- **Public vs Private IP** – NSG rules need your **public** IP for external access  
- **Defender CSPM** – Free posture score + recommendations, even on a brand-new sub  
- **IP changes suck** – SSH rule must be updated if my home IP changes (future fix: Bastion or JIT)

## Challenges I Fixed Like a Boss 🛠️😤
- Defender took hours to load – normal for new subs, just waited it out  
- Accidentally used private IP first – caught it, switched to public IP  
- Learned NSG rule order the hard way – now I know why priority matters!

## Future Plans (Project 2 & Beyond) 🔥
- Automate everything with Terraform (IaC baby!)  
- Deploy secure AKS cluster with image scanning & Key Vault secrets  
- Add Sentinel + agentic AI for smart threat hunting  
- Implement Just-In-Time VM access & Azure Bastion  
- Fix Defender recommendations (encryption, tags, etc.)

This is my first original security project — built from scratch, no copy-paste.  
Ready for junior/mid-level Azure Security Engineer interviews 💼

Feedback, roast, or collab welcome!  
Connect with me: [Your LinkedIn / X handle here]

#Azure #CloudSecurity #ZeroTrust #Cybersecurity #Portfolio
