# Proxmox VE Cloud-init VM Template for Ubuntu24.04 LTS

## Summary
This Ubuntu24.04 Template includes essential packages and tools for a development environment.
Details are listed below

| Name | versions | how it was installed |
| ---- | -------- | -------------------- |
| Git  | Latest Version | ```apt-get upgrade``` |
| Docker | Latest LTS Version | from **Docker CE** Repository |
| net-tools | - | ```apt-get install net-tools``` |
| tree | - | ```apt-get install tree``` |
| gcc / g++ | Latest Version | ```apt-get install build-essential``` |
| GNU make | Latest Version | ```apt-get install build-essential``` |
| Node.js / npm | Latest LTS Version | from **NodeSource** Repository |
| openJDK | Latest Version| ```apt-get install openjdk-21-jdk``` |

## Srcipt Design Philosophy

### **Why the Memory is Set to 5GiB?**
- When I was developing this script, my own development typically used arround 3 - 4 GiB of memory.
  To give it some extra breathing room, I set to allocate 5 GiB.

---

### **Why does the wait loop use a 5-minute (300 seconds) timeout?**
- In practice, initialization tasks usually take between 2 and 4 minutes.
  To avoid false timeouts, the upper bound is set to 5 minutes.

---

### Why are the OS initialization (ci-vendor) and the development environment setup separated?
1. **Clear separation of responsibilities**  
   - `ci-vendor` handles initial OS configuration.  
   - The service script handles the development environment setup.  
   This improves maintainability and reduces coupling.

2. **Kernel update consistency**  
   `ci-vendor` performs `apt-get update` and `apt-get upgrade` (including kernel updates).  
   Performing a restart before installing Docker prevents kernel-version mismatches.

3. **Faster provisioning workflow**  
   After the first reboot, SSH access becomes available sooner.  
   This avoids unnecessary delays during VM creation.

### **Why is this template besed on cloud-init instead of using Packer?**
SIMPLY BECAUSE I WASNT AWARE OF Packer AT THE TIME.
I LOOKED IT UP, AND IT'S SUPRE CONVIENIENT!!!
**I absolutely plan to adopt it in the future.**
