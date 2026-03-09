# 🐙 OctopAI: Distributed Cognitive Routing for Agentic AI

**OctopAI** is a resilient, Byzantine Fault Tolerant (BFT) cognitive routing system for multi-agent AI.

Just as an octopus distributes its "brain" across its eight arms—allowing them to process information, react, and solve problems semi-autonomously while coordinating with a central nervous system—OctopAI shatters the monolithic LLM paradigm. It distributes reasoning, tool-execution, and memory across a decentralized web of agentic nodes.

Built as a core component of the KeyExchange.org initiative, OctopAI natively supports decentralized accounting, allowing agents to buy, sell, and share cognitive labor, "products," and context with cryptographically secured provenance.

---

## 🧠 The "Distributed Brain" Architecture

Traditional AI pipelines rely on massive, centralized models acting as single points of failure. OctopAI operates as a **Cognitive AI Fabric**. Tasks are routed dynamically to the most efficient edge nodes, micro-agents, or hardware enclaves based on network topology, cost, and trust metrics.

```mermaid
graph TD
    %% Define external actors and systems with styles from the image
    Human_User["Human User / Admin"]:::actor
    External_LLM["External LLM APIs<br>(OpenAI, Anthropic, etc.)"]:::external
    KeyExchange["KeyExchange.org Ledger<br>(Substrate)"]:::external
    Vector_DB["Vector Database<br>(Qdrant)"]:::external
    MCP_Data["MCP Data Sources"]:::external

    %% Define the core OctopAI system boundary box
    subgraph OctopAI_System ["OctopAI Cognitive Fabric<br>System Boundary"]
        User_IF["User Interface<br>(Web / CLI / API Gateways)"]:::ui

        %% Position text objects within the layout as no-border text-nodes
        l_queries["Issues Queries/Commands"]:::label_text
        l_routes["Routes Request"]:::label_text
        l_ctrl["Control Plane Pub/Sub"]:::label_text
        l_llm["Final LLM Call"]:::label_text
        l_mcp_l["Inject Dynamic Context"]:::label_text
        l_mcp_a["Inject Dynamic Context"]:::label_text
        l_mcp["Inject Dynamic Context"]:::label_text
        
        %% Use invisible edges to stack text labels outside subgraph boxes
        l_queries ~~~ User_IF
        User_IF ~~~ l_routes
        l_ctrl ~~~ Nervous_System

        %% Define the nested subgraph for Brain Core
        subgraph Cognitive_Brain ["Cognitive Brain Core"]
            direction TB
            Router["Cognitive Router<br>(Rust/Go)"]:::core
            BFT_Consensus["BFT Consensus Engine<br>(Malachite)"]:::bft
            Accounting["Accounting & Provenance<br>Interface"]:::accounting
            Logic_Core["Core Logic & RAG<br>(Rig Lib)"]:::logic
            Graphlink_Comp["Graphlink Compression<br>Algorithm"]:::core
            
            %% Positioning labels as no-border text nodes
            l_state["State Agreement"]:::label_text
            l_txn["Transaction Data"]:::label_text
            l_rag["RAG Processing"]:::label_text
            l_sem["Semantic Deltas"]:::label_text
            
            %% Stacking labels in Brain subgraph
            Router ~~~ l_state
            Router ~~~ l_txn
            Router ~~~ l_rag
            Router ~~~ l_sem
        end
        
        %% Define the nested subgraph for Distributed Agents
        subgraph Distributed_Arms ["Distributed Agents<br>(WasmActors)"]
            direction LR
            Agent_Nodes["Agent Nodes<br>(wasmCloud Host)"]:::arms
            Secure_Runtime["Secure Runtime<br>(ZeroClaw OS)"]:::arms
            Agent_Logic["Agent Logic<br>(Rig Lib)"]:::arms
            
            %% Positioning labels as no-border text nodes
            l_exec["Executes Within"]:::label_text
            l_inv["Invokes"]:::label_text
            
            %% Stacking labels in Arms subgraph
            Agent_Nodes ~~~ l_exec
            Agent_Nodes ~~~ l_inv
        end

        %% Lone nodes within System boundary
        Nervous_System["Nervous System<br>(Zenoh Pub/Sub Mesh)"]:::nervous
        Data_Serialization["Data Serialization<br>(Toon Format)"]:::serialization
        
        %% Lone text within boundary
        l_msg_s["Message Serialization"]:::label_text
        l_data["Data Plane Pub/Sub"]:::label_text
        l_pay["Format Payloads"]:::label_text
        l_msg["Format Messages"]:::label_text
        l_final_llm["Final LLM Call"]:::label_text
        l_tally["Tally Value / Settle"]:::label_text
        l_vec["Vector Search"]:::label_text
        
        %% Connect to Lone nodes with labels
        l_msg_s ~~~ Data_Serialization
        l_data ~~~ Nervous_System
        Data_Serialization ~~~ l_pay
        Agent_Logic ~~~ l_msg
    end

    %% -- Connections with edge logic and text nodes --
    
    %% User input
    Human_User --> l_queries
    l_queries --> User_IF

    %% UI to Brain
    User_IF --> l_routes
    l_routes --> Cognitive_Brain
    
    %% Brain internal connections
    Router --> l_state
    l_state --> BFT_Consensus
    Router --> l_txn
    l_txn --> Accounting
    Router --> l_rag
    l_rag --> Logic_Core
    Router --> l_sem
    l_sem --> Graphlink_Comp
    
    %% Arms internal connections
    Agent_Nodes -.-> l_exec
    l_exec --> Secure_Runtime
    Agent_Nodes --> l_inv
    l_inv --> Agent_Logic
    
    %% Nervous System and Serialization connections
    Router --> l_ctrl
    l_ctrl --> Nervous_System
    Agent_Nodes --> l_data
    l_data --> Nervous_System
    
    Logic_Core --> l_msg_s
    l_msg_s --> Data_Serialization
    Agent_Logic --> l_msg
    l_msg --> Data_Serialization
    Data_Serialization -.-> l_pay
    l_pay --> Agent_Nodes
    
    %% External call connections
    Router --> l_final_llm
    l_final_llm --> External_LLM
    
    Router --> l_tally
    l_tally --> KeyExchange
    
    Logic_Core --> l_vec
    l_vec --> Vector_DB
    
    %% Combine logic and agent calls for single MCP data sources node
    Logic_Core --> l_mcp_l
    l_mcp_l --> l_mcp
    Agent_Logic --> l_mcp_a
    l_mcp_a --> l_mcp
    l_mcp --> MCP_Data

    %% -- Class Definitions with correct color codes from image --
    
    %% External actors/systems (tan or no-fill dashed)
    classDef actor fill:#fdb,stroke:#333,stroke-width:2px;
    classDef external fill:none,stroke:#666,stroke-width:2px,stroke-dasharray: 5 5,color:grey;

    %% Internal Boundary nodes
    classDef ui fill:#fff,stroke:#333,stroke-width:1px;
    classDef control fill:none,stroke:none; %% for invisible lines

    %% Brain Core Nodes
    classDef core fill:#ccf,stroke:#333,stroke-width:2px;
    classDef bft fill:#faa,stroke:#333,stroke-width:2px;
    classDef accounting fill:#ffe,stroke:#333,stroke-width:2px;
    classDef logic fill:#cbf,stroke:#333,stroke-width:2px;
    classDef nervous fill:#fdc,stroke:#333,stroke-width:2px;

    %% Distributed Agents Nodes
    classDef arms fill:#dfd,stroke:#333,stroke-width:1px;
    
    %% Data Serialization nodes
    classDef serialization fill:none,stroke:#666,stroke-width:1px,stroke-dasharray: 3 3,color:grey;
    
    %% Text objects as no-border nodes
    classDef label_text fill:none,stroke:none,color:black, font-weight:normal, font-family:sans-serif;
```

### Key Capabilities

* **M2M & A2A Routing:** Native Machine-to-Machine and Agent-to-Agent communication protocols bridging the gap between hardware sensors and cognitive reasoning layers.
* **Model Context Protocol (MCP) Support:** Standardized integration for injecting dynamic context, database schemas, and external APIs into agent workflows safely.
* **Byzantine Fault Tolerance (BFT):** Built for untrusted environments. If a fraction of agent nodes are compromised, hallucinating, or returning malicious data, the cognitive fabric reaches a healthy consensus before finalizing state.

---

## ⚙️ Core Technologies & Stack

OctopAI stands on the shoulders of the most resilient open-source tools in the Rust, WebAssembly, and decentralized ecosystems.

### 1. Agentic Execution & Orchestration

* **ZeroClaw:** Powers the core secure-by-default runtime for OctopAI's individual "arm" nodes, ensuring agents can operate securely on constrained edge hardware.
* **Rig:** Provides the foundational Rust primitives for building the state machines, RAG pipelines, and tool bindings within each agent.
* **wasmCloud:** Orchestrates the distributed agents as portable WebAssembly actors, allowing cognitive workloads to shift seamlessly between cloud datacenters and the edge.

### 2. Data Protocols & Compression

* **Zenoh:** Serves as the high-throughput, zero-overhead pub/sub nervous system connecting the decentralized nodes.
* **Toon:** Utilized for agent-to-agent payload serialization, drastically reducing context-window consumption compared to JSON.
* **Graphlink Compression Algorithm:** A proprietary protocol built into OctopAI. Graphlink performs delta-encoding and semantic pruning on LLM vector outputs before transmission over the Zenoh mesh. By transmitting only the semantic delta (the change in context state), Graphlink reduces bandwidth requirements for A2A communication by up to 85%.

### 3. Trust & Decentralized Accounting

* **Malachite:** Provides the ultra-fast BFT consensus engine, ensuring agents agree on the sequence of events and the validity of shared context.
* **Substrate:** The backbone of the KeyExchange.org integration. Substrate powers the distributed ledger that tracks agentic value creation.

---

## ⚖️ KeyExchange.org: The Tokenomic Ledger

OctopAI isn't just a technical framework; it is an economic one. As agents collaborate to solve complex problems, they generate value. Through the KeyExchange.org integration, OctopAI implements an automated, M2M economic layer:

* **Provenance Tracking:** When Agent A generates a useful predictive model or data synthesis (a "Value-Add Product"), the Substrate ledger records its creation, the token economics expended (compute + time + underlying model costs), and cryptographically signs it.
* **Cognitive Marketplaces:** If Agent B requests this product to fulfill its own goal, the transaction is routed via OctopAI.
* **Automated Clearing:** The system automatically handles the accounting. It deducts tokens from Agent B's programmatic wallet and credits Agent A, establishing a dynamic pricing model based on compute expenditure and scarcity.

---

## 🚀 Getting Started

> **Note:** OctopAI is in active development. The following commands reflect the upcoming `v0.1-alpha` release.

### Prerequisites

* Rust 1.75+
* `wasm32-unknown-unknown` target
* A running Zenoh router instance

### Installation

```bash
# Clone the repository
git clone https://github.com/KeyExchange/OctopAI.git
cd OctopAI

# Build the core cognitive router
cargo build --release --bin octopai-router

# Build the substrate accounting node
cargo build --release --bin keyexchange-node

```

### Starting a Local Fabric

```bash
# 1. Start the KeyExchange ledger
./target/release/keyexchange-node --dev

# 2. Start the local Zenoh mesh
zenohd &

# 3. Boot the OctopAI BFT router
./target/release/octopai-router --config config/local_mesh.toml

```

---

## 🤝 Contributing

We welcome contributions from researchers, Rustaceans, and AI engineers. Please see `CONTRIBUTING.md` for our guide on submitting pull requests, writing tests, and participating in architecture discussions.

## 📄 License

OctopAI is licensed under the Apache 2.0 License. See `LICENSE` for more information.
