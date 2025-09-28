# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a research repository for hypercerts v.2 architecture design and documentation. **The main goal is to write a whitepaper, research paper, or RFC** describing the complete system outlined in `ideas.md` and supported by all materials in `resources/`. The repository contains conceptual materials, architectural diagrams, and research resources for a blockchain-based system for tracking and funding impact work.

## Architecture Concepts

The repository documents a hypercerts v.2 system with these key components:

### Core Architecture
- **ERC4626 vaults for projects**: Projects represented as vaults where shares can be minted to stewards, project owners, and contributors
- **Funding mechanisms**: Early funders buy shares via deposit, grants fund vaults without minting shares
- **EAS attestations**: On-chain attestations for work claims, verifications/evaluations, and endorsements
- **Smart accounts**: Hyper accounts with cross-platform support and Zodiac modules for roles
- **Canonical EVM network**: Single chain chosen for canonical state
- **Ponder indexer**: Multi-chain indexing with embeddings, minhash/simhash for duplicate detection, and spatial queries

### Key Features
- Retrospective funding for impact work
- Fractionalizable hypercerts (ERC-1155)
- Open evaluation system with multiple evaluators
- Attribution tracking and transparent reward distribution
- Interoperable funding mechanisms

### Impact Evaluation
The repository includes research on a hybrid PageRank impact evaluator that:
- Models contributors, artifacts, and outcomes as a directed weighted graph
- Uses hybrid attribution algorithm combining forward and reverse PageRank
- Implements configurable weighting for community governance
- Supports automated attribution and reward distribution
- Aligns with Generalized Impact Evaluators (GIE) framework

## Repository Structure

- `ideas.md` - Core architecture notes and system design (primary source document)
- `resources/` - Supporting documentation and visual resources:
  - `hypercerts_youtube.md` - Detailed summary of hypercerts concepts and retrospective funding mechanisms
  - `github_discussion.md` - Reference to GitHub discussion
  - `use_cases.md` - Specific use cases including scientific research, environmental projects, public goods, and reputation systems
  - `hybrid_pagerank_paper.md` - Academic paper on graph-based impact evaluation using hybrid PageRank algorithm for attribution and reward distribution
  - `*.png` - Architecture diagrams including system overview, data models, UI mockups, and trust graphs
- `research/` - **(Recommended)** Create this folder for structured whitepaper development:
  - `outline.md` - Paper structure and section breakdown
  - `sections/` - Individual sections (abstract, introduction, methodology, etc.)
  - `drafts/` - Complete draft versions
  - `references.md` - Bibliography and citations

## Primary Objective: Whitepaper Development

The main deliverable is a comprehensive whitepaper/research paper that:

1. **Synthesizes** all concepts from `ideas.md` into a coherent narrative
2. **Integrates** supporting materials from `resources/` as evidence and context
3. **Structures** the content as an academic or technical document suitable for:
   - Research publication
   - Technical RFC (Request for Comments)
   - Project whitepaper for implementation

### Recommended Workflow

1. **Analysis Phase**: Review all source materials (`ideas.md` + `resources/`)
2. **Structure Phase**: Create outline based on standard academic paper format
3. **Synthesis Phase**: Combine concepts into cohesive sections
4. **Documentation Phase**: Write complete draft with proper citations
5. **Review Phase**: Iterate on structure and content

## Development Notes

This is a research/documentation repository without traditional build commands or test suites. Work primarily involves:
- Synthesizing architectural concepts into formal documentation
- Creating structured academic or technical papers
- Integrating visual diagrams and supporting research
- Iterating on document structure and content