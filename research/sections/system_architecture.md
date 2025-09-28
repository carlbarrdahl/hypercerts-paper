# 3. System Architecture

## 3.1 Architectural Overview

Hypercerts v.2 implements a three-layer architecture that separates data persistence, business logic, and user interfaces while enabling interoperability across blockchain networks and storage systems. This design allows different components to evolve independently while maintaining system coherence and enabling specialized optimization of each layer.

```
┌─────────────────────────────────────────────────────────────┐
│                    Interface Layer                          │
│  Attestation Creation • Funding UI • Governance Tools      │
└─────────────────────────────────────────────────────────────┘
                                │
┌─────────────────────────────────────────────────────────────┐
│                     Logic Layer                             │
│  ERC4626 Vaults • Smart Accounts • Attribution Engine      │
└─────────────────────────────────────────────────────────────┘
                                │
┌─────────────────────────────────────────────────────────────┐
│                     Data Layer                              │
│  PostgreSQL • IPFS • EAS • Multi-chain Indexing           │
└─────────────────────────────────────────────────────────────┘
```

The architecture implements the Generalized Impact Evaluator framework by distributing its functions across these layers: measurement occurs primarily in the data layer, evaluation in the logic layer, and reward distribution through the combination of logic and interface layers. The scope function spans all layers through filtering and access control mechanisms.

## 3.2 Data Layer Architecture

### 3.2.1 Unified Data Architecture

**Ponder Indexer as Central Database**: Ponder serves as the primary data layer, indexing and normalizing data from multiple sources into a unified PostgreSQL database. This eliminates architectural complexity by having a single source of truth while maintaining data sovereignty across different systems.

**EAS Integration**: Both on-chain and off-chain EAS attestations are indexed by Ponder, which normalizes their different formats into consistent database schemas. This creates a unified view of:

- On-chain attestations (permanent, transparent, higher gas cost)
- Off-chain attestations (flexible, private, lower cost)
- Cross-chain attestations from multiple networks

**IPFS with Storacha**: Provides decentralized storage for attestation metadata, project documentation, and supporting evidence. The content-addressable nature of IPFS ensures data integrity while Storacha's incentive layer provides persistence guarantees. Project vaults include IPFS hash metadata fields that point to detailed project descriptions, contribution guidelines, and evaluation criteria.

**Ethereum Attestation Service (EAS)**: Stores published attestations on-chain for maximum transparency and verifiability. EAS provides standardized schemas for different attestation types and enables composable verification workflows. The system uses EAS for:

- Work claim attestations referencing off-chain evidence
- Verification attestations from evaluating organizations
- Endorsement attestations creating reputation networks
- Project registration and metadata updates

### 3.2.2 Simplified Data Flow

**Unified Indexing**: Ponder eliminates architectural complexity by serving as the single data normalization layer:

1. **Data Creation**: Attestations created via EAS (on-chain or off-chain), funding events into ERC4626 vaults
2. **Data Indexing**: Ponder monitors and indexes all EAS attestations plus blockchain events across multiple networks
3. **Data Normalization**: Ponder transforms diverse attestation schemas and transaction data into unified graph structures
4. **Graph Construction**: Attribution algorithms operate directly on the normalized Ponder database

**Cross-chain Identity**: Smart accounts serve as canonical identity anchors that can operate across multiple blockchain networks. Using account abstraction standards, contributors maintain consistent identities regardless of which network they interact with, enabling attribution that spans chain boundaries.

**Spatial Data Support**: The indexer includes PostGIS extensions for handling geospatial data, enabling location-based impact verification for environmental and social projects. GeoJSON data attached to attestations can support queries like "all forest restoration projects within 100km of this location" or "carbon offset projects in tropical regions."

### 3.2.3 Semantic Search and Duplicate Detection

**Embedding Generation**: The system generates vector embeddings for attestation text using transformer-based language models. These embeddings enable semantic similarity search and help identify potentially duplicate or related claims across different projects and contributors.

**MinHash and SimHash**: Implements locality-sensitive hashing algorithms to efficiently detect near-duplicate content at scale. MinHash identifies similar sets of contributors or project dependencies, while SimHash detects similar textual descriptions or claims.

**Duplicate Resolution Workflows**: When potential duplicates are detected, the system creates flagged review queues where human evaluators can determine whether claims represent legitimate overlapping work, complementary contributions, or actual gaming attempts. This hybrid automated-human approach balances scale with accuracy.

## 3.3 Logic Layer Architecture

### 3.3.1 ERC4626 Vault System

**Tokenized Project Representation**: Each project is represented as an ERC4626 vault that holds assets and manages shares representing different forms of ownership and participation. This standard interface enables composability with existing DeFi infrastructure while providing project-specific customization.

**Multi-class Share Structure**: Vaults support different share classes with distinct rights and characteristics:

- **Contributor shares**: Minted to contributors based on verified work claims
- **Steward shares**: Allocated to project maintainers and governance participants
- **Founder shares**: Reserved for project initiators with potential vesting schedules
- **Investor shares**: Purchased by early funders through deposit mechanisms

**Value Accrual Mechanisms**: Vault value increases through multiple channels:

- Grant funding deposited without minting new shares (pure value increase)
- Fee capture from project usage or derivative works
- Retrospective funding allocated based on demonstrated impact
- Secondary market appreciation of vault shares

### 3.3.2 Smart Account Integration

**Canonical Identity System**: Each participant maintains a smart account that serves as their canonical identity across the system. These accounts integrate with existing identity providers while maintaining sovereignty and portability.

**Multi-signature and Role-based Access**: Organizations can deploy multi-signature smart accounts with role-based permissions using Zodiac modules. This enables complex governance structures while maintaining security and accountability. The smart contract also includes a Metadata module that contains information about the Organizations (this is picked up by the Ponder indexer).

**Cross-platform Compatibility**: Smart accounts implement account abstraction standards that enable operation across different blockchain networks and integration with traditional systems through API bridges.

### 3.3.3 Attestation Processing Engine

**Schema Validation**: Enforces standardized schemas for different types of attestations while enabling community-specific extensions. Core schemas include work claims, verifications, endorsements, and resource allocations.

**Workflow Management**: Implements state machines for attestation lifecycles, including draft creation, collaborative editing, verification processes, and publication workflows. Different attestation types can follow different approval processes based on their schemas and risk profiles.

**Privacy Controls**: Manages access permissions for different attestation visibility levels:

- **Private**: Visible only to attestation creator and explicitly authorized parties
- **Organizational**: Visible within specific organizations or project boundaries
- **Public Draft**: Visible to community for review and comment before publication
- **Published**: Permanently published to EAS with full transparency

## 3.4 Attribution and Evaluation Architecture

### 3.4.1 EAS-Based Graph Construction

**Attestation-Driven Node Creation**: The system extracts graph nodes directly from EAS attestations indexed by Ponder:

- **Agents**: Contributors, evaluators, and organizations referenced in attestations
- **Artifacts**: Projects, repositories, papers, and works claimed or evaluated
- **Outcomes**: Funding events, grants, citations, and impact measurements

**Graph Edges from Attestation Types**: Relationships are derived from standardized EAS attestation schemas:

- **Work Claims**: Create Agent → Artifact edges (contribution relationships)
- **Evaluations**: Generate Outcome → Artifact edges (impact valuation)
- **Endorsements**: Form Agent → Agent edges (trust and reputation)
- **Funding Events**: Produce Outcome → Vault edges (financial flows)
- **Dependencies**: Link Artifact → Artifact edges (building upon prior work)

**Weight Calculation**: Edge weights combine multiple factors:

- Attestation confidence scores provided by creators
- Community verification status and reputation
- Temporal decay functions for aging contributions
- Domain-specific multipliers for different edge types

### 3.4.2 Hybrid PageRank Implementation

**Forward Pass**: Computes structural importance by running standard PageRank on the contribution graph. This rewards agents and artifacts that are well-connected and serve as hubs in the contribution network, regardless of outcome realization.

**Reverse Pass**: Reverses edges from outcome nodes and runs personalized PageRank with outcomes as personalization seeds. This propagates credit backward from demonstrated value to the agents and artifacts that contributed to that value.

**Hybrid Combination**: Final scores combine forward and reverse rankings using a configurable balance parameter α:

```
Score(agent) = α × Forward_Score(agent) + (1-α) × Reverse_Score(agent)
```

**Configuration Management**: Communities can adjust evaluation parameters through governance mechanisms:

- Balance parameter α (structural vs. outcome emphasis)
- Edge type multipliers (relative importance of different contribution types)
- Temporal decay rates (how quickly old contributions lose weight)
- Personalization vectors (which outcomes to emphasize)

### 3.4.3 Reward Distribution System

**Score Normalization**: Attribution scores are normalized to sum to 1.0 within each evaluation scope, enabling proportional distribution of fixed reward pools.

**Multi-pool Support**: The system can simultaneously manage multiple reward pools with different distribution criteria:

- Project-specific pools funded by project revenues
- Cross-project pools for infrastructure contributions
- Time-bounded pools for specific funding rounds
- Stakeholder-specific pools (e.g., only for certain contributor classes)

**Continuous vs. Batch Distribution**: Supports both continuous reward distribution (as new funding arrives) and batch distribution (periodic reward rounds with accumulated funds).

**Counterfactual Analysis**: Provides tools for analyzing how reward distributions would change under different parameter settings or data scenarios, enabling communities to understand the effects of their governance decisions.

## 3.5 Integration and Interoperability

### 3.5.1 External System Integration

**API Layer**: RESTful and GraphQL APIs enable integration with existing project management tools, version control systems, and funding platforms. Standard schemas facilitate data exchange while preserving system autonomy.

**Webhook System**: Real-time notifications enable responsive integration with external systems. Projects can receive notifications about new funding, attestations, or evaluation updates to trigger automated workflows.

**Bridge Protocols**: Standardized protocols enable other systems to contribute data to or consume data from the Hypercerts system while maintaining data sovereignty and user privacy preferences.

### 3.5.2 Governance Integration

**Modular Governance**: Different system components can be governed independently, enabling specialized expertise while maintaining system coherence:

- Technical parameters (algorithm settings) governed by technical experts
- Evaluation criteria governed by domain communities
- Funding allocation governed by stakeholder representatives

**Upgrade Pathways**: Smart contract architecture supports upgrades to evaluation algorithms and system components while preserving data continuity and user consent.

**Exit Rights**: Participants maintain rights to export their data and migrate to alternative systems, preventing lock-in and ensuring competitive pressure for system quality.

The architecture's modularity and standards-based design enable it to function as infrastructure for a broader ecosystem of impact funding tools while providing a complete, integrated system for organizations that prefer comprehensive solutions. This balance between integration and modularity reflects the core design philosophy of enabling coordination without requiring consensus on all system aspects.
