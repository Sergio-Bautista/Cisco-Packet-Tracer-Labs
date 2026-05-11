# Lab1: Minimal Two-PC Connection

## OVERVIEW
Build a minimal two-PC network through a single switch and verify end-to-end ping.

## TOPOLOGY
**PC0** ──── **Switch0** ──── **PC1**  
*(Network: 192.168.1.0/24)*

## OBJECTIVES
1. **Initialize Workspace:** Open Packet Tracer and add 2 PCs and 1 2960 switch to the workspace.
2. **Cabling:** Connect each PC to the switch using straight-through copper cables.
3. **Addressing:** Assign static IPv4 addresses:
    * **PC0** → `192.168.1.10/24`
    * **PC1** → `192.168.1.20/24`
4. **Testing:** Open the Command Prompt on PC0 and run: `ping 192.168.1.20`
5. **Verification:** Confirm 4 successful replies with 0% packet loss.

---

## CLI HINTS
* **On a PC:** Desktop tab → IP Configuration → set IP and subnet mask.
* **Ping:** Desktop → Command Prompt.
* **Switch Observation:** Use `show mac address-table` on the switch to observe learned MACs.

## KEY SKILLS
* IP addressing
* Straight-through cables
* Ping
* Switch basics

> [!TIP]
> **PRO TIP:** If ping fails, check cables are connected to correct port types and IPs are in the same subnet.