# 5. Impact Evaluation Method

## 5.1 Graph-Based Attribution Model

### 5.1.1 Heterogeneous Graph Representation

The impact evaluation system models contribution networks as directed, weighted, heterogeneous graphs G = (V, E) where nodes represent different types of entities and edges encode various relationships between them. This graph-theoretic approach enables systematic analysis of complex contribution patterns that span multiple projects, organizations, and domains.

**Node Types and Classification**:
- **Agents (A)**: Individual contributors, organizations, institutions, and other actors who perform work or make decisions. Examples include researchers, developers, project maintainers, funding organizations, and evaluation bodies.
- **Artifacts (B)**: Tangible outputs and intermediate products created through work. Examples include code repositories, research papers, datasets, designs, protocols, and documentation.
- **Outcomes (C)**: Observable value signals that indicate impact realization. Examples include grant awards, citations, downloads, adoption metrics, revenue generation, and social impact measurements.

**Edge Types and Semantics**:
- **Creation edges (A → B)**: Link agents to artifacts they created, with weights reflecting effort contribution, leadership roles, or authorship shares.
- **Contribution edges (A → C)**: Connect agents to outcomes they helped achieve, including both direct attribution and collaborative contributions.
- **Dependency edges (B → B)**: Relate artifacts that build upon, cite, or incorporate other artifacts, enabling transitive attribution through dependency chains.
- **Valuation edges (C → B)**: Connect outcomes to the artifacts they recognize or reward, such as grants funding specific projects or citations acknowledging particular works.
- **Attribution edges (C → A)**: Direct connections from outcomes to agents, representing explicit recognition or reward allocation.

### 5.1.2 Weight Calculation and Confidence Scoring

**Multi-factor Weight Computation**: Edge weights combine several factors to reflect the strength and reliability of relationships:

```
Weight(e) = Base_Weight(e) × Confidence(e) × Type_Multiplier(e) × Temporal_Decay(e)
```

- **Base Weight**: The fundamental strength of the relationship, derived from attestations, transaction amounts, citation counts, or other quantitative measures.
- **Confidence Score**: Community assessment of relationship reliability, incorporating verification status, reviewer reputation, and evidence quality.
- **Type Multiplier**: Community-configured parameters that adjust the relative importance of different edge types based on domain-specific value systems.
- **Temporal Decay**: Time-based discounting that prevents old contributions from dominating current evaluations while preserving historical attribution.

**Confidence Scoring Framework**: The system implements a multi-layered confidence assessment:
- **Self-reported confidence**: Creators provide initial confidence estimates based on their certainty about the relationship
- **Peer verification**: Community members can verify or dispute claims, with verification weighted by reviewer reputation
- **Automated consistency checks**: Algorithms identify potential inconsistencies or anomalies that may indicate errors or gaming attempts
- **Cross-reference validation**: Claims are checked against external data sources where available (blockchain transactions, public repositories, citation databases)

### 5.1.3 Dynamic Graph Construction

**Incremental Updates**: The graph structure updates continuously as new attestations are created, existing claims are verified, and temporal decay functions reduce the weight of aging relationships. This enables real-time attribution that responds to evolving contribution patterns.

**Scope Management**: Different evaluation contexts require different graph scopes. The system supports:
- **Project-specific graphs**: Focus on contributions within individual projects
- **Domain-specific graphs**: Include related projects within specific fields (e.g., climate research, open-source security tools)
- **Cross-domain graphs**: Capture interdisciplinary contributions and infrastructure work that spans multiple domains
- **Temporal scoping**: Limit analysis to specific time periods or include historical contributions with appropriate decay

**Missing Node Handling**: The graph model gracefully handles incomplete information by creating placeholder nodes for entities that are referenced but not fully characterized. This enables attribution to flow through unknown intermediaries while identifying areas where additional data collection might improve accuracy.

## 5.2 Hybrid PageRank Algorithm

### 5.2.1 Forward Influence Propagation

The forward pass computes structural importance using standard PageRank on the original graph structure. This measures how agents and artifacts contribute to the overall network structure and identifies nodes that serve as important hubs or connectors in the contribution ecosystem.

**Algorithm Specification**:
```
PR_forward(v) = (1-d)/N + d × Σ(u→v) [PR_forward(u) × Weight(u,v) / OutDegree_weighted(u)]
```

Where:
- d is the damping factor (typically 0.85)
- N is the number of nodes in the graph
- Weight(u,v) is the edge weight from node u to node v
- OutDegree_weighted(u) is the sum of weights of outgoing edges from u

**Interpretation**: Forward scores reflect how much influence a node has based on its position in the contribution network. Agents with high forward scores are well-connected contributors who create many artifacts or collaborate with many other contributors. Artifacts with high forward scores are widely used, cited, or built upon by others.

### 5.2.2 Reverse Credit Attribution

The reverse pass propagates credit backward from outcome nodes to identify which agents and artifacts contributed most to valuable outcomes. This involves reversing edges that originate from outcome nodes while maintaining the direction of other edges, then running personalized PageRank with outcome nodes as personalization seeds.

**Graph Transformation**:
- Edges originating from outcome nodes (C → *) are not reversed, allowing value to flow outward
- All other edges are reversed to enable credit to flow backward through the contribution chain
- Edge weights are preserved but may be modulated by confidence scores and type multipliers

**Personalized PageRank Computation**:
```
PR_reverse(v) = (1-d) × PersonalizationVector(v) + d × Σ(u→v) [PR_reverse(u) × Weight(u,v) / OutDegree_weighted(u)]
```

Where PersonalizationVector(v) = OutcomeValue(v) / TotalOutcomeValue for outcome nodes, 0 for other nodes.

**Interpretation**: Reverse scores reflect how much credit each node deserves based on its contribution to observed valuable outcomes. High reverse scores indicate nodes that are causally connected to realized value, either directly or through chains of contribution.

### 5.2.3 Hybrid Score Combination

The final attribution score combines forward and reverse rankings using a configurable balance parameter α that enables communities to adjust the relative emphasis on structural importance versus outcome-based attribution:

```
HybridScore(agent) = α × PR_forward(agent) + (1-α) × PR_reverse(agent)
```

**Parameter Interpretation**:
- α = 1: Pure structural importance (rewards network centrality regardless of outcomes)
- α = 0: Pure outcome-based attribution (rewards only proximity to demonstrated value)
- α = 0.5: Balanced approach giving equal weight to structure and outcomes

**Community Configuration**: Different domains and communities may prefer different balance points:
- **Research communities** might emphasize outcomes (α ≈ 0.3) to reward impact over productivity
- **Infrastructure projects** might emphasize structure (α ≈ 0.7) to reward foundational work that enables others
- **Commercial projects** might use balanced approaches (α ≈ 0.5) to reward both innovation and execution

### 5.2.4 Convergence and Stability Analysis

**Convergence Guarantees**: The hybrid algorithm inherits convergence properties from standard PageRank. Under standard conditions (strongly connected graph, positive edge weights), both forward and reverse passes converge to unique stationary distributions.

**Sensitivity Analysis**: The system provides tools for analyzing how attribution scores change in response to:
- Parameter variations (α, damping factor, type multipliers)
- Data perturbations (adding or removing nodes/edges)
- Temporal changes (evolution of the graph over time)

**Stability Metrics**: Regular computation of stability metrics helps identify when attribution results are robust versus when they depend heavily on specific parameter choices or data points.

## 5.3 Configurable Evaluation Parameters

### 5.3.1 Community Governance of Algorithms

**Parameter Spaces**: The evaluation system exposes multiple configuration parameters that communities can adjust through governance processes:
- **Balance parameter (α)**: Controls the forward/reverse hybrid combination
- **Edge type multipliers**: Adjust relative importance of different relationship types
- **Node type multipliers**: Weight different entity classes (agents vs. artifacts vs. outcomes)
- **Temporal decay rates**: Control how quickly old contributions lose influence
- **Confidence thresholds**: Set minimum confidence levels for including relationships

**Governance Mechanisms**: Parameter adjustment follows domain-appropriate governance processes:
- **Technical parameters** (convergence criteria, computational limits) governed by system maintainers
- **Evaluation methodology** (α, multipliers) governed by domain expert communities
- **Scope and inclusion criteria** governed by stakeholder representatives

**Impact Simulation**: Before implementing parameter changes, communities can simulate the effects on historical data to understand how modifications would affect attribution patterns and identify potential unintended consequences.

### 5.3.2 Domain-Specific Customization

**Academic Research Configuration**: Research communities might configure the system to:
- Heavily weight citation outcomes over download metrics
- Apply strong temporal decay to emphasize recent work
- Use low α values to emphasize impact over productivity
- Implement peer review confidence scoring

**Open Source Software Configuration**: Developer communities might prefer:
- Strong weighting for dependency relationships
- Balanced α values recognizing both infrastructure and application development
- Reputation-based confidence scoring
- Integration with code analysis metrics

**Environmental Impact Configuration**: Conservation projects might emphasize:
- Spatial clustering of related projects
- Long temporal windows to capture slow environmental changes
- Integration with satellite monitoring and field verification data
- Stakeholder diversity in evaluation processes

### 5.3.3 Dynamic Parameter Learning

**Adaptive Algorithms**: Future versions of the system could incorporate machine learning approaches to automatically tune parameters based on community feedback and outcome validation:
- **Preference learning**: Infer community preferences from funding allocation decisions and explicit feedback
- **Outcome prediction**: Optimize parameters to maximize correlation with future realized impact
- **Fairness constraints**: Ensure parameter choices don't systematically disadvantage specific contributor groups

**Multi-objective Optimization**: Parameter tuning must balance multiple objectives including accuracy, fairness, gaming resistance, and computational efficiency. Multi-objective optimization frameworks can help communities navigate these trade-offs explicitly.

## 5.4 Reward Distribution and Normalization

### 5.4.1 Score Normalization

**Proportional Allocation**: Attribution scores are normalized to sum to 1.0 within each evaluation scope, enabling direct proportional distribution of fixed reward pools:

```
NormalizedScore(agent) = HybridScore(agent) / Σ(all_agents) HybridScore(agent)
```

**Multi-pool Management**: The system can simultaneously manage multiple reward pools with different scopes and criteria:
- **Project-specific pools**: Distribute project revenues among project contributors
- **Cross-project pools**: Reward infrastructure work that benefits multiple projects
- **Time-bounded pools**: Allocate funding for specific periods or funding rounds
- **Stakeholder-specific pools**: Separate rewards for different contributor types

### 5.4.2 Continuous vs. Batch Distribution

**Continuous Distribution**: Rewards can be distributed continuously as new funding arrives and attribution scores update. This provides immediate feedback and recognition for contributions while ensuring that reward distribution remains current with evolving contribution patterns.

**Batch Distribution**: Alternative systems accumulate rewards over specified periods (monthly, quarterly, annually) and distribute based on time-averaged attribution scores. This reduces transaction costs and provides predictable reward schedules but may delay recognition of contributions.

**Hybrid Approaches**: Some systems might combine both approaches, providing continuous small rewards for immediate recognition while reserving larger batch distributions for major funding rounds.

### 5.4.3 Counterfactual Analysis and Transparency

**What-if Analysis**: The system provides tools for analyzing how reward distributions would change under different scenarios:
- Removing specific funding sources or outcome measurements
- Adjusting algorithm parameters within reasonable ranges
- Including or excluding specific projects or contributors from evaluation scopes

**Attribution Tracing**: Contributors and funders can trace the specific paths through which attribution scores were calculated, providing transparency and enabling identification of potential errors or gaming attempts.

**Gaming Detection**: Regular counterfactual analysis can identify attribution patterns that might indicate gaming attempts, such as sudden score increases following specific attestation patterns or unusual concentration of rewards among related entities.

The impact evaluation method provides a principled, transparent, and configurable approach to large-scale attribution that can adapt to diverse community needs while maintaining mathematical rigor and gaming resistance. By combining automated algorithmic analysis with community governance and continuous transparency, the system addresses key limitations of both pure expert evaluation (scalability) and pure automated systems (context sensitivity).