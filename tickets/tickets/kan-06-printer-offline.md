# KAN-6: Executive Printer Offline After Power Outage

**Priority:** High
**Status:** Resolved
**Category:** Hardware / networking
**Labels:** dhcp-reservation, networking, printer, tcp-ip, windows-11

## Issue
Users on the 2nd floor reported that the executive printer (PRN-EXEC-FL2) showed as "Offline" in Windows after an office power outage. Printing to the device failed, even though the printer's display showed it was powered on and connected to Ethernet.

## Steps Taken
1. Checked the printer's status in the Windows **Print Management** console.
2. Found that the printer's IP address had changed from 192.168.1.200 to 192.168.1.215. The printer had no static DHCP reservation, so it received a new address after the outage.
3. Updated the **TCP/IP port** on the print server to match the new IP address.
4. Created a permanent **DHCP reservation** for the printer's MAC address on the core router/DHCP server so the address can't change again.
5. Sent a test page and confirmed the print queue returned to **Ready**.

## Result
Printing was restored for all users. Ticket resolved.

## Root Cause
The printer relied on a dynamic IP address. After the power outage it received a different address, and the print server was still pointing at the old one.

## Why High Priority
The printer served an executive floor and was offline for all users on it.

## Lessons Learned
- When a printer shows offline but is powered on and connected, check whether its IP address changed.
- Shared devices like printers should have a DHCP reservation or a static IP so power outages don't break them.

![KAN-6 ticket](../images/kan-06.png)
