
# Windows Network Troubleshooting Lab

## Overview

In this lab, I worked through a Windows 11 workstation with multiple network configuration issues.

The goal was to troubleshoot the problem systematically instead of assuming there was a single cause. I used built-in Windows networking tools to test the local TCP/IP stack, gateway connectivity, external connectivity, DNS resolution, routing, and active network connections.

The lab was completed in a Windows 11 virtual machine running in VMware Fusion.

## Environment

- Windows 11 Enterprise
- VMware Fusion
- Windows PowerShell
- Windows network settings

## Scenario

A user reports that their workstation cannot reliably access websites or network resources.

The workstation appears to have a network connection, but external communication and name resolution are not working properly.

The objective was to determine whether the problem was related to:

- the local network adapter
- TCP/IP configuration
- the default gateway
- internet connectivity
- DNS
- routing
- or an application-level network connection

