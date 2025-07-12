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

### **Action Plan for Phase 4: Implementation of Scheduling Logic**

**Objective:** To implement and integrate two distinct scheduling algorithms—a simple baseline and your novel network-aware version—into your custom Ryu controller.

---

#### **Part 1: Implementing the Baseline (Network-Agnostic) Scheduler**

**Goal:** Create the simple scheduler that only considers compute resources. This will be your scientific control group.

*   **Task P4.A: Implement Compute State Acquisition**
    *   **Objective:** Give your controller the ability to query the CPU load of all hosts in the network.
    *   **Step-by-Step Actions:**
        1.  **Create the Agent:** Write a small Python script named `agent.py` using the Flask web framework (`pip install Flask`). This agent will have one purpose: when it receives an HTTP GET request at a `/status` endpoint, it will check the system's CPU load and return it as a JSON object. You will need a library like `psutil` (`pip install psutil`) to get the CPU load easily.
        2.  **Deploy the Agent:** In your Mininet topology scripts (`datacenter.py`, etc.), add a command to start this `agent.py` on every host when the network starts.
            ```python
            h1 = self.addHost('h1')
            h1.cmd('python3 agent.py &') # The '&' runs it in the background
            ```
        3.  **Create the Poller:** In your main `network_aware_controller.py`, write a function `_get_compute_states()`. This function will periodically (or on-demand) send HTTP requests to the known IP addresses of your hosts to get their status from the agent. It should store the results in a dictionary, e.g., `self.compute_states = {'10.0.0.1': {'cpu': 15}, '10.0.0.2': {'cpu': 80}}`.
    *   **✅ Success Criteria:** You can run your Mininet topology, and from the controller's log, you can see it successfully polling and printing the CPU loads from all active hosts.

*   **Task P4.B: Implement the Network-Agnostic Scheduling Logic**
    *   **Objective:** Write the code for the baseline scheduler.
    *   **Step-by-Step Actions:**
        1.  In your `network_aware_controller.py`, create a new function `_schedule_baseline(self)`.
        2.  **The Logic:** This function is very simple. It will:
            a. Call `_get_compute_states()` to get the latest CPU data.
            b. Iterate through the returned dictionary.
            c. Find the host with the *lowest* CPU load value.
            d. Return the ID or IP address of that host.
        3.  Modify the REST API endpoint you created in Phase 3. When it's triggered, it should call this `_schedule_baseline()` function and log the result clearly: `[BASELINE] Decision: Chose host hX with CPU load Y%`.
    *   **✅ Success Criteria:** You can trigger the scheduler via its API, and it correctly identifies and logs the host with the lowest CPU load, regardless of network conditions.

---

#### **Part 2: Implementing the Proposed (Network-Aware) Scheduler**

**Goal:** Build the "smart" scheduler that co-optimizes compute and network resources, directly addressing your research questions.

*   **Task P4.C: Implement Network State Monitoring (Answering RQ1)**
    *   **Objective:** Give your controller the ability to measure network link properties (latency).
    *   **Step-by-Step Actions:**
        1.  **Latency Probing:** In your controller, create a function that periodically sends a special probe packet (e.g., a custom LLDP packet or even just a specially crafted ICMP Echo request) between every pair of connected switches discovered in Phase 3.
        2.  **Measure RTT:** By recording the time the probe was sent and the time the reply was received, you can calculate the Round-Trip Time (RTT) for that link. Latency is `RTT / 2`.
        3.  **Update Graph:** Store this calculated latency as an attribute on the corresponding edge in your `networkx` graph. `self.topo_graph[switch1][switch2]['latency'] = calculated_latency`.
    *   **✅ Success Criteria:** Your controller periodically logs the measured latencies for all the links in the topology, and these values are stored in your internal network graph.

*   **Task P4.D: Implement the Unified Cost Function (Answering RQ2)**
    *   **Objective:** Create the mathematical formula that unifies compute and network costs.
    *   **Step-by-Step Actions:**
        1.  Create a new function in your controller: `_calculate_unified_cost(self, compute_load, path_latency)`.
        2.  **The Formula:** Implement the cost function. Start with a simple weighted sum. Define the weights as easily configurable variables at the top of your class.
            ```python
            # At the top of your controller class
            WEIGHT_CPU = 0.6
            WEIGHT_LATENCY = 0.4
            
            # The function
            def _calculate_unified_cost(self, compute_load, path_latency):
                # Normalize values if necessary (e.g., CPU load 0-100 -> 0-1)
                normalized_cpu = compute_load / 100.0
                # Assuming latency is in ms and we want to penalize higher values
                cost = (self.WEIGHT_CPU * normalized_cpu) + (self.WEIGHT_LATENCY * path_latency)
                return cost
            ```
    *   **✅ Success Criteria:** You have a function that takes compute and network metrics as input and produces a single, comparable cost score as output.

*   **Task P4.E: Implement the Network-Aware Scheduling Algorithm (Answering RQ3)**
    *   **Objective:** Write the main algorithm that uses the cost function to find the optimal host.
    *   **Step-by-Step Actions:**
        1.  Create a new function `_schedule_network_aware(self)`.
        2.  **The Logic:** This function will:
            a. Get the latest compute states for all hosts.
            b. For **each candidate host**:
                i. Find the best network path from a source (e.g., a designated ingress switch) to that host using Dijkstra's algorithm on your `networkx` graph. Use 'latency' as the weight for the pathfinding: `nx.dijkstra_path(self.topo_graph, source_switch, host_switch, weight='latency')`.
                ii. Calculate the total path latency by summing the latency of all links in the path.
                iii. Get the host's CPU load.
                iv. Use your `_calculate_unified_cost()` function to get a final score for this host.
            c. Compare the scores for all hosts and select the one with the *lowest* cost.
            d. Log the decision-making process and the final choice: `[AWARE] Chose host hY with cost Z`.
    *   **✅ Success Criteria:** The function correctly evaluates all possible hosts and selects the one with the best combined compute-network score. You can create a test case where the host with the lowest CPU is *not* chosen because it has a very high-latency path.
   ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
### **Action Plan for Phase 5: Experimentation & Analysis**

**Objective:** To design and execute a series of controlled experiments that quantitatively demonstrate the performance difference between your network-agnostic (Baseline) and network-aware (Proposed) schedulers, using realistic task types and collecting clear performance metrics.

---

#### **Part 1: Defining the Experiments (The "What" and "How")**

**Goal:** Establish a clear, repeatable, and automated experimental methodology.

*   **Task P5.A: Define "Task Requests" and Performance Metrics**
    *   **Objective:** Translate the abstract concept of a "task" into concrete Mininet commands and define exactly what you will measure.
    *   **Step-by-Step Actions:**
        1.  **Define "Large Data Transfer" Task:**
            *   **Command:** `iperf`
            *   **Implementation:** A function that takes a source host and destination host and runs `h_dest.cmd('iperf -s &')` and `h_src.cmd('iperf -c h_dest.IP()')`.
            *   **Primary Metric:** **Completion Time**. You will parse the `iperf` output to get the total time taken for the transfer.
        2.  **Define "Low-Latency Control" Task:**
            *   **Command:** `ping`
            *   **Implementation:** A function that runs `h_src.cmd('ping -c 10 h_dest.IP()')` to send 10 packets.
            *   **Primary Metric:** **Average Latency**. You will parse the `ping` output to get the `avg` round-trip time.
        3.  **Define "Deadline":** For some experiments, you will set a pass/fail condition. For example, a data transfer must complete in `< 5 seconds`, or average ping latency must be `< 100ms`. This allows you to measure **Task Success Rate**.
    *   **✅ Success Criteria:** You have Python functions ready that can execute these specific tasks within a running Mininet simulation and parse their text output to extract numerical results.

*   **Task P5.B: Design the Experimental Scenarios**
    *   **Objective:** Create specific network conditions that will highlight the differences between your two schedulers.
    *   **Step-by-Step Actions:**
        1.  **Scenario 1: The Obvious Choice (Datacenter Topology)**
            *   **Setup:** Modify your `datacenter.py` topology. Make the link to `h1` very slow and high-latency (`bw=1, delay='100ms'`). Make the link to `h4` fast (`bw=10, delay='1ms'`).
            *   **Initial State:** Manually set the CPU load on the hosts. Make `h1` have very low CPU load, and `h4` have very high CPU load.
            *   **Hypothesis:** The Baseline scheduler will incorrectly choose `h1` for a large data transfer, resulting in a very long completion time. The Aware scheduler will correctly choose `h4`, even with its high CPU, because the network path is superior.
        2.  **Scenario 2: The Latency Trap (Mesh Topology)**
            *   **Setup:** Use your `mesh.py` topology. Set all links to have high bandwidth (`bw=100`) but create one path that has significantly higher latency (e.g., goes through 3 hops vs. 1 hop).
            *   **Initial State:** Set CPU loads to be roughly equal on all hosts.
            *   **Hypothesis:** For a low-latency control task, the Baseline scheduler might pick a host that is "further away" in terms of network hops/latency. The Aware scheduler will explicitly choose the host with the lowest end-to-end latency path.
    *   **✅ Success Criteria:** You have documented these scenarios, including the specific topology settings and initial conditions you will use for each test.

---

#### **Part 2: Running the Experiments (The "Do It")**

**Goal:** Execute the planned experiments and meticulously collect the raw data.

*   **Task P5.C: Create an Automated Experiment Runner**
    *   **Objective:** Automate the entire process to ensure consistency and save time.
    *   **Step-by-Step Actions:**
        1.  Write a master Python script (`run_experiments.py`).
        2.  This script should be able to:
            a. Accept arguments, e.g., `python3 run_experiments.py --scenario=datacenter --scheduler=baseline --task=data_transfer`.
            b. Programmatically start your Ryu controller with the correct mode.
            c. Start your Mininet topology with the correct scenario setup.
            d. Trigger the scheduler via its REST API.
            e. Once the scheduler returns a decision (e.g., "use h4"), execute the appropriate task function (from P5.A) on the correct hosts.
            f. Capture the numerical result (e.g., `3.45` seconds).
            g. Append the result to a CSV file with all relevant info: `timestamp, scenario, scheduler, task, result, success_or_fail`.
            h. Clean up and shut down Mininet and Ryu.
    *   **✅ Success Criteria:** You have a single command that can run one full experiment from start to finish and log the result.

*   **Task P5.D: Execute the Experiment Batches**
    *   **Objective:** Run all your defined experiments and gather the data.
    *   **Step-by-Step Actions:**
        1.  Wrap your `run_experiments.py` script in a loop.
        2.  **For the Baseline scheduler:** Run each scenario (e.g., Datacenter and Mesh) 20-30 times to get a good sample size. Your script will automatically log the results for each run.
        3.  **For the Aware scheduler:** Repeat the exact same process. Run each scenario 20-30 times.
    *   **✅ Success Criteria:** You have a CSV data file containing hundreds of rows, with each row representing the outcome of a single, controlled experiment. The data is clean and structured.

---

#### **Part 3: Analyzing the Results (The "Prove It")**

**Goal:** Turn your raw data into clear, compelling charts and statistics that prove your thesis.

*   **Task P5.E: Process and Analyze the Data**
    *   **Objective:** Calculate the key statistics that compare the two schedulers.
    *   **Step-by-Step Actions:**
        1.  Use a Jupyter Notebook with the `pandas` library to load your CSV data file into a DataFrame.
        2.  Group the data by `scenario`, `scheduler`, and `task`.
        3.  For each group, calculate the key performance metrics:
            *   **Mean and Median:** (e.g., average completion time, average latency).
            *   **Standard Deviation:** To see how consistent the results are.
            *   **Success Rate:** The percentage of tasks that met their deadline.
    *   **✅ Success Criteria:** You have a table in your notebook summarizing the aggregated performance of each scheduler under each scenario. For example:

| Scenario   | Scheduler | Avg. Completion Time (s) | Success Rate |
| :--------- | :-------- | :----------------------- | :----------- |
| Datacenter | Baseline  | 25.4                     | 10%          |
| Datacenter | Aware     | 4.8                      | 95%          |

*   **Task P5.F: Visualize the Results**
    *   **Objective:** Create the graphs that will go into your thesis to make your findings easy to understand.
    *   **Step-by-Step Actions:**
        1.  Using `matplotlib` or `seaborn` in your Jupyter Notebook, create plots from your aggregated data.
        2.  **Bar Charts are essential:** Create a bar chart comparing the "Average Task Completion Time" for Baseline vs. Aware for the datacenter scenario.
        3.  **Box Plots are excellent:** Create a box plot to show the distribution of ping latencies for the mesh network scenario. This shows not just the average but also the consistency.
        4.  **Label Everything Clearly:** Ensure your plots have titles, labeled axes (with units!), and a clear legend. These plots should be "presentation-ready."
    *   **✅ Success Criteria:** You have a set of 3-5 high-quality, clearly labeled plots that visually and dramatically show the superiority of your network-aware scheduler in the scenarios you designed.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### **Action Plan for Phase 6: Thesis Writing**

**Objective:** To produce a complete, well-structured Master's thesis that effectively documents your project's approach, controller design, experimental results, and conclusions, leading to a successful final submission.

---

#### **Part 1: Drafting the Technical Core (The "What I Did")**

**Goal:** Start by documenting the concrete work you just completed. This is the easiest way to build momentum and get a large volume of content written quickly.

*   **Task P6.A: Finalize Thesis Structure and Draft "Design & Implementation" (Chapters 3 & 4)**
    *   **Objective:** Create the skeleton of your document and fill in the parts that describe the system you built.
    *   **Step-by-Step Actions:**
        1.  **Create the Master Document:** Set up your thesis file in LaTeX (recommended for academic work) or Word. Create placeholder files for each chapter: Intro, Related Work, System Design, Implementation, Evaluation, Discussion, Conclusion.
        2.  **Write Chapter 3 (System Design):** This is the high-level "blueprint."
            *   Describe the overall architecture: the SDN controller, the Mininet environment, and the host agents. Use a diagram to show how they interact.
            *   Explain the *concept* of your network-aware approach. Describe your unified cost function (RQ2) and the logic of your scheduling algorithm (RQ3) in prose and pseudocode.
        3.  **Write Chapter 4 (Implementation):** This is the "how-to" guide.
            *   Get specific. Detail the key technologies used (Mininet, Ryu, Python, Flask, NetworkX).
            *   Include well-commented code snippets from `network_aware_controller.py` to illustrate the most important functions (e.g., the cost function, the main scheduling loop).
            *   Show an example of your Mininet topology script with custom link parameters.
    *   **✅ Success Criteria:** You have two complete draft chapters that explain what you designed and how you built it, with supporting diagrams and code.

*   **Task P6.B: Draft "Evaluation & Results" (Chapter 5)**
    *   **Objective:** Present the data from your experiments objectively and clearly.
    *   **Step-by-Step Actions:**
        1.  **Leverage your Phase 5 work directly.** This chapter is about presenting facts, not opinions.
        2.  **Describe the Experimental Setup:** Detail the scenarios you designed (e.g., "High-Load Datacenter," "Latency-Sensitive Swarm"). Explain the task types ("large data transfer," "low-latency control") and the metrics you collected (completion time, latency, success rate).
        3.  **Insert Your Visuals:** Place the plots and tables you generated in Phase 5 into the document. Ensure they are high-resolution and have clear, numbered captions (e.g., "Figure 5.1: Comparison of Task Completion Times...").
        4.  **Describe the Visuals:** For each plot or table, write a paragraph that states exactly what the data shows. Example: *"As shown in Figure 5.1, the average completion time for the network-aware scheduler was 4.8 seconds, representing an 81% improvement over the baseline scheduler's average of 25.4 seconds under the same conditions."*
    *   **✅ Success Criteria:** You have a data-driven chapter filled with your key results, presented as clear, easy-to-understand figures and tables with descriptive text.

---

#### **Part 2: Framing the Narrative and Drawing Conclusions (The "Why It Matters")**

**Goal:** Now that the core content is done, frame it with an introduction, connect it to existing research, and state its significance.

*   **Task P6.C: Draft "Introduction" and "Related Work" (Chapters 1 & 2)**
    *   **Objective:** Set the stage for your work and position it within the scientific landscape.
    *   **Step-by-Step Actions:**
        1.  **Leverage your Phase 1 work.** You already have detailed notes and summaries.
        2.  **Write Chapter 1 (Introduction):** Now that you know your exact results, you can write a powerful introduction.
            *   Start broad (the importance of CPS, distributed systems).
            *   Narrow down to the specific problem (network-agnostic schedulers are inefficient).
            *   State your thesis statement and explicitly list your Research Questions (RQ1-RQ4).
            *   Briefly summarize your approach and your key findings.
            *   Outline the structure of the rest of the thesis.
        3.  **Write Chapter 2 (Related Work):** Polish your literature review summary from Phase 1 into a formal chapter. Group related papers together thematically (e.g., "Traffic Engineering in Data Centers," "Scheduling in Edge Computing"). For each area, summarize the state-of-the-art and clearly state the "gap" that your work addresses.
    *   **✅ Success Criteria:** The reader understands the problem, why it's important, what others have done, and what you are contributing that is new.

*   **Task P6.D: Draft "Discussion" and "Conclusion" (Chapters 6 & 7)**
    *   **Objective:** Interpret your results, acknowledge limitations, and provide a strong concluding statement.
    *   **Step-by-Step Actions:**
        1.  **Write Chapter 6 (Discussion):** This is where you answer "why?"
            *   Go back to your results from Chapter 5 and interpret them. Why did the network-aware scheduler perform better? Connect its success back to the design choices you made in Chapter 3.
            *   Discuss any limitations of your work. (e.g., "The study was conducted in a simulation... a physical testbed could reveal different challenges.") This shows critical self-reflection.
        2.  **Write Chapter 7 (Conclusion & Future Work):** End on a strong, clear note.
            *   **Conclusion:** Briefly summarize the entire thesis in a few paragraphs. Re-state the problem, your solution, and the main results. Directly answer each of your research questions one by one.
            *   **Future Work:** Suggest 3-5 concrete ideas for how this research could be extended. (e.g., "Incorporate machine learning to dynamically adjust cost function weights," "Extend the controller to manage energy consumption," "Test with real-world CPS application traffic profiles.")
    *   **✅ Success Criteria:** The reader understands the significance of your results and the potential impact of your work, as well as its boundaries.

---

#### **Part 3: Finalization and Polish**

**Goal:** Transform your complete draft into a professional, submission-ready document.

*   **Task P6.E: Compile Front/Back Matter and Do a Full Read-Through**
    *   **Objective:** Add all finishing touches and perform a holistic review for flow and clarity.
    *   **Step-by-Step Actions:**
        1.  **Add Front/Back Matter:** Create the Title Page, Abstract, Table of Contents, List of Figures, and List of Tables.
        2.  **Generate Bibliography:** Use your reference manager (Zotero/Mendeley) to automatically generate and format your entire bibliography. This saves hours of manual work.
        3.  **Full Read-Through:** Read the *entire thesis* from start to finish. Check for consistent terminology, logical flow between chapters, and clear explanations. This is your chance to improve the overall narrative.
    *   **✅ Success Criteria:** The document reads as a single, coherent story, not just a collection of chapters.

*   **Task P6.F: Final Proofread and Submission**
    *   **Objective:** Catch any remaining errors and submit your work.
    *   **Step-by-Step Actions:**
        1.  **Proofread:** Do one final pass specifically for spelling, grammar, and punctuation errors. It's often helpful to read it aloud or use a text-to-speech tool to catch awkward phrasing.
        2.  **Check Formatting:** Ensure all university formatting guidelines (margins, fonts, page numbers, etc.) are met.
        3.  **Generate Final PDF:** Create the final, clean PDF file.
        4.  **Submit!** Send the document to your supervisor, Dr. Calabretta, for review.
    *   **✅ Success Criteria (Milestone):** You have submitted a complete, polished, high-quality draft of your Master's thesis.
