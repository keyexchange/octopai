# 🐙 OctopAI: Distributed Cognitive Routing for Agentic AI

**OctopAI** is a resilient, Byzantine Fault Tolerant (BFT) cognitive routing system for multi-agent AI.

Just as an octopus distributes its "brain" across its eight arms—allowing them to process information, react, and solve problems semi-autonomously while coordinating with a central nervous system—OctopAI shatters the monolithic LLM paradigm. It distributes reasoning, tool-execution, and memory across a decentralized web of agentic nodes.

Built as a core component of the KeyExchange.org initiative, OctopAI natively supports decentralized accounting, allowing agents to buy, sell, and share cognitive labor, "products," and context with cryptographically secured provenance.

---

## 🧠 The "Distributed Brain" Architecture

Traditional AI pipelines rely on massive, centralized models acting as single points of failure. OctopAI operates as a **Cognitive AI Fabric**. Tasks are routed dynamically to the most efficient edge nodes, micro-agents, or hardware enclaves based on network topology, cost, and trust metrics.

---
config:
  layout: elk
---
graph TD
    User["Human User / Admin"]:::actor
    Ext_LLM_APIs["External LLM APIs <br/>(OpenAI, Anthropic, etc.)"]:::external
    Vector_DB["Vector Database <br/>(Qdrant)"]:::external
    KeyExchange_Ledger["KeyExchange.org Ledger <br/>(Substrate)"]:::external
    MCP_Sources["MCP Data Sources"]:::external
    subgraph OctopAI_System ["OctopAI Cognitive Fabric System Boundary"]
        User_IF["User Interface <br/>(Web / CLI / API Gateways)"]:::ui
        Nervous_System["Nervous System <br/>(Zenoh Pub/Sub Mesh)"]:::communication
        subgraph Cognitive_Brain ["Cognitive Brain Core"]
            direction TB
            Router["Cognitive Router <br/>(Rust/Go)"]:::core
            BFT_Consensus["BFT Consensus Engine <br/>(Malachite)"]:::bft
            Accounting["Accounting & Provenance <br/>Interface"]:::ledger
            Compression["Graphlink Compression <br/>Algorithm"]:::core
            Logic_Core["Core Logic & RAG <br/>(Rig Lib)"]:::core
        end
        subgraph Distributed_Arms ["Distributed Agents (WasmActors)"]
            direction LR
            Agent_Nodes["Agent Nodes <br/>(wasmCloud Host)"]:::wasm
            Secure_Runtime["Secure Runtime <br/>(ZeroClaw OS)"]:::wasm
            Agent_Logic["Agent Logic <br/>(Rig Lib)"]:::wasm
        end
        Data_Serialization["Data Serialization <br/>(Toon Format)"]:::utility
    end
    User -->|"Issues Queries/Commands"| User_IF
    User_IF -->|"Routes Request"| Router
    Router <-->|"State Agreement"| BFT_Consensus
    Router -->|"Transaction Data"| Accounting
    Router <-->|"Semantic Deltas"| Compression
    Router -->|"RAG Processing"| Logic_Core
    Logic_Core -->|"Message Serialization"| Data_Serialization
    Router <-->|"Control Plane Pub/Sub"| Nervous_System
    Agent_Nodes <-->|"Data Plane Pub/Sub"| Nervous_System
    Agent_Nodes -->|"Format Payloads"| Data_Serialization
    Agent_Nodes -.->|"Executes Within"| Secure_Runtime
    Agent_Nodes -.->|"Invokes"| Agent_Logic
    Agent_Logic -->|"Format Messages"| Data_Serialization
    Router -->|"Final LLM Call"| Ext_LLM_APIs
    Logic_Core -->|"Vector Search"| Vector_DB
    Accounting -->|"Tally Value / Settle"| KeyExchange_Ledger
    Router -.->|"Inject Dynamic Context"| MCP_Sources
    Agent_Logic -.->|"Inject Dynamic Context"| MCP_Sources
    classDef actor fill:#fdb,stroke:#333,stroke-width:2px;
    classDef external fill:#ddd,stroke:#333,stroke-width:2px,stroke-dasharray: 5 5;
    classDef ui fill:#fff,stroke:#333,stroke-width:1px;
    classDef core fill:#bbf,stroke:#333,stroke-width:2px;
    classDef communication fill:#f96,stroke:#333,stroke-width:2px;
    classDef wasm fill:#dfd,stroke:#333,stroke-width:1px;
    classDef bft fill:#fbb,stroke:#333,stroke-width:2px;
    classDef ledger fill:#ffd,stroke:#333,stroke-width:2px;
    classDef utility fill:#eee,stroke:#333,stroke-width:1px,stroke-dasharray: 3 3;

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
