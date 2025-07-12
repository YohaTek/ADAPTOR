# ADAPTOR

### **Action Plan for Phase 1: Literature Review**

**Objective:** To gain a deep understanding of the existing research in network-aware scheduling and SDN-based control for distributed systems, in order to precisely define the contribution of your thesis and inform your design decisions for RQ1, RQ2, and RQ3.

**Key Areas of Focus (as per the proposal):**
1.  Network-Aware Scheduling
2.  Traffic Engineering in Data Centers
3.  SDN Applications in Edge/Fog Computing

Let's break down each area into specific topics and search keywords.

#### **Area 1: Network-Aware Scheduling**

This is the core of your project. You need to understand how schedulers have evolved to consider the network.

*   **What to Investigate:**
    *   **Classic "Network-Agnostic" Schedulers:** Understand the baseline. Look at schedulers like Hadoop YARN, Kubernetes default scheduler, or basic Slurm configurations. Focus on *what they measure* (CPU/memory load) and *what they ignore* (network state).
    *   **Early Network-Aware Approaches:** How did systems first start incorporating the network? Often, it was just about "data locality"—placing compute close to the data. This is a simple form of network awareness.
    *   **Advanced Scheduling Algorithms:** Explore more sophisticated algorithms. These systems explicitly model the network.
    *   **Metrics and Cost Functions:** How do other researchers solve **RQ2**? Look for papers that propose cost functions combining compute and network metrics (latency, bandwidth, jitter, hop count, path congestion).

*   **Keywords for Academic Search (Google Scholar, IEEE Xplore, ACM Digital Library):**
    *   `"network-aware scheduling"`
    *   `"topology-aware task placement"`
    *   `"joint scheduling and routing"`
    *   `"co-flow scheduling"`
    *   `"data locality" + "scheduler"`
    *   `"deadline-aware scheduling" + "distributed systems"`

#### **Area 2: Traffic Engineering (TE) and Network State**

This area directly informs **RQ1 (Network State Abstraction)** and **RQ3 (Control Plane Logic)**. How do you get a view of the network state without overwhelming it, and what do you do with that information?

*   **What to Investigate:**
    *   **TE in Data Centers:** Data centers were one of the first areas to heavily use centralized TE. Concepts like Hedera, SWAN, and B4 are seminal works. Understand their goals (e.g., maximizing bisection bandwidth, minimizing flow completion time).
    *   **Network State Monitoring:** How is network state collected? This is critical for **RQ1**.
        *   **Passive Monitoring:** Using data from the switches themselves (e.g., OpenFlow port stats). It's low-overhead but can be coarse-grained.
        *   **Active Probing:** Sending small probe packets to measure latency and available bandwidth (e.g., `ping`, `iperf`-like tools). More accurate but adds traffic.
        *   **In-band Network Telemetry (INT):** A modern approach where data packets collect state information as they traverse the network. This might be too complex to implement but is important to know about.
    *   **From your CCNP knowledge:** Contrast these SDN approaches with traditional TE methods like RSVP-TE or how OSPF/EIGRP use metrics. This will help you highlight the unique advantages of a centralized SDN controller.

*   **Keywords for Academic Search:**
    *   `"traffic engineering" + "data center networks"`
    *   `"SDN" + "traffic engineering"`
    *   `"network monitoring" + "SDN"`
    *   `"available bandwidth estimation"`
    *   `"network state abstraction" + "SDN"`
    *   (Seminal Projects): `"Google B4"`, `"Microsoft SWAN"`, `"Facebook Express Backbone"`

#### **Area 3: SDN Applications in Edge/Fog Computing**

This provides the architectural pattern for your solution. Your project is essentially applying data center SDN principles to a more general distributed system (like Edge/CPS).

*   **What to Investigate:**
    *   **SDN Controller Architectures:** Look at how controllers like Ryu, POX, and ONOS are used. Your project mentions Ryu, so focus on papers that use it. See how they structure their Python applications for custom logic. This will directly help you in **Phase 3**.
    *   **Edge/Fog Computing Schedulers:** This is a hot research area. Many papers deal with placing services (e.g., IoT data processing) in a distributed edge environment. Their problems are very similar to yours.
    *   **Use of Mininet in Research:** Find papers that use Mininet as their simulation/emulation platform. Pay close attention to their "Methodology" or "Evaluation Setup" sections. This will give you practical examples of how to set up topologies and experiments in **Phase 2 & 5**.

*   **Keywords for Academic Search:**
    *   `"SDN" + "edge computing" + "resource allocation"`
    *   `"fog computing" + "task scheduling"`
    *   `"Ryu controller" + "application"` or `"use case"`
    *   `"Mininet" + "SDN" + "performance evaluation"`
    *   `"service placement" + "edge network"`

---

### **Workflow and Deliverables for Phase 1**

1.  **Tool Setup:**
    *   Use a reference manager like **Zotero** or **Mendeley**. This is non-negotiable. It will save you countless hours when writing your thesis. Install the browser connector to save papers with one click.

2.  **Execution Strategy (Weeks 1-4, for example):**
    *   **Week 1: Broad Survey.** Start by finding 2-3 recent survey papers or high-level articles for each of the three areas. This will give you a map of the entire field and key terminology.
    *   **Week 2: Deep Dive.** Use the keywords above to find 10-15 highly-cited or highly-relevant papers. Read their abstracts and introductions to filter them. Download the most promising ones into Zotero.
    *   **Week 3: Synthesize and Annotate.** Read the selected papers in detail. For each paper, write a short summary (3-5 bullet points) in Zotero's notes field:
        *   What problem are they solving?
        *   What is their proposed method (especially their cost function or algorithm)?
        *   How did they evaluate it (simulation, testbed)?
        *   What are its key limitations or assumptions?
    *   **Week 4: Structure and Write.** Begin outlining and writing.

3.  **Phase 1 Deliverables:**
    *   **An Annotated Bibliography:** A structured list of the papers you've reviewed, with your summaries. This is an excellent appendix for your thesis and a great discussion document for meetings with your supervisor.
    *   **A "State-of-the-Art" Summary (2-4 pages):** A document that synthesizes your findings. It should have sections corresponding to the three areas above. Crucially, it must end with a section titled **"Identified Research Gap and Project Positioning,"** where you explicitly state how your proposed work is different from or improves upon existing work. This directly justifies your project's novelty.
    *   **Draft of Thesis Chapter 1 (Introduction) & Chapter 2 (Related Work):** Start writing these chapters now while the information is fresh. It's much easier than trying to write everything at the end.
    *   **A Refined Set of Research Questions:** Based on your reading, you might slightly tweak the wording of the RQs to make them more precise. For example, for RQ2, you might have a clearer idea of what the "cost function" components will be.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### **Action Plan for Phase 3: Controller and Topology Development**

**Objective:** To write a custom SDN controller in Python (using Ryu) that discovers the network topology, monitors its state, and contains the core logic for making network-aware scheduling decisions.

---

#### **Part 1: Enhancing the Simulation Environment (The "World")**

First, we'll make our Mininet world more realistic, as described in the proposal.

*   **Task P3.A: Define Realistic Topologies**
    *   **Objective:** Update your topology scripts from Phase 2 to better reflect the project's use cases and have realistic network characteristics.
    *   **Step-by-Step Actions:**
        1.  Open your `datacenter.py` and `mesh.py` scripts.
        2.  Use the Mininet API's link parameters to add properties. For example:
            *   **Datacenter:** Links from hosts to leaf switches might be `10Gbps` with low latency (`1ms`), while links between switches might be `40Gbps`.
            *   **Satellite Mesh:** Links will have much higher latency (`delay='80ms'`) and potentially lower bandwidth (`bw=1`).
        3.  **Example Code:** Modify the `addLink` line:
            ```python
            # Before:
            # self.addLink(s3, h1)
            
            # After:
            from mininet.link import TCLink
            # ... inside the build method:
            self.addLink(s3, h1, cls=TCLink, bw=10, delay='1ms') 
            ```
            *(Note: You must specify `cls=TCLink` to use parameters like `bw` and `delay`.)*
    *   **✅ Success Criteria:** You can run `sudo python3 datacenter.py`. Inside Mininet, running `iperf` between two hosts shows a bandwidth close to the limit you set (e.g., ~10 Gb/s). Running `ping` shows a round-trip time reflecting your delay settings (e.g., ~2ms).

---

#### **Part 2: Building the Controller (The "Brain")**

Now we build the controller itself, piece by piece.

*   **Task P3.B: Create the Controller Skeleton**
    *   **Objective:** Set up a clean, working Ryu application that will house all your custom logic.
    *   **Step-by-Step Actions:**
        1.  In your project folder (`~/thesis_project`), create a new file named `network_aware_controller.py`.
        2.  Find the source code for Ryu's `simple_switch_13.py` (it's in the Ryu source code or easily found online). Copy its contents into your new file. This gives you a working baseline that handles basic packet switching.
        3.  Rename the class from `SimpleSwitch13` to something meaningful, like `NetworkAwareController`.
    *   **✅ Success Criteria:** You can run your new controller (`ryu-manager network_aware_controller.py`) and your Mininet topology (`sudo python3 datacenter.py --controller=remote`), and `pingall` succeeds. You have successfully created your own custom controller.

*   **Task P3.C: Implement Topology Discovery & Representation (Answering RQ1 partially)**
    *   **Objective:** Make the controller build and maintain an internal map of the network.
    *   **Step-by-Step Actions:**
        1.  Install the `networkx` library: `pip install networkx`.
        2.  In your `network_aware_controller.py`, import the necessary Ryu event classes and `networkx`:
            ```python
            from ryu.controller import ofp_event
            from ryu.controller.handler import set_ev_cls
            from ryu.topology import event
            import networkx as nx
            ```
        3.  In your controller's `__init__` method, create an empty `networkx` graph: `self.topo_graph = nx.Graph()`.
        4.  Create event handler functions to automatically populate the graph:
            *   A handler for `event.EventSwitchEnter` that adds switches as nodes to your graph.
            *   A handler for `event.EventLinkAdd` that adds links as edges between the switch nodes in your graph.
        5.  Add some logging to see it work. For example, when a link is added, print `f"Discovered Link: {link.src.dpid} <--> {link.dst.dpid}"`.
    *   **✅ Success Criteria:** When you start your controller and Mininet, the controller's log output shows the switches and links being discovered and added. You have given your brain "eyes."

*   **Task P3.D: Implement a Scheduling "Brain" Stub**
    *   **Objective:** Create the basic structure of the scheduler itself. At this stage, it won't do anything smart, but it will establish the framework for the logic you'll add later.
    *   **Step-by-Step Actions:**
        1.  **Define the "Scheduler" as a separate class or a set of methods** within your controller. This keeps the code clean.
        2.  **Create a main scheduling function stub, `_schedule_task(self, task_type)`**. This function will be the entry point for your logic.
        3.  **Add a REST API endpoint** to your Ryu controller so you can trigger the scheduler from outside. Ryu has built-in support for this. You'll create a controller method that listens for an HTTP POST request (e.g., to `http://localhost:8080/scheduler/schedule_task`).
            ```python
            # Example using Ryu's built-in web server
            from ryu.app.wsgi import ControllerBase, WSGIApplication, route
            
            class MyRestController(ControllerBase):
                def __init__(self, req, link, data, **config):
                    super(MyRestController, self).__init__(req, link, data, **config)
                    self.scheduler_app = data['scheduler_app']

                @route('scheduler', '/scheduler/schedule_task', methods=['POST'])
                def schedule_task_handler(self, req, **kwargs):
                    # In a real app, you'd parse the request body
                    # For now, just trigger the scheduler
                    self.scheduler_app._schedule_task("large_data") 
                    return "Scheduling triggered!\n"
            ```
    *   **✅ Success Criteria:** You can run your controller and use a command-line tool like `curl` to send a request to your controller's new API endpoint (`curl -X POST http://localhost:8080/scheduler/schedule_task`). You should see a log message from your `_schedule_task` function stub, confirming that the "brain" can be activated on command.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
