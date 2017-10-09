# PT Activity 5.5.3: Troubleshooting Spanning Tree Protocol

![Imgur](https://i.imgur.com/d9SoMRS.png)

![Imgur](https://i.imgur.com/RFy622t.png)

### Learning Objectives

• Identify the initial state of all trunks

• Correct the source of the problem

• Document the switch configuration

### Scenario

- You are responsible for the operation of the redundant switched LAN shown in the topology diagram. You
and your users have been observing increased latency during peak usage times, and your analysis points
to congested trunks. You recognize that of the six trunks configured, only two are forwarding packets in
the default STP configuration currently running. The solution to this problem requires more effective use
of the available trunks.

- This activity is complete when all wired trunks are carrying traffic, and all three switches are participating
in per-VLAN load balancing for the three user VLANs.

### Task 1: Identify the Initial State of All Trunks

On each of the switches, display the spanning tree table with the show spanning-tree command. Note
which ports are forwarding on each switch, and identify which trunks are not being used in the default
configuration. You can use your network topology drawing to document the initial state of all trunk ports.

### Task 2: Correct the Source of the Problem

Modify the spanning tree configuration so that all three trunks are in use. Assume that the three user
LANs (10, 20, and 30) carry an equal amount of traffic. Aim for a solution that will have a different set of
ports forwarding for each of the three user VLANs.

In order for the activity to be correctly graded, you must meet the following guidelines:

• S1 is root for VLAN 10 (priority 4096) and backup root for VLAN 20 (priority 16384)
• S2 is root for VLAN 20 (priority 4096) and backup root for VLAN 30 (priority 16384)
• S3 is root for VLAN 30 (priority 4096) and backup root for VLAN 10 (priority 16384)

### Task 3: Document the Switch Configuration

When you have completed your solution, capture the output of the show run command and save it to a
text file for each switch.