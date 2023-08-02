EIP-x, Xtreamly
Stateless Account abstraction that scales Ethereum.

## Motivation

Ethereum's state grows rapidly, burdening consensus nodes with 35 GB state and 100 GB with proofs, increasing every six months. 
The increasing state size hampers scalability, imposing storage and processing burdens on nodes. Participants pay one-time costs perpetually,
raising economic concerns. Additionally, ERC-4337 wallets incur elevated gas costs (~42000 gas for basic operations) due to multiple storage read/write costs, business logic overhead, and log payments not required in EOAs. A stateless based solution is essential to maintain  Ethereum's efficiency and long-term viability. Additionally, the light clients, which do not store the entire state but rely on simplified verification mechanisms, struggle to efficiently access and  validate the state data against the mainnet. The lack of a concise and constant-sized proof of the current state limits light clients' ability to interact with the blockchain seamlessly.
Therefore we Propose a stateless Account abstraction model which doesn't force any change in the current Ethereum core but can solve the above problems at the account level.


## Project description

The challenge at hand is to enable stateless verification of blocks in the blockchain system. The goal is to allow clients to verify the
correctness of individual blocks without needing a full state. Instead, clients can rely on compact witness files generated by state-holding nodes, which contain the portion of the state accessed by the block along with proofs of correctness. This stateless verification offers several benefits, including supporting sharding setups and reducing reliance on validators. The state provider entity is at the core of stateless AA, providing a succinct and constant-sized proof of the current state. Light clients can effortlessly verify this proof against the mainnet, improving scalability, and reducing resource requirements for light clients. Users and applications can efficiently interact with the blockchain, relying on the security and integrity of zk-proofs to verify the state. This approach enables more participants to engage with the network without needing the computational resources and storage capacity required for full nodes.


## Specification

To sustain scalability, we propose Stateless Account Abstraction with Two new entities: 
## 1- State provider: 
this entity consists of Ethereum light clients  providing the latest  state, peer to peer network and  ZK circuit. 
We introduce a decentralized peer-to-peer network with a state provider entity, collaborating to validate and generate ZK-SNARKs proofs 
for state information.A lightweight client verifies proofs and validates state data from the state provider.

A- ZK-SNARKs for State Proof:
To provide a trustless and efficient proof of state, we employ ZK-SNARKs, a cryptographic primitive that allows a prover to generate 
a succinct proof of the validity of a statement without revealing any sensitive information. By using ZK-SNARKs, the state provider can
generate proofs of state integrity that can be verified by any participant in the peer-to-peer network, ensuring the trustworthiness of 
the provided state.

B- Peer-to-Peer Network:
The proposed solution requires a decentralized peer-to-peer network to distribute the state provider functionality. Peers in the network 
collaborate to validate and generate ZK-SNARKs proofs for the requested state information. This distributed approach ensures fault tolerance,and resilience, and enhances the scalability of the state provider.

C-Proof Generation and Validation:
When a stateless transaction enters the alternative mempool, it includes a reference to the required state information. The state provider 
peers collaborate to generate a ZK-SNARKs proof that verifies the validity and integrity of the specified state against the Mainnet. 
This proof is then shared with the requesting node, allowing it to verify the state without relying on direct interaction with the
Ethereum Mainnet.

## 2-hybrid witness sharing.
we implement  Hybrid Witness Sharing (HWS), a novel approach that separates witness information from transaction data, optimizing gas usage, improving efficiency, and enhancing overall network scalability. This advancement is particularly beneficial for complex smart contracts and  data-intensive applications, empowering Ethereum to handle a higher transaction volume without compromising security or incurring exorbitant costs.
A-Transaction Data Inclusion: Each transaction will continue to include the essential data, such as inputs, outputs, and parameters, required for seamless execution and state changes on the blockchain.

B-Witness Information Sharing: In contrast to the current approach, HWS advocates for the separation of witness information from the 
transaction data. Rather than including the full witness in each transaction, it will be shared among multiple transactions. 
This sharing mechanism can be implemented using Merkle trees, zk-SNARKs, or other cryptographic techniques, ensuring the validity 
and integrity of witness data while minimizing redundancy.

C-Efficiency and Scalability: HWS and SAA contribute to improving the efficiency and scalability of the blockchain network. 
HWS reduces gas consumption, leading to faster block processing times, while SAA reduces the storage requirements for individual nodes.
Together, they enable the network to handle a higher transaction volume and improve the overall responsiveness of the blockchain.

D-Smart Contract Complexity: The combination of HWS and SAA encourages the development of complex smart contracts and data-intensive 
applications. With reduced gas costs and storage requirements, developers are incentivized to create more sophisticated and
feature-rich smart contracts, enhancing the utility and diversity of the Ethereum ecosystem.

E-State Separation: While SAA focuses on separating the state from the execution, HWS complements this approach by separating 
witness information from transaction data. The witness information can be considered part of the state that is shared among transactions. 
By separating both the state and the witness, the blockchain network can achieve a higher level of optimization and maintain 
a more scalable architecture.

## Roadmap


Roadmap for MVP Development of Hybrid Witness Sharing and Stateless Account Abstraction Proposal:

Phase 1: Research and Planning

1. Conduct In-Depth Research: Perform a comprehensive study of existing stateless account abstraction models,
   hybrid witness sharing techniques, and their potential integration with Ethereum's current ERC-4337 architecture.
   Identify any modifications required to adapt the ERC-4337 flow for the proposed solution.

2. Define Use Cases: Identify and document specific use cases that will be showcased in the MVP to demonstrate
   the benefits of the proposal. Consider scenarios where witness sharing and stateless account abstraction can lead
   to improved efficiency, reduced gas consumption, and enhanced scalability.

3. MVP Scope and Features: Define the scope of the MVP, including the core features that will be implemented,
    such as state provider with zk-proof, witness sharing model, and the necessary modifications to the ERC-4337 architecture.

Phase 2: Development

1. Implement Witness Sharing Model: Develop the witness sharing model, leveraging cryptographic techniques like Merkle trees or zk-SNARKs.
   The model should efficiently share witness information among multiple transactions, optimizing gas consumption for transaction validation.

2. Stateless Account Provider with zk-Proof: Create a state provider that stores essential data required for transaction execution,
  adhering to the stateless account abstraction concept. Implement zero-knowledge proofs (zk-proofs) to ensure data integrity and security.

3. Modify ERC-4337 Architecture: Make minor modifications to the ERC-4337 architecture to accommodate the proposed hybrid witness
   sharing and stateless account abstraction. Ensure compatibility with existing smart contracts and functionalities while integrating the new components.

Phase 3: Integration and Testing

1. Integration with Bundler and Entry Point Smart Contract: Integrate the developed state provider and witness sharing model
   with the bundler and entry point smart contract of ERC-4337. Verify that all components work seamlessly together to
   facilitate transaction execution and witness sharing.

3. MVP Testing: Conduct extensive testing to ensure the MVP's functionality, security, and performance. Perform unit testing,
   integration testing, and simulate real-world scenarios to validate the proposal's benefits and use cases.

Phase 4: MVP Showcasing

1. Prepare Documentation: Create comprehensive documentation detailing the MVP's architecture, implementation, and use cases.
    Provide clear instructions for the Ethereum community to understand and interact with the MVP.

2. MVP Showcase: Organize a public showcase event or release the MVP to the Ethereum community for review and feedback.
Engage with developers, stakeholders, and the broader community to gather insights and suggestions for further improvements.

Phase 5: Follow-up Work and Future Extensions

1. Address Protocol Changes (if required): Based on the feedback and findings from the MVP, evaluate the need for any modifications
to the ERC-4337 flow to better support stateless account abstraction. Collaborate with the Ethereum community to propose and implement necessary changes.

2. Continuous Improvement: Continuously refine and optimize the MVP based on community feedback and new research findings.
 Explore potential enhancements, security updates, and additional features that can be incorporated to further improve the proposal's efficiency and scalability.

By following this roadmap, the development team can create a functional MVP showcasing the benefits of the hybrid witness sharing and stateless account abstraction proposal without the dependency on Verkle trees or protocol-level changes. The MVP can serve as a powerful demonstration of the proposed solution's potential and open up new possibilities for the Ethereum community.


## Possible challenges

Users need to ensure that the necessary data (e.g., account balance, contract code) is available and properly validated during transaction 
processing. This may require additional protocols or mechanisms to efficiently generate and validate these proofs.
Smart Contract Interactions: With stateless account abstraction, smart contract interactions may require additional considerations.
For instance, when a contract interacts with other contracts, it needs to obtain and validate the required state information 
during execution.

## Goal of the project

Success for the Hybrid Witness Sharing and Stateless Account Abstraction project would be achieved when the proposed solution is 
fully developed, implemented, and widely adopted within the Ethereum community. The end goal is to demonstrate a functional MVP 
that showcases the benefits of hybrid witness sharing and stateless account abstraction while providing tangible improvements to 
Ethereum's efficiency, scalability, and usability. All are accomplished without dependency to a statelessness roadmap or conduction 
of changes within the core. 


## Collaborators
TBA
### Fellows 
TBA

### Mentors

Guillaume ballet 
Matt Garnett
Yoav Weiss
Sina Mahmoodi 

## Resources
https://github.com/sogolmalek/EIP-x