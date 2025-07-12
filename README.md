# ADAPTOR

# 📘 Action Plan for Phase 1: Literature Review

**🎯 Objective:**  
To gain a deep understanding of the existing research in network-aware scheduling and SDN-based control for distributed systems, in order to precisely define the contribution of your thesis and inform your design decisions for RQ1, RQ2, and RQ3.

---

## 🔍 Key Areas of Focus (as per the proposal)

- **Network-Aware Scheduling**
- **Traffic Engineering in Data Centers**
- **SDN Applications in Edge/Fog Computing**

---

## 🧩 Area 1: Network-Aware Scheduling

This is the core of your project. You need to understand how schedulers have evolved to consider the network.

### 📌 What to Investigate
- **Classic "Network-Agnostic" Schedulers:** e.g., Hadoop YARN, Kubernetes default scheduler, Slurm
- **Early Network-Aware Approaches:** Data locality-based strategies
- **Advanced Scheduling Algorithms:** Explicit modeling of network performance
- **Metrics and Cost Functions:** Solutions to RQ2—latency, bandwidth, jitter, congestion, etc.

### 🔑 Keywords for Academic Search
- `network-aware scheduling`
- `topology-aware task placement`
- `joint scheduling and routing`
- `co-flow scheduling`
- `data locality` + `scheduler`
- `deadline-aware scheduling` + `distributed systems`

---

## 🧩 Area 2: Traffic Engineering (TE) and Network State

Informs **RQ1** (Network State Abstraction) and **RQ3** (Control Plane Logic).

### 📌 What to Investigate
- **TE in Data Centers:** Hedera, SWAN, B4
- **Network State Monitoring:**  
  - *Passive Monitoring:* e.g., OpenFlow stats  
  - *Active Probing:* e.g., ping, iperf  
  - *In-band Network Telemetry (INT)*
- **Contrast with Traditional TE:** RSVP-TE, OSPF, EIGRP (from CCNP knowledge)

### 🔑 Keywords for Academic Search
- `traffic engineering` + `data center networks`
- `SDN` + `traffic engineering`
- `network monitoring` + `SDN`
- `available bandwidth estimation`
- `network state abstraction` + `SDN`
- `Google B4`, `Microsoft SWAN`, `Facebook Express Backbone`

---

## 🧩 Area 3: SDN Applications in Edge/Fog Computing

This provides the architectural pattern for your proposed system.

### 📌 What to Investigate
- **SDN Controller Architectures:** Ryu, POX, ONOS
- **Edge/Fog Computing Schedulers**
- **Use of Mininet in Research** (for simulation/emulation)

### 🔑 Keywords for Academic Search
- `SDN` + `edge computing` + `resource allocation`
- `fog computing` + `task scheduling`
- `Ryu controller` + `application` or `use case`
- `Mininet` + `SDN` + `performance evaluation`
- `service placement` + `edge network`

---

## 📅 Workflow and Deliverables for Phase 1

### 🧰 Tool Setup
- Use **Zotero** or **Mendeley** (mandatory)
- Install browser extension for 1-click saving

---

### 🗓️ Week-by-Week Plan

**Week 1: Broad Survey**
- Find 2–3 recent survey papers per area
- Map the field and extract terminology

**Week 2: Deep Dive**
- Collect 10–15 highly relevant papers using the keywords
- Read abstracts, filter, and save to Zotero

**Week 3: Synthesize and Annotate**
- Read in detail and annotate each paper:
  - Problem addressed?
  - Proposed method/cost function?
  - Evaluation setup?
  - Limitations/assumptions?

**Week 4: Structure and Write**
- Begin outlining & drafting your chapters

---

## 📦 Phase 1 Deliverables

- 📚 **Annotated Bibliography**  
  Structured list of reviewed papers + summaries (for appendix or supervisor review)

- 🧠 **State-of-the-Art Summary (2–4 pages)**  
  Should include:
  - 3 major sections matching key areas
  - ✅ *“Identified Research Gap and Project Positioning”* section at the end

- 📝 **Draft of Thesis Chapters**  
  - Chapter 1: Introduction  
  - Chapter 2: Related Work

- 🎯 **Refined Set of Research Questions**  
  Adjust based on learnings from the literature
