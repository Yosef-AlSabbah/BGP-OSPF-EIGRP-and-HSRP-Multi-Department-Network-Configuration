# BGP-OSPF-EIGRP-and-HSRP-Multi-Department-Network-Configuration

**Student Name:** Yousef Mohammed Yousef Al-Sabbah  
**Student ID:** 120212265  
**Instructor Name:** Malak Ghabayen  

This document outlines the configurations and commands necessary to implement BGP, OSPF, EIGRP, and HSRP routing across a multi-department network topology. It provides a high-level view of configuration commands without specific IP addresses.

---

## Table of Contents

1. [Assignment Overview](#assignment-overview)
2. [Generic Commands for OSPF Configuration](#generic-commands-for-ospf-configuration)
   - [Enable OSPF Routing on Routers](#1-enable-ospf-routing-on-routers)
   - [Verify OSPF Configuration](#2-verify-ospf-configuration)
3. [Specific Department Configurations](#specific-department-configurations)
   - [IT Department (AS-65001)](#it-department-as-65001)
   - [HR Department (AS-65002)](#hr-department-as-65002)
   - [R&D Department (AS-65003)](#rd-department-as-65003)
4. [Core Router Configuration](#core-router-configuration)
5. [EIGRP Configuration for Departments](#eigrp-configuration-for-departments)
6. [Verification Commands](#verification-commands)

---

## Assignment Overview

The goal of this assignment is to configure BGP, OSPF, EIGRP, and HSRP for full network connectivity across three departments connected to a Core Router. The departments are segmented into different subnets and include various routing protocols tailored to their size and complexity. Additionally, BGP is used for communication between departments, with each department treated as an AS, while HSRP is implemented within the HR department for redundancy.

---

## Generic Commands for OSPF Configuration

Below are the high-level steps and commands used to configure OSPF:

### 1. Enable OSPF Routing on Routers
- Enable privileged EXEC mode:
  ```
  enable
  ```
- Enter global configuration mode:
  ```
  configure terminal
  ```
- Start the OSPF process with a specific process ID:
  ```
  router ospf <process-id>
  ```
- Configure networks and associate them with OSPF areas:
  ```
  network <network-ip> <wildcard-mask> area <area-id>
  ```
- (Optional) Manually set the router ID for identification in the OSPF topology:
  ```
  router-id <router-id>
  ```
- Save the configuration:
  ```
  write memory
  ```

### 2. Verify OSPF Configuration
- Check the OSPF neighbor relationships:
  ```
  show ip ospf neighbor
  ```
- Verify the OSPF routing table:
  ```
  show ip route ospf
  ```
- Inspect OSPF database information:
  ```
  show ip ospf database
  ```

---

## Specific Department Configurations

### IT Department (AS-65001)
- Enable EIGRP process:
  ```
  router eigrp <autonomous-system-number>
  ```
- Configure networks:
  ```
  network <network-ip> <wildcard-mask>
  ```
- Redistribute BGP routes into EIGRP:
  ```
  redistribute bgp <as-number>
  ```
- Ensure loopback interfaces are included:
  ```
  network <loopback-ip> 0.0.0.0
  ```

### HR Department (AS-65002)
- Enable EIGRP process:
  ```
  router eigrp <autonomous-system-number>
  ```
- Configure networks for HR routers:
  ```
  network <network-ip> <wildcard-mask>
  ```
- Implement HSRP for redundancy:
  ```
  standby <group-number> ip <virtual-ip>
  standby <group-number> priority <priority-value>
  standby <group-number> preempt
  ```
- Redistribute BGP routes into EIGRP:
  ```
  redistribute bgp <as-number>
  ```

### R&D Department (AS-65003)
- Enable OSPF process:
  ```
  router ospf <process-id>
  ```
- Configure networks for R&D routers:
  ```
  network <network-ip> <wildcard-mask> area <area-id>
  ```
- Redistribute BGP routes into OSPF:
  ```
  redistribute bgp <as-number> subnets
  ```

---

## Core Router Configuration

- Enable OSPF process:
  ```
  router ospf <process-id>
  ```
- Configure inter-department WAN links:
  ```
  network <wan-network-ip> <wildcard-mask> area <area-id>
  ```
- Redistribute BGP routes into OSPF:
  ```
  redistribute bgp <as-number> subnets
  ```
- Enable BGP and configure AS connections:
  ```
  router bgp <core-as-number>
  neighbor <department-router-ip> remote-as <department-as-number>
  ```

---

## EIGRP Configuration for Departments

### IT and HR Departments
- Enable EIGRP process:
  ```
  router eigrp <autonomous-system-number>
  ```
- Configure networks for EIGRP:
  ```
  network <network-ip> <wildcard-mask>
  ```
- Redistribute BGP routes into EIGRP:
  ```
  redistribute bgp <as-number>
  ```
- Configure passive interfaces where necessary:
  ```
  passive-interface <interface>
  ```

---

## Verification Commands

- Verify OSPF neighbor relationships:
  ```
  show ip ospf neighbor
  ```
- Verify EIGRP neighbors:
  ```
  show ip eigrp neighbors
  ```
- Verify the routing table:
  ```
  show ip route
  ```
- Verify HSRP status:
  ```
  show standby brief
  ```
- Verify BGP connections:
  ```
  show ip bgp summary
  ```

---

This document provides a streamlined view of the required configurations for enabling BGP, OSPF, EIGRP, and HSRP across the network topology. Detailed command outputs and configurations are available upon request.

