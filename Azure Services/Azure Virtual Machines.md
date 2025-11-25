# Azure Virtual Machines (VMs)

> **Exam Weight:** High  
> **Estimated Study Time:** 45-60 minutes

## 📋 Overview

Azure Virtual Machines are on-demand, scalable computing resources that give you the flexibility of virtualization without having to buy and maintain physical hardware. VMs are an Infrastructure as a Service (IaaS) offering that allows complete control over the operating system and environment.

**Why This Matters for AZ-900:**
- VMs are a fundamental compute service and frequently appear in exam scenarios
- Understanding when to use VMs vs other compute options (App Services, Functions) is critical
- VM pricing, availability, and configuration are common exam topics

---

## 🎯 Key Concepts

### What is a Virtual Machine?

An Azure VM is a software emulation of a physical computer that runs an operating system and applications. You have full control over the configuration, including the OS, software installed, and security settings.

**Example:**
A company wants to run a legacy Windows Server 2012 application that requires specific software configurations. They create an Azure VM with Windows Server 2012, install their application, and have complete control over the environment - just like having a physical server in their datacenter.

**Key Points:**
- You select the VM size (CPU, memory, storage)
- You choose the operating system (Windows, Linux distributions)
- You're responsible for patching, updates, and maintenance
- Charged by the hour/minute while the VM is running

### VM Sizes and Series

Azure offers different VM sizes optimized for various workloads.

**Common Series:**
- **B-Series (Burstable):** Cost-effective for workloads that don't need continuous CPU performance
- **D-Series (General Purpose):** Balanced CPU-to-memory ratio, good for most applications
- **F-Series (Compute Optimized):** High CPU-to-memory ratio, ideal for web servers
- **E-Series (Memory Optimized):** High memory-to-CPU ratio, great for databases
- **N-Series (GPU):** For graphics rendering and machine learning

**When to Use:**
- Need full control over the operating system
- Running applications that require specific software or configurations
- Lift-and-shift migrations from on-premises
- Testing and development environments

**When NOT to Use:**
- For simple web applications (consider App Services instead)
- Event-driven workloads (consider Azure Functions)
- When you don't want to manage infrastructure (consider PaaS options)

---

## 🔄 How It Works

Creating and using an Azure VM follows this general process:

1. **Choose VM Configuration:** Select region, size, operating system image
2. **Configure Networking:** Set up virtual network, subnet, public IP (optional), NSG rules
3. **Configure Storage:** Choose OS disk type (Standard HDD, SSD, Premium SSD)
4. **Set Authentication:** Configure admin username/password or SSH keys
5. **Deploy VM:** Azure provisions the resources
6. **Connect & Use:** RDP (Windows) or SSH (Linux) to access your VM

```
User Request → Azure Resource Manager → 
Allocate Compute → Configure Network → Attach Storage → 
Start VM → User Connects via RDP/SSH
```

---

## 💰 Pricing Considerations

Azure VM pricing can be complex but understanding the basics is important for the exam.

- **Pricing Model:** Pay-per-minute while VM is running (compute charges)
- **Cost Factors:** 
  - VM size (more vCPUs and memory = higher cost)
  - Storage type and size
  - Bandwidth (outbound data transfer)
  - Running time (stopped/deallocated VMs don't incur compute charges but storage remains)
- **Free Tier:** 750 hours/month of B1S Windows or Linux VM for first 12 months
- **Cost Savings:** 
  - Reserved Instances (1 or 3 year commitment, up to 72% savings)
  - Azure Hybrid Benefit (use existing Windows licenses)
  - Spot VMs (discounted unused capacity, can be evicted)

**Exam Tip:** Know that stopping a VM from the Azure portal (deallocated state) stops compute charges, but storage charges continue.

---

## 🔗 Related Services & Concepts

**Works Well With:**
- **Azure Virtual Network** - VMs require a VNet for networking
- **Azure Load Balancer** - Distribute traffic across multiple VMs
- **Azure Backup** - Backup and disaster recovery for VMs
- **Availability Sets/Zones** - High availability configurations

**Compare With:**
- **Azure App Service:** App Service is PaaS (less management), VMs are IaaS (full control)
  - Choose App Service for web apps when you don't need OS-level control
  - Choose VMs when you need specific configurations or legacy applications
- **Azure Container Instances:** Containers are lighter weight and faster to start
  - Choose VMs when you need persistent state and full OS
  - Choose containers for microservices and stateless applications

---

## ⚠️ Common Misconceptions & Exam Traps

1. **Misconception:** "Stopping a VM from the OS stops all charges"
   - **Reality:** You must deallocate the VM from Azure portal to stop compute charges; storage charges always apply
   - **Exam Tip:** Questions may ask about minimizing costs - remember deallocation vs simple shutdown

2. **Misconception:** "VMs are always the best choice for compute"
   - **Reality:** VMs require more management; PaaS services like App Service are better for standard web apps
   - **Exam Tip:** Scenario questions will test whether you choose IaaS vs PaaS appropriately

3. **Watch Out For:** Questions about high availability - understand that a single VM does NOT provide high availability; you need Availability Sets, Availability Zones, or multiple VMs with a load balancer

4. **Misconception:** "All VM data is automatically backed up"
   - **Reality:** You must configure Azure Backup separately; it's not automatic

---

## 📝 Quick Reference Summary

**Essential Facts:**
- ✅ VMs are IaaS - you manage OS, patches, and applications
- ✅ Charged per minute while running; deallocate to stop compute charges
- ✅ Available in multiple sizes/series for different workloads
- ✅ Can run Windows or Linux operating systems
- ✅ Support both public and private IP addresses
- ✅ Require a Virtual Network for connectivity

**Remember:**
- Single VM = no SLA for availability (need multiple VMs in availability set/zone)
- Reserved Instances provide significant cost savings for long-term workloads
- Azure Hybrid Benefit lets you use existing Windows licenses

---

## 🧪 Practice Questions

### Question 1
Your company needs to run a custom Windows Server 2019 application that requires specific registry modifications and third-party software installations. The application must be available 24/7. Which Azure compute service should you recommend?

A) Azure Functions  
B) Azure App Service  
C) Azure Virtual Machines  
D) Azure Container Instances

<details>
<summary>Click to reveal answer</summary>

**Answer: C**

**Explanation:** Azure Virtual Machines is the correct choice because:
- The application requires specific OS-level configurations (registry modifications)
- Third-party software needs to be installed (full control required)
- This is clearly an IaaS scenario requiring complete control over the environment

Why others are wrong:
- **A) Azure Functions:** Serverless, event-driven - not suitable for continuously running applications
- **B) Azure App Service:** PaaS service - doesn't allow registry modifications or arbitrary software installation
- **D) Azure Container Instances:** While possible, containers are better for stateless apps, and the question implies legacy application needing full Windows Server environment

**Key Concept Tested:** Understanding IaaS vs PaaS scenarios and when full VM control is necessary
</details>

### Question 2
You have an Azure VM running in the West US region. You shut down the VM from within the operating system (Windows shutdown). What charges will you continue to incur?

A) No charges - the VM is shut down  
B) Compute and storage charges  
C) Storage charges only  
D) Network charges only

<details>
<summary>Click to reveal answer</summary>

**Answer: B**

**Explanation:** Shutting down from within the OS only stops the operating system, but Azure still considers the VM allocated. You continue to incur both compute and storage charges.

To stop compute charges, you must **deallocate** the VM from the Azure portal, CLI, or PowerShell. Even when deallocated, storage charges for disks continue.

**Key Concept Tested:** Understanding VM billing, stopped vs deallocated states, and cost management
</details>

### Question 3
Your organization wants to minimize costs for a development VM that is only used during business hours (8 AM - 6 PM, Monday-Friday). What should you recommend?

A) Delete and recreate the VM daily  
B) Use Azure Spot VMs  
C) Deallocate the VM outside business hours  
D) Use a smaller VM size

<details>
<summary>Click to reveal answer</summary>

**Answer: C**

**Explanation:** Deallocating the VM when not in use is the best approach:
- Stops compute charges (saves ~70% of total VM cost)
- Preserves the VM configuration and data
- Can be automated with Azure Automation or scripting
- Easy to start up again when needed

Why others are wrong:
- **A)** Deleting/recreating is too complex and risks data loss
- **B)** Spot VMs can be evicted at any time - not suitable for predictable dev schedule
- **D)** Smaller size reduces cost but VM still runs 24/7 incurring charges

**Key Concept Tested:** Cost optimization strategies for VMs
</details>

---

## 🔗 Additional Resources

- [Official Microsoft Documentation](https://docs.microsoft.com/azure/virtual-machines/)
- [Microsoft Learn: Introduction to Azure Virtual Machines](https://learn.microsoft.com/training/modules/intro-to-azure-virtual-machines/)
- [Hands-on Lab](https://portal.azure.com) - Create a free B1S Linux VM and practice connecting via SSH

**Try This:**
1. Create a small B1S VM in the Azure portal
2. Connect to it via RDP (Windows) or SSH (Linux)
3. Stop it from the portal and observe billing stops for compute
4. Practice deallocating and restarting

---

## ✏️ Study Notes

*Use this space for your own notes, insights, or questions as you study:*

- 
- 
- 

---

**Next Topic:** [Azure App Services](app-services.md)  
**Previous Topic:** [Compute Overview](README.md)  
**Back to:** [Azure Services Section](../README.md)