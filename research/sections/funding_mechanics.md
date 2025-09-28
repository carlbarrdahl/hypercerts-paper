# 4. Funding Mechanics

## 4.1 Vault-Based Project Funding Model

### 4.1.1 ERC4626 Vault Structure

Hypercerts v.2 represents each project as an ERC4626-compliant vault that serves as both a funding vehicle and a coordination mechanism. Unlike traditional project funding where capital flows directly to project accounts, the vault structure creates a persistent entity that can accumulate value over time while maintaining transparent governance and accountability.

**Asset Management**: Vaults hold multiple asset types including stablecoins, ETH, governance tokens, and other digital assets. The standardized ERC4626 interface ensures compatibility with existing DeFi infrastructure while enabling project-specific customization of deposit and withdrawal mechanics.

**Share Token Economics**: Vault shares represent proportional ownership in the project's accumulated value and future cash flows. The total value of shares increases through multiple mechanisms:
- Grant deposits that add assets without minting new shares
- Revenue generation from project usage or licensing
- Retrospective funding based on demonstrated impact
- Appreciation of held assets and governance tokens

**Metadata Integration**: Each vault includes IPFS metadata hashes that point to comprehensive project documentation including contribution guidelines, evaluation criteria, governance structures, and impact measurement frameworks. This creates a verifiable link between the financial instrument (vault shares) and the project's actual work and impact.

### 4.1.2 Multi-Stakeholder Share Classes

The vault system supports differentiated share classes that align different stakeholder incentives while maintaining overall project coherence:

**Contributor Shares**: Minted to individuals and organizations based on verified work contributions. These shares carry both economic rights (proportional reward distribution) and governance rights (voting on project direction). Contributor shares can be:
- **Performance-based**: Minted based on measured outputs (code commits, papers published, experiments completed)
- **Impact-based**: Allocated through the attribution algorithm based on downstream value creation
- **Time-based**: Earned through sustained participation and stewardship activities

**Early Funder Shares**: Purchased by investors and supporters through the vault's deposit mechanism. Early funders provide essential capital for project initiation and operation while receiving potential upside through share appreciation. Key features include:
- **Risk-adjusted pricing**: Share prices may reflect project risk and development stage
- **Vesting schedules**: Shares may vest over time to encourage long-term alignment
- **Liquidity mechanisms**: Secondary markets enable early funders to exit while preserving project continuity

**Steward Shares**: Allocated to project maintainers, governance participants, and community builders who provide ongoing coordination and maintenance. Stewardship activities include:
- Technical maintenance and security updates
- Community building and contributor onboarding
- Governance participation and dispute resolution
- External relationship management and partnership development

**Founder Shares**: Reserved for project initiators with potential vesting schedules that align founder incentives with long-term project success. Founder allocation policies vary by project but typically include:
- Initial allocation based on pre-launch contributions
- Ongoing allocation based on leadership and vision
- Vesting terms that encourage sustained commitment
- Dilution protection mechanisms for major value creation events

### 4.1.3 Value Accrual and Distribution

**Grant Integration**: Traditional grants can fund vault operations without diluting existing shareholders by depositing assets directly into the vault. This increases the net asset value per share while preserving the proportional ownership structure. Grant providers may:
- Specify how funds should be allocated across different project activities
- Require reporting on fund usage and impact achievement
- Establish milestone-based disbursement schedules
- Retain governance rights proportional to their funding contribution

**Revenue Capture**: Projects that generate revenue through licensing, services, or product sales can direct these funds to the vault, benefiting all stakeholders proportionally. Revenue streams may include:
- Software licensing and support contracts
- Research data and analysis services
- Educational content and training programs
- Consulting and implementation services

**Retrospective Funding Integration**: When external retrospective funding programs (like Optimism RetroPGF or private foundation grants) reward projects, these funds flow to vaults and increase share value. The automated attribution system can provide evidence for funding applications and distribute awards appropriately among contributors.

## 4.2 Stakeholder Incentive Alignment

### 4.2.1 Early Funder Reward Mechanisms

Early funders face significant risk when supporting projects with uncertain outcomes. The vault structure addresses this through several mechanisms that provide upside participation while protecting against total loss:

**Shared Upside**: When projects receive grants, achieve adoption milestones, or generate revenue, early funders benefit through share appreciation rather than just receiving reports on fund usage. This creates incentive alignment between funders and projects.

**Risk Diversification**: Funders can purchase shares in multiple project vaults, creating portfolio effects that reduce overall risk while maintaining exposure to high-potential projects.

**Secondary Markets**: Share transferability enables early funders to exit positions as projects mature and risk profiles change, providing liquidity that traditional grant funding lacks.

**Governance Participation**: Early funders receive voting rights proportional to their share ownership, enabling them to influence project direction and protect their investments through active governance participation.

### 4.2.2 Contributor Incentive Structures

Contributors need assurance that their efforts will be fairly recognized and rewarded, particularly for high-risk, high-impact work that may not show immediate results:

**Immediate Recognition**: Contributor shares are minted based on verified work claims, providing immediate tokenization of contributions even before impact is fully realized.

**Long-term Upside**: As projects succeed and attract funding, contributor shares appreciate in value, ensuring that contributors benefit from the long-term success of their work.

**Cross-project Attribution**: The global attribution system enables contributors to receive recognition and rewards for infrastructure work that benefits multiple projects, addressing the underinvestment problem in shared resources.

**Reputation Building**: Verified contributions and successful project outcomes build contributor reputation scores that influence future share allocations and funding opportunities.

### 4.2.3 Grant Provider Value Proposition

Traditional grant providers (foundations, governments, DAOs) gain several advantages from integrating with the vault system:

**Increased Impact Leverage**: Grant funds that increase vault value benefit all stakeholders, creating multiplicative effects where grant funds attract additional investment and contributor effort.

**Transparent Impact Tracking**: The integrated attribution and evaluation system provides grant providers with detailed evidence of fund usage and impact achievement, addressing accountability requirements.

**Reduced Due Diligence Costs**: Standardized project vaults with consistent reporting and evaluation mechanisms reduce the cost and complexity of grant evaluation and monitoring.

**Portfolio Management**: Grant providers can maintain ongoing relationships with funded projects through share ownership rather than terminating involvement after grant disbursement.

## 4.3 Dynamic Funding Flows

### 4.3.1 Continuous Funding Model

Unlike traditional funding cycles that require periodic application and approval processes, the vault system enables continuous funding flows that respond dynamically to project performance and community needs:

**Performance-Based Allocation**: Automated systems can direct funding to high-performing projects based on attribution scores, usage metrics, or impact assessments. This creates competitive pressure for projects to maximize their effectiveness.

**Community-Driven Funding**: Token holders in broader ecosystem governance systems can vote to direct treasury funds to specific project vaults based on strategic priorities and community needs.

**Revenue Sharing**: Projects can establish revenue sharing agreements where successful projects contribute portions of their earnings to fund related infrastructure or early-stage projects.

### 4.3.2 Cross-Project Coordination

The shared infrastructure and standardized interfaces enable coordination mechanisms that span individual projects:

**Infrastructure Funding**: Critical infrastructure projects (security tools, development frameworks, educational resources) can receive funding from multiple project vaults that benefit from their work.

**Collaborative Research**: Multi-project research initiatives can pool funding from participating projects while maintaining clear attribution and reward distribution.

**Risk Sharing**: Project vaults can form mutual insurance pools that provide support during development challenges or external shocks.

### 4.3.3 Temporal Coordination

The system addresses temporal misalignment between funding needs and impact realization through several mechanisms:

**Bridge Funding**: Early funders provide capital for immediate needs while retrospective funders provide rewards based on eventual impact realization.

**Milestone-Based Release**: Funding can be released based on achievement of specific milestones or evaluation thresholds rather than arbitrary time schedules.

**Impact Bonds**: Projects can issue bonds against future retrospective funding, enabling immediate capital access while providing returns to bondholders when impact is realized and rewarded.

## 4.4 Economic Security and Sustainability

### 4.4.1 Gaming Resistance

The financial incentives created by the vault system require careful design to prevent gaming and ensure that value flows to genuine contributors:

**Stake-Based Participation**: Certain activities (like project governance or high-value attestations) may require stake deposits that are forfeited if gaming is detected.

**Reputation Weighting**: Attribution scores incorporate contributor reputation, making it costly to create new identities for gaming purposes.

**Community Oversight**: Share holders have economic incentives to prevent gaming that would dilute vault value, creating distributed enforcement mechanisms.

**Multi-Signal Evaluation**: The attribution algorithm incorporates multiple types of evidence rather than relying on single metrics that might be easily gamed.

### 4.4.2 Sustainability Mechanisms

**Fee Capture**: The system can capture fees from various activities (share transfers, attestation creation, evaluation services) to fund ongoing development and maintenance.

**Network Effects**: As more projects join the system, the value of cross-project attribution and funding coordination increases, creating positive feedback loops that encourage adoption.

**Ecosystem Development**: Successful projects that benefit from the system have incentives to contribute resources back to system development and maintenance.

**Modular Upgradeability**: System components can be upgraded independently to respond to changing needs and technological developments while preserving existing value and relationships.

The funding mechanics create a self-reinforcing ecosystem where successful impact generation attracts funding, which enables more impact generation, while providing fair compensation to all participants in the value creation process. This addresses the core challenge of public goods funding: aligning individual incentives with collective outcomes while maintaining the scalability and transparency necessary for large-scale coordination.