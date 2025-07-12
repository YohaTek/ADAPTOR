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


  Excellent. Let's execute Phase 2. Here is a detailed, step-by-step action plan to guide you through building your simulation environment. The goal is to be very practical, with specific commands and clear success criteria for each step.

---

### **Action Plan for Phase 2: Simulation Environment Setup**

**Objective:** To build a stable, fully functional virtual laboratory on your laptop that includes a Linux VM, Mininet, and the Ryu SDN controller. By the end of this phase, you will have successfully run a custom network topology managed by an external SDN controller.

---

#### **Task P2.1: Virtual Machine (VM) Setup**

*   **Objective:** Create an isolated and clean Linux environment for all project work. This prevents conflicts with your host OS and makes your setup portable and reproducible.
*   **Recommended Tools:**
    *   **Virtualization Software:** [VirtualBox](https://www.virtualbox.org/) (Free, cross-platform)
    *   **Operating System:** [Ubuntu Desktop 22.04 LTS](https://ubuntu.com/download/desktop) (LTS = Long-Term Support, very stable)
*   **Step-by-Step Actions:**
    1.  **Install VirtualBox:** Download and install the appropriate package for your laptop (Windows, macOS, or Linux).
    2.  **Download Ubuntu ISO:** Get the Ubuntu 22.04 LTS disk image (`.iso` file) from the link above.
    3.  **Create a New VM:**
        *   Open VirtualBox and click "New".
        *   Name it something like "SDN_Thesis_VM".
        *   **Allocate Resources:** This is important. Give the VM at least:
            *   **Memory (RAM):** 4 GB (4096 MB) or more if you can spare it.
            *   **CPUs:** 2 or more cores.
            *   **Hard Disk:** 25-30 GB (Dynamically allocated is fine).
        *   In the settings for the new VM, go to `Storage`, click the empty CD icon, and select the Ubuntu `.iso` file you downloaded.
    4.  **Install Ubuntu:** Start the VM and follow the on-screen instructions to install Ubuntu inside the VM. A minimal installation is perfectly fine.
*   **✅ Success Criteria:** You have a fully bootable Ubuntu desktop running inside a VirtualBox window. You can open a terminal and run basic commands like `ls` and `pwd`.

---

#### **Task P2.2: Mininet Installation & Verification**

*   **Objective:** Install the core network emulation software.
*   **Action (inside your Ubuntu VM):**
    1.  Open a terminal in Ubuntu.
    2.  First, update your package lists:
        ```bash
        sudo apt update
        ```
    3.  Install Mininet using the package manager. This is the easiest method.
        ```bash
        sudo apt install mininet
        ```
*   **✅ Success Criteria:** The installation completes without errors. You can run Mininet's built-in test command and see a successful result.
    ```bash
    sudo mn --test pingall
    ```
    You should see a list of hosts pinging each other with "**0% dropped**" at the end.

---

#### **Task P2.3: Mininet Basics & Tutorial (Critical Learning Task)**

*   **Objective:** Learn how to interact with Mininet. Don't just have it installed; understand how to use it.
*   **Action:**
    1.  **Work through the Mininet Walkthrough:** This is the most important step in this phase. Dedicate a few hours to it. Open a web browser *inside your VM* and go to the official walkthrough: [Mininet Walkthrough](http://mininet.org/walkthrough/).
    2.  **Key skills to practice:**
        *   Starting Mininet with different topologies (`--topo linear,2`, `--topo tree,depth=2,fanout=2`).
        *   Listing nodes, links, and hosts in the Mininet CLI (`nodes`, `links`, `net`).
        *   Running commands on simulated hosts (`h1 ifconfig`, `h2 ping h3`).
        *   Testing bandwidth between hosts (`iperf`).
        *   Understanding how to write and run a basic topology using a Python script.
*   **✅ Success Criteria:** You can comfortably create a simple topology from the Mininet CLI, make hosts ping each other, and run an `iperf` test between two hosts.

---

#### **Task P2.4: Initial Topology Scripting**

*   **Objective:** Programmatically define the network topologies relevant to your project.
*   **Action:**
    1.  Create a folder for your project, e.g., `~/thesis_project`.
    2.  **Create `datacenter.py`:** Inside that folder, create a new Python file. This script will build a simple 2x2 leaf-spine topology.
        ```python
        # ~/thesis_project/datacenter.py
        from mininet.net import Mininet
        from mininet.topo import Topo
        from mininet.cli import CLI
        from mininet.log import setLogLevel

        class DataCenterTopo(Topo):
            "Simple 2x2 Leaf-Spine Topology"
            def build(self):
                # Add spine switches
                s1 = self.addSwitch('s1')
                s2 = self.addSwitch('s2')

                # Add leaf switches
                s3 = self.addSwitch('s3')
                s4 = self.addSwitch('s4')

                # Add hosts
                h1 = self.addHost('h1')
                h2 = self.addHost('h2')
                h3 = self.addHost('h3')
                h4 = self.addHost('h4')

                # Wire spine to leaf
                self.addLink(s1, s3)
                self.addLink(s1, s4)
                self.addLink(s2, s3)
                self.addLink(s2, s4)

                # Wire leaf to hosts
                self.addLink(s3, h1)
                self.addLink(s3, h2)
                self.addLink(s4, h3)
                self.addLink(s4, h4)

        if __name__ == '__main__':
            setLogLevel('info')
            topo = DataCenterTopo()
            net = Mininet(topo=topo)
            net.start()
            CLI(net)
            net.stop()
        ```
    3.  **Create `mesh.py`:** Create a second script for a simple 4-node mesh topology.
*   **✅ Success Criteria:** You can run your script (`sudo python3 datacenter.py`) and, at the `mininet>` prompt, run `pingall` and get 0% packet loss.

---

#### **Task P2.5: SDN Controller (Ryu) Setup**

*   **Objective:** Install the Python-based SDN controller framework you will use to implement your scheduler.
*   **Action:**
    1.  Install `pip`, the Python package installer:
        ```bash
        sudo apt install python3-pip
        ```
    2.  Install Ryu:
        ```bash
        pip install ryu
        ```
    3.  Test the Ryu manager by running its built-in simple learning switch application. This will just sit and listen for a connection from Mininet.
        ```bash
        ryu-manager ryu.app.simple_switch_13
        ```
*   **✅ Success Criteria:** The `ryu-manager` command starts without errors and displays messages like "loading app" and "instantiating app", ending with a "sockets listening on..." message. Keep this terminal open for the final milestone.

---

### **Task P2.M1: Milestone - Full Stack Validation**

*   **Objective:** Prove that all components (Mininet, custom topology, Ryu controller) can work together. This is the final check for Phase 2.
*   **Action:**
    1.  You should have **one terminal open** running the `ryu-manager` from task P2.5.
    2.  **Open a second terminal.**
    3.  Navigate to your project folder (`cd ~/thesis_project`).
    4.  Start your custom Mininet topology, but this time, tell it to connect to the Ryu controller running locally.
        ```bash
        sudo python3 datacenter.py --controller=remote,ip=127.0.0.1,port=6633
        ```
    5.  Watch the Ryu terminal. You should see a burst of activity (e.g., "dpid=...", "OFPStateChange") as the switches from your Mininet topology connect to it.
    6.  In the Mininet terminal (at the `mininet>` prompt), run the final test:
        ```bash
        pingall
        ```
*   **🏆 MILESTONE ACHIEVED:** The `pingall` command reports **0% dropped**. This proves that Mininet handed over control to Ryu, and Ryu correctly installed the necessary flow rules to allow all hosts to communicate.

Your virtual lab is now fully operational and ready for Phase 3, where you will start developing your custom controller logic.
