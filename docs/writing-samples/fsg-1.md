---
title: "Module 1 Retrofit Guide"
description: "Anonymized excerpt from a field service upgrade guide."
hide:
  - toc
---

!!! info "Confidentiality and Scope"
    The following excerpt is anonymized and adapted from a field service manual. Proprietary product names, serial numbers, part numbers, PCB diagrams, and images have been removed to protect intellectual property.

## test header

more text

```mermaid
flowchart LR
    subgraph Panel["Side Access Panel (Removable)"]
        WP["Replacement Contact PCBA<br/><i>[PART-NUM-NEW]</i><br/>Exposed Spring Pins"]
    end

    subgraph Chassis["Platform Enclosure"]
        CB["Chassis Contact Block<br/><i>Routed via Wire Channel</i>"]
        
        subgraph Board["Main Controller Interconnect Board (<i>[REV-NEW]</i>)"]
            JA["Interlock Header [J-A]<br/><i>Window Loop</i>"]
            JB["Interlock Header [J-B]<br/><i>Factory Jumper (Closed)</i>"]
            LOGIC{"Interlock<br/>Circuit Check"}
        end
    end

    AUX["UV / Filtration Module<br/><i>(AUX Control Line)</i>"]

    WP <== "Physical Mating<br/>(Panel Seated)" ==> CB
    CB -- "2-Pin Wire Harness" --> JA
    JA --> LOGIC
    JB --> LOGIC
    LOGIC -- "Circuit Closed = Safe to Operate<br/>Circuit Open = Power Inhibited" --> AUX
```