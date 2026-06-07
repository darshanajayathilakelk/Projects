# ESXi Migration Project: v5.5 to v6.5 | Cisco UCS to HP C7000 Blades
**Timeline:** Jan 2017 – May 2017  
**Scope:** ~130 Hosts | Windows vCenter to VCSA | Cisco UCS to HP C7000

---

## Project Overview

End-to-end datacenter infrastructure migration covering two parallel workstreams:

1. **VMware ESXi 5.5 → 6.5** with migration from Windows-based vCenter Server to the vCenter Server Appliance (VCSA)
2. **Cisco UCS blade infrastructure → HP BladeSystem C7000** chassis migration

The project was executed in phases across 2016–2017, with zero unplanned downtime for production workloads.

---

## Scope

| Item | Detail |
|------|--------|
| Total ESXi Hosts | ~130 |
| vCenter Servers | 3  
| Cisco UCS Chassis 
| HP C7000 Chassis | 4 x C7000 |
| Blade Servers | HP ProLiant BL460c Gen9 |
| VM Count | ~5000 VMs |
| Datacenters | 3 

---

## Workstream 1 — ESXi 5.5 to 6.5 Upgrade

### Objectives
- Upgrade all ESXi hosts from 5.5 U3 to 6.5 U1
- Migrate Windows vCenter 5.5 to VCSA 6.5
- Retain all existing clusters, resource pools, and DRS/HA configurations
- Upgrade VMware Tools and VM hardware compatibility levels post-migration

### Phases

#### Phase 1 — Assessment & Planning (Q1 2016)
- Audited all hosts for hardware compatibility with ESXi 6.5 HCL
- Identified deprecated drivers and NICs requiring remediation
- Documented all vCenter plugins and third-party integrations (vROps, SRM, vDP)
- Firmware upgrade
- HP Chassis configuration
- Created host upgrade runbooks and rollback procedures

#### Phase 2 — VCSA Migration (Q2 2016)
- Deployed VCSA 6.5 appliances alongside existing Windows vCenter instances
- Used VMware Migration Assistant tool for in-place Windows vCenter → VCSA migration
- Migrated in non-production environment first;
- Production vCenter migration executed during a Saturday maintenance window


#### Phase 3 — Host Upgrades (Q3 2016 – Q2 2017)
- Upgraded hosts cluster-by-cluster using vSphere Update Manager (VUM)
- Evacuated VMs via vMotion prior to each host upgrade (zero VM downtime)
- Upgrade batch size: 10 hosts per maintenance window
- Validated networking (vDS), storage multipath, and HA/DRS post each batch

#### Phase 4 — VM Hardware Upgrades (Q3–Q4 2017)
- Upgraded VMware Tools on all ~5000 VMs
- Upgraded VM hardware version from v9/v10 → v13 (in waves, by criticality)
- Tested application compatibility before and after each wave

---

## Workstream 2 — Cisco UCS to HP C7000 Blade Migration

### Objectives
- Decommission Cisco UCS chassis
- Procure and rack HP BladeSystem C7000 chassis with BL460c Gen9 blades
- Re-home all ESXi hosts and VMs onto new HP blade infrastructure
- Maintain redundancy and HA throughout migration

### Phases

#### Phase 1 — Infrastructure Procurement & Build (Q1–Q2 2016)
- Scoped and ordered HP C7000 chassis, BL460c Gen9 blades, Virtual Connect FlexFabric modules
- Racked, cabled, and configured C7000 chassis (OA, VC, power, cooling)
- Configured HP Virtual Connect profiles to match existing network/storage connectivity
- Deployed ESXi 6.5 baseline image via HP SPP (Service Pack for ProLiant)

#### Phase 2 — Pilot Migration (Q3 2016)
- Selected 10 non-production UCS hosts as pilot
- Migrated VMs off UCS hosts via vMotion to temporary capacity
- Decommissioned UCS hosts, re-provisioned equivalent capacity on HP C7000
- Added new HP blades to existing vSphere clusters; validated performance baselines

#### Phase 3 — Production Migration (Q4 2016 – Q2 2017)
- Migrated production hosts in rolling batches (10–15 hosts per window)
- Coordinated storage (EMC/NetApp) re-zoning with storage team for each batch
- Updated vDS uplink assignments and NIC teaming policies for HP FlexFabric profile
- Verified UCS host removal from UCS Manager and updated CMDB records

#### Phase 4 — UCS Decommission (Q3 2017)
- Full decommission of all  UCS  chassis and Fabric Interconnects
- Removed UCS from Cisco UCS Manager domains
- Returned hardware to leasing vendor / arranged asset disposal
- Closed out all network and storage configurations tied to UCS

---

## Key Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| vCenter SSO corruption during VCSA migration | Full snapshot + backup of Windows vCenter pre-migration |
| ESXi 6.5 driver incompatibility | Pre-validated all hosts against VMware HCL; async driver updates staged via VUM |
| Network profile mismatch (UCS → HP VC) | Lab-validated HP VC profiles before production rollout |
| Storage connectivity loss during blade swap | Per-host zoning changes coordinated with storage team in each batch window |
| Extended maintenance window overrun | Parallel runbooks per team (VMware, network, storage, server) with clear go/no-go checkpoints |

---

## Team & Stakeholders

Project management
Datacenter Team
Wintel team
Storage team
Network team
Change Management
Security team
Audit team

---

## Tools & Technologies

- VMware vSphere 5.5 / 6.5, VCSA, vSphere Update Manager
- VMware vROps, Site Recovery Manager (SRM)
- Cisco UCS Manager
- HP BladeSystem C7000, BL460c Gen9, Virtual Connect FlexFabric
- HP OneView, HP Service Pack for ProLiant (SPP)
- Hitachi 


