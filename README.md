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

## 1. **Created Resource Group** 📁  
   Name: `proj1-hardened-landing-zone-rg` | Region: UK South  
   [Screenshot: RG creation success](screenshots/003-resource-group-created-success.png)

## 2. **Built Virtual Network (VNet)** 🌐  
   Name: `proj1-vnet` | Address space: 10.0.0.0/16 | Subnet: default (10.0.0.0/24)
   <img width="610" height="721" alt="image" src="https://github.com/user-attachments/assets/e2baa4e4-e2e3-461f-abce-c0279f51bf15" />
      
## 3. **Created & Attached NSG** 🛡️  
   Name: `proj1-nsg` | Attached to `default` subnet
   <img width="789" height="382" alt="image" src="https://github.com/user-attachments/assets/aa5a5564-15a0-40b3-ad10-7e196a99a9a0" />
   <img width="1111" height="727" alt="image" src="https://github.com/user-attachments/assets/9e66534a-e611-4569-9998-5b91bdb28275" />
   <img width="1098" height="697" alt="image" src="https://github.com/user-attachments/assets/2ef12d3d-355d-4c1f-9568-6a33f7ebf873" />

## 4. **Locked Down Inbound Rules** 🚫→✅  
   - Priority 100: **Deny-All-Inbound-Internet** (Any → Deny)  
   <img width="589" height="775" alt="image" src="https://github.com/user-attachments/assets/a41d40ba-933d-4420-b1d4-89c6b852685e" />
   <img width="1426" height="373" alt="image" src="https://github.com/user-attachments/assets/832b16be-7f6e-499d-96c8-14760531a86d" />
   
   - Priority 110: **Allow-SSH-Inbound** (only my public IP → port 22 TCP → Allow)
   <img width="559" height="814" alt="image" src="https://github.com/user-attachments/assets/0440f3f2-2e80-4f4c-bfcb-5362c4b7c7de" />
   <img width="1452" height="429" alt="image" src="https://github.com/user-attachments/assets/4b8d7f09-6a9e-448f-81c3-15dfcff2a578" />
   <img width="564" height="670" alt="image" src="https://github.com/user-attachments/assets/f2d6cb0c-c9c3-472b-9e17-967efb6d7e80" />

## 5. **Controlled Outbound Traffic** 🌍  
   Priority 120: **Allow-Outbound-Internet** (Any → Allow)  
   <img width="552" height="766" alt="image" src="https://github.com/user-attachments/assets/8e47cfd2-e5b7-46c0-9c01-3a0b22fcf3d4" />
   <img width="1663" height="391" alt="image" src="https://github.com/user-attachments/assets/4d243fc3-982f-4283-a14a-e45a9eb83b21" />

## 6. **Enabled Microsoft Defender for Cloud (Free CSPM)** 👀  
   Free posture management onboarded → 2 resources scanned, 0 critical alerts, 6 recommendations  
   <img width="1885" height="796" alt="image" src="https://github.com/user-attachments/assets/3cafcdfa-2924-49e5-a8ab-4597bc3e2710" />
   <img width="1914" height="766" alt="image" src="https://github.com/user-attachments/assets/f1214a8f-5ce5-4cce-82d6-7e52ae07715e" />
   <img width="1644" height="637" alt="image" src="https://github.com/user-attachments/assets/e97d2f7d-cd1d-486f-b344-197145f9a0af" />

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
