# Overzicht
## [Wat is Site Recovery?](site-recovery-overview.md)
## [Hoe werkt Site Recovery?](site-recovery-azure-to-azure-architecture.md)
## [Hoe werkt Hyper-V-replicatie naar Azure?](site-recovery-hyper-v-azure-architecture.md)
## [Welke workloads kunt u beveiligen?](site-recovery-workload.md)
## [Ondersteuningsmatrix voor Site Recovery](site-recovery-support-matrix-azure-to-azure.md)
## [Veelgestelde vragen](site-recovery-faq.md)
## [Een inleiding bekijken](https://azure.microsoft.com/resources/videos/index/?services=site-recovery)

# Aan de slag
## [Virtuele Azure-machines repliceren (preview)](site-recovery-azure-to-azure.md)
## [Virtuele VMware-machines repliceren naar Azure](site-recovery-vmware-to-azure.md)
## [Fysieke servers repliceren naar Azure](site-recovery-physical-servers-to-azure.md)
## [Virtuele Hyper-V-machines repliceren naar Azure (met VMM)](site-recovery-vmm-to-azure.md)
## [Virtuele Hyper-V-machines repliceren naar Azure](site-recovery-hyper-v-site-to-azure.md)
## [Virtuele Hyper-V-machines repliceren naar een secundaire site (met VMM)](site-recovery-vmm-to-vmm.md)
## [Virtuele VMware-machines en fysieke servers repliceren naar een secundaire site](site-recovery-vmware-to-vmware.md)
## [Virtuele VMware-machines repliceren naar Azure in een multitenant-implementatie (CSP)](site-recovery-multi-tenant-support-vmware-using-csp.md)

# Procedures
## Plannen
### [Vereisten voor Azure-replicatie](site-recovery-azure-to-azure-prereq.md)
### [Uitgaande netwerkverbindingen plannen voor virtuele Azure-machines (preview)](site-recovery-azure-to-azure-networking-guidance.md)
### [Netwerkinfrastructuur voor on-premises machines plannen](site-recovery-network-design.md)
### [Netwerktoewijzing plannen](site-recovery-network-mapping-azure-to-azure.md)
### [Capaciteit plannen en schalen voor VMware-replicatie naar Azure](site-recovery-plan-capacity-vmware.md)
### [Implementatieplanner voor VMware-replicatie naar Azure](site-recovery-deployment-planner.md)
### [Capacity Planner voor Hyper-V-replicatie](site-recovery-capacity-planner.md)
### [VM-replicatie beheren met op rollen gebaseerde toegang](site-recovery-role-based-linked-access-control.md)

## Configureren
### [De bronomgeving instellen](site-recovery-set-up-vmware-to-azure.md)
### [De doelomgeving instellen](site-recovery-prepare-target-vmware-to-azure.md)
### [Replicatie-instellingen configureren](site-recovery-setup-replication-settings-vmware.md)
### [De Mobility-service voor VMware-replicatie implementeren](site-recovery-vmware-to-azure-install-mob-svc.md)
#### [De Mobility-service implementeren met behulp van System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
#### [De Mobility-service implementeren met behulp van Azure Automation DSC](site-recovery-automate-mobility-service-install.md)
### [Replicatie inschakelen](site-recovery-replicate-azure-to-azure.md)
## Failover en failback
### [Herstelplannen instellen](site-recovery-create-recovery-plans.md)
#### [Azure-runbooks aan herstelplannen toevoegen](site-recovery-runbook-automation.md)
### [Een testfailover uitvoeren](site-recovery-test-failover-to-azure.md)
### [Door failover beveiligde machines](site-recovery-failover.md)
### [Machines opnieuw beveiligen na een failover](site-recovery-how-to-reprotect-azure-to-azure.md)
### [Failback vanaf Azure](site-recovery-failback-azure-to-vmware.md)

## Migreren
### [Migreren naar Azure](site-recovery-migrate-to-azure.md)
### [Migreren tussen Azure-regio's](site-recovery-migrate-azure-to-azure.md)
### [AWS Windows-instanties migreren naar Azure](site-recovery-migrate-aws-to-azure.md)
### [Gemigreerde machines naar een andere Azure-regio repliceren](site-recovery-azure-to-azure-after-migration.md)

## Workloads
### [Active Directory en DNS](site-recovery-active-directory.md)
### [SQL Server](site-recovery-sql.md)
### [SharePoint](site-recovery-sharepoint.md)
### [Dynamics AX](site-recovery-dynamicsax.md)
### [RDS](site-recovery-workload.md#protect-rds)
### [Exchange](site-recovery-workload.md#protect-exchange)
### [SAP](site-recovery-workload.md#protect-sap)
### [Webtoepassingen op basis van IIS](site-recovery-iis.md)
### [Citrix XenApp en XenDesktop](site-recovery-citrix-xenapp-and-xendesktop.md)
### [Andere workloads](site-recovery-workload.md#workload-summary)
## Replicatie automatiseren
### [Hyper-V-replicatie naar Azure automatiseren (zonder VMM)](site-recovery-deploy-with-powershell-resource-manager.md)
### [Hyper-V-replicatie naar Azure automatiseren (met VMM)](site-recovery-vmm-to-azure-powershell-resource-manager.md)
### [Hyper-V-replicatie naar een secundaire site automatiseren (met VMM)](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
## Beheren
### [Replicatie-instellingen bewerken](site-recovery-setup-replication-settings-vmware.md#edit-replication-policy.md)
### [Processervers in Azure beheren](site-recovery-vmware-setup-azure-ps-resource-manager.md)
### [De configuratieserver beheren](site-recovery-vmware-to-azure-manage-configuration-server.md)
### [Uitgeschaalde processervers beheren](site-recovery-vmware-to-azure-manage-scaleout-process-server.md)
### [VCenter-servers beheren](site-recovery-vmware-to-azure-manage-vCenter.md)
### [Servers verwijderen en beveiliging uitschakelen](site-recovery-manage-registration-and-protection.md)
## Controleren en problemen oplossen
### [Problemen met replicatie van een virtuele Azure-machine](site-recovery-azure-to-azure-troubleshoot-errors.md)
### [Problemen met replicatie van on-premises naar Azure](site-recovery-monitoring-and-troubleshooting.md)

# Naslaginformatie
## [PowerShell](/powershell/module/azurerm.siterecovery)
## [PowerShell klassiek](/powershell/module/azure/?view=azuresmps-3.7.0)
## [REST](https://msdn.microsoft.com/en-us/library/mt750497)

# Verwant
## [Azure Automation](/azure/automation/)

# Bronnen
## [Leertraject](https://azure.microsoft.com/documentation/learning-paths/site-recovery/)
## [Forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hypervrecovmgr)
## [Blog](http://azure.microsoft.com/blog/tag/azure-site-recovery/)
## [Prijzen](https://azure.microsoft.com/pricing/details/site-recovery/)
## [Service-updates](https://azure.microsoft.com/updates/?product=site-recovery)
