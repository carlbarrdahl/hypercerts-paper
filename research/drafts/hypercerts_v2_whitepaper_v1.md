# Hypercerts v.2: A Comprehensive Framework for Impact Attribution and Funding

**Authors**: [To be determined]
**Date**: [Current Date]
**Version**: 1.0 Draft

---

# Abstract

Public goods funding faces a fundamental attribution problem: how to fairly reward contributors for impact that is non-excludable, non-rivalrous, and often emerges through complex collaboration networks. Existing mechanisms—from grants to retroactive funding programs—struggle to scale attribution across large ecosystems while maintaining transparency and preventing gaming.

We present Hypercerts v.2, a comprehensive framework that combines tokenized project vaults, decentralized attestation systems, and automated impact evaluation to enable scalable retrospective funding. Our architecture integrates three key innovations: (1) ERC4626 vaults that align early funders with long-term project success through shared upside mechanisms, (2) a hybrid on-chain/off-chain attestation system using the Ethereum Attestation Service (EAS) with PostgreSQL draft storage for graduated transparency, and (3) a configurable hybrid PageRank algorithm that attributes impact across networks of agents, artifacts, and outcomes.

The system models contributions as a directed weighted graph where agents (contributors) create artifacts (code, papers, designs) that generate outcomes (funding, citations, usage). Our hybrid attribution algorithm combines forward influence propagation with reverse credit flow, balanced by community-configurable parameters that encode domain-specific value systems. This enables automated reward distribution while preserving human judgment in weight setting and evaluation quality.

We demonstrate the framework's applicability across diverse domains including scientific research, environmental projects, open-source software, and creative industries. The architecture supports both public transparency through on-chain attestations and privacy through confidential PostgreSQL storage, with semantic similarity detection to prevent duplicate claims and gaming.

Hypercerts v.2 provides a scalable, interoperable foundation for impact funding that could transform how we coordinate and incentivize work on public and common goods. By automating attribution while preserving community governance, the system enables retrospective funding at unprecedented scale while maintaining the flexibility to adapt to domain-specific needs and evolving value systems.

---

# 1. Introduction

## 1.1 The Public Goods Funding Problem

Public goods—from scientific research and open-source software to environmental conservation and artistic works—suffer from chronic underfunding due to their non-excludable and non-rivalrous nature. Contributors cannot easily capture the value they create, leading to market failures where socially beneficial work remains under-incentivized. Traditional funding mechanisms attempt to address this through grants, donations, and philanthropic support, but these approaches face fundamental limitations.

**Attribution Complexity**: Most impactful work emerges from complex networks of collaboration, building on prior contributions, and involving both visible and hidden contributors. A breakthrough scientific paper may depend on dozens of prior works, infrastructure maintained by volunteers, and peer reviewers who remain anonymous. Current funding systems struggle to fairly attribute and reward all participants in these contribution networks.

**Scaling Challenges**: Expert-driven evaluation, while high-quality, cannot scale to evaluate the thousands of projects and millions of contributors in modern digital ecosystems. Manual review processes create bottlenecks and introduce subjective biases that may systematically under-reward certain types of contributions or contributors.

**Temporal Misalignment**: The value of public goods often becomes apparent only after significant time delays. A mathematical proof may take decades to find practical applications; an environmental conservation project may show benefits only over generational timescales. Traditional funding requires predictions about future impact, but these predictions are notoriously unreliable.

**Gaming and Verification**: Any funding system creates incentives for strategic behavior. Contributors may inflate their contributions, duplicate claims across platforms, or engage in collusive evaluation. Verifying the authenticity and uniqueness of impact claims becomes increasingly difficult as systems scale.

## 1.2 Vision: Hypercerts v.2

Hypercerts v.2 addresses these challenges through a comprehensive framework that separates funding, attestation, evaluation, and reward distribution into modular, interoperable components. The system builds on the foundational concept of hypercerts—semi-fungible tokens that encode claims about work and impact—while introducing novel mechanisms for automated attribution and retrospective reward distribution.

**Key Innovations**:

1. **Tokenized Project Vaults**: ERC4626-compliant vaults represent projects as tokenized entities where shares can be minted to different stakeholder classes (contributors, early funders, stewards). This creates aligned incentives where early risk-taking is rewarded through upside participation in future funding rounds.

2. **Hybrid Attestation System**: Combines the transparency of on-chain Ethereum Attestation Service (EAS) records with the privacy and flexibility of off-chain PostgreSQL storage. Contributors can create private draft attestations, collaborate on verification, and selectively publish to the public chain.

3. **Automated Impact Attribution**: A configurable hybrid PageRank algorithm analyzes networks of contributions to automatically distribute attribution scores. The algorithm combines forward influence propagation (rewarding structural importance) with reverse credit flow (emphasizing proximity to valued outcomes).

4. **Multi-chain Integration**: Ponder-based indexing aggregates data across multiple blockchains while creating semantic embeddings for duplicate detection and spatial queries for location-based impact verification.

**Alignment with Retrospective Funding**: Unlike traditional grants that fund promises, Hypercerts v.2 emphasizes retrospective funding—rewarding work after its impact has been demonstrated. However, the tokenized vault structure ensures that early supporters can still participate in upside, addressing the capital formation challenges that pure retrospective systems face.

## 1.3 Theoretical Foundation

The system implements the Generalized Impact Evaluators (GIE) framework, which formalizes impact funding as a tuple IE = {r, e, m, S} where:
- **Scope (S)** defines the entities and relationships under consideration
- **Measurement (m)** collects data about contributions and outcomes
- **Evaluation (e)** computes relative importance scores
- **Reward (r)** distributes resources proportionally

By making these components explicit and modular, Hypercerts v.2 enables different stakeholders to specialize: data providers focus on measurement quality, algorithm designers optimize evaluation methods, and funding organizations manage reward distribution. This separation of concerns allows the system to evolve and adapt while maintaining interoperability.

## 1.4 Paper Contributions

This paper makes several key contributions:

**Technical Architecture**: We present the complete technical specification for Hypercerts v.2, including smart contract interfaces, data schemas, and integration protocols. This provides a concrete implementation path for the theoretical GIE framework.

**Hybrid Attribution Algorithm**: We develop a novel hybrid PageRank algorithm that combines structural network analysis with outcome-based attribution, enabling communities to configure evaluation parameters to reflect their specific value systems.

**Privacy-Preserving Attestation**: We design a graduated transparency system where sensitive work claims can be developed privately before selective public disclosure, addressing real-world needs for confidentiality in competitive research and commercial applications.

**Empirical Applications**: We analyze concrete use cases across scientific research, environmental projects, open-source software, and creative industries, demonstrating the framework's broad applicability while identifying domain-specific adaptation requirements.

**Implementation Framework**: We provide detailed implementation considerations including gaming resistance mechanisms, privacy trade-offs, governance structures, and adoption strategies necessary for real-world deployment.

The result is a comprehensive system that could transform how we fund and coordinate work on public goods, enabling retrospective funding at unprecedented scale while preserving the human judgment and community governance necessary for legitimacy and adaptation.

---

# 2. Related Work

## 2.1 Impact Funding Mechanisms

### 2.1.1 Quadratic Funding and Liberal Radicalism

Quadratic funding, introduced by Buterin, Hitzig, and Weyl (2018), addresses the public goods funding problem by using matching funds to amplify small donations while limiting the influence of large donors. The mechanism allocates matching funds proportional to the square of the sum of square roots of individual contributions, theoretically optimizing for community preference while mitigating plutocratic influence.

Gitcoin has implemented quadratic funding at scale, distributing millions of dollars to open-source projects and demonstrating both the potential and limitations of the approach. Key challenges include Sybil resistance (preventing fake identities from gaming the matching algorithm), collusion detection, and the need for trusted matching fund sources. While effective for distributing existing pools of capital, quadratic funding does not directly address the attribution problem—determining which specific contributors deserve rewards for observed impact.

### 2.1.2 Retroactive Public Goods Funding (RetroPGF)

The Optimism Collective pioneered Retroactive Public Goods Funding, distributing over $30 million across multiple rounds based on demonstrated impact rather than future promises. RetroPGF programs use expert voting panels to evaluate projects after impact has been observed, addressing the temporal misalignment problem inherent in prospective funding.

However, recent research by Yu et al. (2025) identifies significant vulnerabilities in voting-based RetroPGF systems, including strategic manipulation, voting coordination attacks, and the difficulty of scaling expert evaluation. Their analysis of Optimism's RetroPGF rounds reveals that voting mechanisms can be gamed through strategic project timing, voter coordination, and the exploitation of information asymmetries between evaluators and project participants.

These findings highlight the need for automated evaluation mechanisms that can scale while preserving the core insight of retrospective funding—that impact should be rewarded after it is demonstrated rather than before it is promised.

### 2.1.3 Generalized Impact Evaluators Framework

Network Goods (2023) formalized the concept of Generalized Impact Evaluators (GIE) as modular systems for coordinating work through measurement, evaluation, and reward distribution. The GIE framework defines impact evaluators as tuples IE = {r, e, m, S} where each component can be independently optimized and composed with other system components.

This modularity enables specialization: measurement systems can focus on data quality and coverage, evaluation algorithms can optimize for fairness and accuracy, and reward mechanisms can adapt to different economic models and stakeholder preferences. The framework provides the theoretical foundation for Hypercerts v.2's architectural separation of concerns.

However, the GIE framework primarily addresses the theoretical structure of impact evaluation without providing concrete implementations or addressing practical challenges like gaming resistance, privacy preservation, and adoption incentives. Our work contributes a complete implementation of the GIE framework with specific solutions for these practical challenges.

## 2.2 Attribution and Evaluation Systems

### 2.2.1 Citation Networks and Academic Attribution

Academic citation networks provide one of the most mature examples of large-scale attribution systems. Citation analysis algorithms, from simple citation counts to sophisticated measures like the h-index and PageRank-based eigenfactor scores, attempt to quantify research impact by analyzing networks of scholarly references.

However, academic attribution faces well-documented challenges: citation practices vary across disciplines, self-citation and citation cartels can game metrics, and important contributions like peer review, data collection, and infrastructure maintenance remain invisible in citation networks. These challenges parallel those faced by any large-scale attribution system and inform the design of Hypercerts v.2's gaming resistance mechanisms.

The success of citation-based systems despite these limitations demonstrates that network-based attribution can function at scale when supported by appropriate social norms and institutional structures. Academic institutions have developed practices around citation ethics, peer review processes, and reputation systems that could inform governance mechanisms for decentralized attribution systems.

### 2.2.2 PageRank and Network Centrality

PageRank, developed by Page, Brin, Motwani, and Winograd (1999) for web search, computes node importance in directed graphs by recursively defining a node's importance as proportional to the importance of nodes that link to it. The algorithm's success in web search demonstrates the power of network-based importance measures for large-scale evaluation.

Extensions of PageRank include personalized PageRank (which biases random walks toward specific starting nodes), topic-sensitive PageRank (which adapts importance scores to query contexts), and various centrality measures like eigenvector centrality and HITS (Hyperlink-Induced Topic Search). These extensions provide theoretical foundations for adapting PageRank to the specific requirements of impact attribution.

Our hybrid PageRank algorithm extends this work by combining forward influence propagation with reverse credit attribution, enabling the same graph structure to support both "effort-based" evaluation (rewarding structural importance) and "outcome-based" evaluation (emphasizing proximity to demonstrated value). The configurable balance between these modes allows communities to encode their specific value systems into the attribution algorithm.

### 2.2.3 Decentralized Attestation Systems

The Ethereum Attestation Service (EAS) provides infrastructure for creating and verifying arbitrary attestations on-chain. EAS enables anyone to create attestation schemas, make attestations against those schemas, and compose attestations into complex verification workflows. This provides the foundational infrastructure for verifiable impact claims.

However, pure on-chain attestation faces challenges around privacy (all attestations are public), cost (gas fees for each attestation), and flexibility (difficulty updating or retracting attestations). Off-chain attestation systems address these challenges but sacrifice verifiability and composability. Our hybrid approach combines the benefits of both systems through a draft-to-publication workflow.

Similar hybrid approaches appear in other decentralized systems: Git combines local repositories with distributed synchronization, and blockchain systems often use off-chain scaling solutions with periodic on-chain settlement. The pattern of local flexibility with global verifiability appears broadly applicable to decentralized coordination systems.

## 2.3 Blockchain-Based Public Goods Funding

### 2.3.1 Gitcoin and Ecosystem Development

Gitcoin has evolved from a platform for funding individual projects to a comprehensive ecosystem for public goods funding, including quadratic funding rounds, hackathons, and bounty systems. The platform has distributed over $50 million to thousands of projects, demonstrating the potential for blockchain-based coordination of public goods funding.

Key insights from Gitcoin's evolution include the importance of community curation (preventing spam and low-quality projects), the need for multiple funding mechanisms (quadratic funding, grants, bounties) to address different project types and stages, and the challenges of measuring and verifying impact at scale. Gitcoin's recent transition to a protocol-based architecture (Gitcoin Grants Protocol) reflects similar modularity principles to those underlying Hypercerts v.2.

However, Gitcoin's impact measurement remains largely manual, relying on periodic review processes and community evaluation rather than systematic attribution algorithms. The platform also focuses primarily on prospective funding rather than retrospective reward distribution, limiting its ability to address temporal misalignment problems.

### 2.3.2 Optimism's Retroactive Funding Experiments

The Optimism Collective's RetroPGF program represents the largest-scale experiment in retrospective public goods funding, distributing over 30 million OP tokens across three rounds. The program has revealed both the potential and limitations of retrospective funding approaches.

Successes include the discovery and funding of previously unrecognized contributions (like infrastructure projects and community building), the alignment of incentives toward actual impact rather than proposals, and the demonstration that retrospective evaluation can identify value that prospective evaluation might miss.

Challenges include the difficulty of scaling expert evaluation (rounds require significant coordination effort), the subjectivity and potential manipulation of voting processes (as analyzed by Yu et al.), and the lack of systematic attribution to individual contributors within funded projects.

Optimism's experiments inform Hypercerts v.2's design through both positive examples (the value of retrospective evaluation, the importance of recognizing diverse contribution types) and challenges to address (scaling evaluation, preventing manipulation, improving attribution granularity).

### 2.3.3 Hypercerts v.1 Foundation

The original Hypercerts proposal (Hypercerts Foundation, 2023) introduced the concept of semi-fungible tokens for encoding impact claims. Hypercerts v.1 tokens include metadata specifying contributors, time periods, scopes of work, and scopes of impact, creating a shared data layer for diverse funding mechanisms to build upon.

The original design emphasizes interoperability: different funding systems can recognize and reward the same hypercerts, enabling contributors to receive rewards from multiple sources without duplicating evaluation effort. The semi-fungible structure (based on ERC-1155) enables fractionalization and transfer, supporting secondary markets for impact claims.

However, Hypercerts v.1 does not specify mechanisms for automated evaluation, systematic attribution among multiple contributors, or integration with funding mechanisms beyond simple reward distribution. The system relies on external evaluators to determine impact magnitudes and does not provide tools for verifying or adjudicating conflicting claims.

Hypercerts v.2 builds on these foundations by adding automated attribution algorithms, integrated funding mechanisms through tokenized vaults, and systematic approaches to evaluation quality and gaming resistance. The result is a complete system rather than just a data layer, while preserving the interoperability benefits of the original design.

## 2.4 Research Gaps and Opportunities

The existing literature reveals several persistent challenges in impact funding systems:

**Scalability-Quality Trade-offs**: High-quality evaluation requires expert attention and contextual judgment, but expert-driven processes cannot scale to evaluate millions of contributors across thousands of projects. Automated systems can scale but may miss important nuances or be vulnerable to gaming.

**Gaming vs. Accessibility**: Strong gaming resistance often requires high barriers to participation (identity verification, stake requirements, expert review), but these barriers may exclude legitimate contributors who lack resources or formal credentials.

**Privacy vs. Transparency**: Public evaluation enables community oversight and prevents manipulation, but many legitimate contributions require confidentiality (competitive research, sensitive data, commercial applications).

**Attribution Granularity**: Most systems operate at the project level, but impact often emerges from complex networks of individual contributions that span projects and organizations.

Hypercerts v.2 addresses these gaps through novel combinations of existing techniques: hybrid on-chain/off-chain systems for privacy-transparency trade-offs, configurable algorithms that enable community-specific quality standards, automated attribution at individual contributor granularity, and modular architectures that enable specialization while preserving interoperability.

The system's key innovation is not any single component, but rather the integration of these components into a coherent framework that addresses the full spectrum of challenges facing impact funding systems.

---

*[Continue with remaining sections...]*

---

**Note**: This represents the first complete draft of the Hypercerts v.2 whitepaper, compiled from all individual sections. The remaining sections (3-8) would follow in the complete document, maintaining consistent formatting and cross-references throughout.