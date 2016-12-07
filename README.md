12/5/2016 F2F NY

 

Attendees:

- Ram Jagadeesan
- Binh Nguyen
- Tamas Blummer
- Stan Liberman
- Hart Montgomery
- Vipin 
- Makoto Takemiya
- Bobbie Cochrane
- Terry Heath
- Alexander Yakovlev
- About 10     others… please update

 

Agenda:

- GSL Deep dive lead by     Tamas continued
- Storage Layer Abstraction

 

Notes:

- GSL overview recap
- Active Contracts:     “Functional programming” UTXO-like model, a contract is replaced with     another, which embeds the evolving current state. Instead of separate     algorithm and state, contract embeds state (procedural vs functional).
- Transaction is to replace     a contract with another one
- GSL doesn’t specify how     contracts are evolved, left to SC/Work-flow layer to determine how     contracts are replaced, and what constitutes a valid replacement.
- State of ledger is set of     “active contracts”.
- Active-contact set is     sufficient. Trust assumption is trust of signing authorities. History can     still be maintained for audits, etc.
- DAH uses DAML for     expressing contracts/work-flows. 
- Notifications: Connection     between layers. GSL only deals with evidences (hashes/ID’s of contracts).     Cryptographic tokens that be used to notify concerned parties. What are     the cryptographic primitives. Compute token that they recognize that     no-one else recognizes. GSL, deploy public-keys, and use DH to generate     keys that only those parties recognize.Support TX for 1000’s of     participants - scanning 1000’s of tokens. (like bitcoin addresses - their     wallet are notified - bloom filters). Corporate action -> split     millions of holdings.
- NSD Question: What is the     proof that a party received the notification. May be needed for a contract     to be legally binding. Are we eliminating intermediaries? TB: Not really     eliminating intermediaries - they still play a role. More enabling     intermediaries with new audit capabilities - to audit     notifications.Eliminating reconciliation. When is a transaction final? Have     all the parties rx notifications?
- Notification decouples     validation at SC layer from GSL layer.
- End of 2017 production tp     ASX.
- Would like to see a     general GSL as part of HPL
- Research on scalable     notification
- Iroha: UTXO model is less     scalable, since you have more transactions than people (accounts). TB:     Contracts are not limiting.

 

11/9/2016 Teleconference

 

Hopefully enough people are recovered fromthe shock … Life must go on ...

 

Attendees:

- Ram Jagadeesan
- Tamas Blummer
- Jeremy Sevareid     (independent)
- Binh Nguyen
- Stan Liberman
- Vipin Bharathan
- Hart Montgomery

 

 

 

Agenda:

- Deep dive discussion on     Global Synchronization Log Paper lead by Tamas
- Arch-WG Doc
-  

 

Notes:

- TB:Privacy models 4) and     5) Segregated ledgers and Data/Execution commitments are well suited for     financial use-cases, due to typical presence of centralized parties /     market infrastructure.
- TB:Information     (trades/positions data) confidentiality is strong requirement. GSL meets     these requirements. 
- BN: Fabric 1.0 trying to     address this using multiple sub-ledgers to hold private data. App can     create sub-ledgers and controls which ledger to share evidence of the     private data.
- TB: Primary task of GSL -     identity complete set of contracts that entities are party-to. Cannot be     optional evidencing of contracts. Needs to be reliable distribution of     info -> cannot be any contract that is not evidenced, and that any     interested party will be notified.
- HM: correlation-attacks?     TB: Evidence of contract and notification. Evidence and notification     appear as random data (hard to correlate). Even patterns of trade frq can     be obfuscated.
- State of ledger - state     of active contracts.
- GSL - assured info     dissemination mechanism. Subscribers ->
- Tx - two parts 
- Ledgers integrity is     guaranteed -> invariance of GSL is separated and algorithms that check     this invariance. Set of actors audit invariance of ledger. Overlapping     responsibilities.
- Imagine auditor is     guaranteeing uniqueness (regulator), can be done without revealing     contract details. Keeps check on writer, to ensure that contract is     replaced “validly”
- Contract T->Bank (Bank     has obligation pay $100 to T, or T has $100 in Bank account), “payment     from T-R”, R->Bank. GSL evidences original and second contract, and     indicates second contract replaces first contract. Notification tokens for     T and R.
- UTXO model: Contract     consumes old contract (inputs) and produces new contracts (outputs).
- Differentiation from     journaling file-system with entitlements and notification? Not really     since FS is not segregated. GSL is only evidencing similar to inode     structure.
- GSL records a fingerprint     of active contract-set-IDs. New contract, replaces old contract,     notification. Contracts details are exchanged oob, bilaterally.     Contract-IDs. ID could be blinded-hash of contract details (content     addressable ID).
- Smart Contract layer that     deals with the payload, communication layer.
- Aim define GSL as a     useful “component” - assured notification mechanism - base utility which     provides ordering, and notification.
- Will publish API to GSL.     Look at working with Fabric and Corda.

 

10/26/2016 Teleconference

 

Attendees:

- Ram Jagadeesan
- Binh Nguyen
- Hart Montgomery
- Stan Liberman
- Vipin Bharathan
- Sri
- Alexander Yakovlev

 

 

Agenda:

- Arch Doc Review -     Edits/comments in Arch Doc

 

10/12/2016 Teleconference

 

Attendees:

- Ram Jagadeesan
- Binh Nguyen
- Jamie Osborne - SWIFT
- Vipin Bharathan
- Stan Liberman
- Murali Krishna
- Jan Noppen - SWIFT
- Hart Montgomery
- Mic Bowman

 

Agenda:

- Security, Identity
- Doc Review
-  

 

Notes

- JO: Business standards     support on HPL - As we move up the stack to financial business standards,     SWIFT has some assets that can be shared/leveraged to help ensure that     blockchain-based business transactions are compatible with the existing     rails that global finance runs on – New info paper that includes results     of a research project that SWIFT recently completed here:     https://www.swift.com/file/31746/download?token=tUL6iYmi

 

- BN: To update the     Consensus section with input and team to review in the next meeting
-  
- SL: Have an     implementation specific policy around rejected transactions
-  
- Requirements: Allow     multiple nodes that operate within an administrative domain.
- MB: This can be satisfied     with a general schema for identity and policy - policy decisions - predicates     on identities. DB - with organizational binding - can specify that. 
- Go with a generic schema     for now, allow domains to specify attributes such as organization, and sp
- JN: Certificate alias

 

 

 

 

 

Meeting Notes from Amsterdam HackfestWorking Session

 

Attendees:

- Ram Jagadeesan
- Binh Nguyen
- Stefan Teis
- Tamas Blummer
- Vipin Bharathan remotely
- Jonathan Levi
- Thiru Vijayan
- Jan Noppen

,

Agenda:

- Security Requirements     & Identity & Policy

 

Notes:

- - Swift: Ability to work      with existing Identity framework
  - One CA for each      production environment

- Bootstrap: binding     between identities/certs and node

- Fabric proposal - TLS     cert and enrollment-cert.

- Pros for having identity     registry on-chain

- - Native record on the BC      – and reduces dependency on external system
  - Time-synched to changes      on on-chain – changes are synchronized with the tx that are being      validated on chain

- Identity services:

- - Provides a mechanism for      registering “network entities” such as validators, endorsers during the      boot-strap process. The registry provides a binding between the network      entity and it’s credentials (public-key). There are advantages to having      this registry on-chain. White-list of members.
  - Today PBFT      implementation does not include changes to membership.
  - Boot-strap can be static      configuration of n-nodes, or 1-node at a time, with ability of      genesis-node to on-board new nodes.

- Revocation: Need to     support CRL’s. May need to post CRL’s on-chain.

- In the new concept of     channels - CRL’s need to be synchronized across channels. Can     simultaneously replicate CRL’s across channels work? TB: You destroy     global order, if you have ordering (consensus) on a per-channel basis.     Basic functioning of BC is time-ordering/stamping evidencing records -     channels without ordering destroys the basic value. BN: PBFT-like     consensus has N^2 complexity - by going to local ordering system scales     much better. Throughput is 100 tps with PBFT. Doesn’t scale. It’s     performance vs global-order.

- ST: trading requires global     ordering

- CLS - FX trading -     Post-trade needs to keep up with money flows in real-time. SLA’s 95% in 1     minute, 100% in 5 minutes for full processing an instruction, validating,     matching and notifying. Settlement is offline batch process.

- Iroha: If you change     membership, have to re-initialize the consensus algorithm

- In mainstream Enterprise     applications, if a node fails - it’s should come back. 

 

Record retention, immutability andeditability. Accenture - chameleon hashes - ability to edit the chain. Right tobe forgotten. The risk of backdoors is another disadvantage of editability. Theproblem of having to reverse erroneous transactions, is that you need theconsent and signature, of the counter-parties in order to post the reversingtransactions.

 

Notes:

\1. Zero Data Loss requirement - whoretains the data on rejected transactions?

- Correct duplicate     checking, unique matching - cross-reference two entities - that needs to     happen on business-logic on ledger data. 

 

`

 

9/14/2016 Teleconference

 

Attendees:

- Ram Jagadeesan
- Mic Bowman
- Stan Liberman
- Vipin Bharathan
- Tamas Blummer
- Hart Montgomery

 

Agenda:

- Security 
- Arch Doc

 

 

Notes:

Sawtooth - Network Object -Endpoint/participants - Typed - associated policy.

Open Network - anyone can register anend-point, no validation.

Explicit Private Network - White-list:Call to Database - ECDSA public key identifier for end-point -> registrationauthenticates registering node.

With SGX - a version of POET - support forattacks and improvements. Intel attestation-server - one-time, and create achunk that registers an enclave -> identity. Validity of enclave isverified.

 

Genesis: special case. Special validationprivileges. 

Policies about who can validate aparticular block. Genesis entity can validate only first-N (say 5) blocks. Incase of SGX -> probabilistic identification of bad entities, and black-listthem.

 

Revocation -> work in progress. Cannotremove identity. Even if keys are compromised can remove yourself. Who isgranted the right to revoke the ability of an object/end-point to validate(white-list/black-list).

(Sybil attack protection. Validator notallowed until they participate in a few txns not as validator.?) SGX providesEPID one-way map to a group - contextual to enclave -> Sybil preventionpiece. Block, hash, hash of identity to generate wait-time -> requiring thatyou wait for two -> can’t control the hash, by choosing a identity thatbenefits you (in terms of favorable wait time). Need to bind a signing key toEPID.

 

First block: Ledger parameters ->commit to initial policies 

Second Block: Transaction familyinitialization -> base set of asset types, that other can derive from.(Market place - generic token that can be given to every participant -> SCbasic set of assets -> special token becomes trigger for provisioning).Essential for establishing base-classes.

Third, 4th and 5th: Registration block-> Validation information - type specific. Open reg -> no validation.Permissioned ECDSA public key. SGX - proof of valid enclave.

Having dependency on external DB could benon-deterministic. External state (DB) may have changed. If you have finalitynot a problem. If using probabilistic (Nakamoto) then need. Identity - usingECDSA public keys.

 

 

Request for re-verification of someoneelse: protection against denial of service, once a week? Tie to successfultransactions

 

 

 

 

8/31/Teleconference

 

Attendees:

- Ram Jagadeesan
- Murali
- Hart 
- David
- Stan
- Alex
- Sri

 

Agenda:

- Security Functions     Continued
- Bootstrap
- Identity & Policy     Modules

 

Identity Requirements: Are webootstrapping identities from scratch on the blockchain, or is there arequirement for using an external/legacy identity service?

David’s original membership services modelallows user identity to be imported from an external authority.

 

Federated Identity: Example DTCC has anode - DTCC identity service is responsible for authentication, authorizationof DTCC entities, similarly each node/domain has it’s own service. 

 

System entities are known/public- will notbe anonymous. In the future do we need to consider pseudo-anonymous systementities?

We can rely on PKI backbone of the system- have a root-CA within the system - Can designate an entity to authorizeadditions.

 

“Selective Release”

 

8/17/2016

 

Attendees:

- Ram Jagadeesan
- Vipin Bharathan
- Stan Liberman
- Binh Nguyen
- Murali
- Mic Bowman
- David Kravitz

 

 

Agenda:

- Agenda Review
- Security Requirements
- Bootstrap process
- Identity Services
-  

 

 

Notes:

- Future agenda topics     Storage Abstraction - Binh and Vipin to have offline discussion
-                #        <EnrollmentID>: <system_role (1:client, 2:     peer, 4: validator, 8: auditor)> <EnrollmentPWD>     <Affiliation> <Affiliation_Role> <JSON_Metadata>
- Fabric membership     services config file     https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=blob;f=membersrvc/membersrvc.yaml;h=f4567bc9c5a66323e710a0d4bf55c296369bea44;hb=refs/heads/master
-  

 

Security Requirements:

- No single-point of     failure
- No single point of trust

 

Identity Services:

- Authenticate system     entities - identity and credentials
- Registration - Enrollment     - vetting
- Authorization and     entitlement (permissions)

Policy Services:

- Group policies for chain
- Identity, enrollment,     entitlement policies
- Policy management
- Interfaces to policy     enforcement points

 

Bootstrap Process:

- Fabric - 

- - 1) Static configuration      file - specified in config file. Identities and properties are specified      in the config. “Register” the id’s in the system. The Peer would use the      identity to enroll with Membership services. Peer gets Ecert (Enrollment      cert) from MS, and uses the cert for authentication with other entities.      Peers can then obtain and use Tcerts (Transaction certs) for tx for      privacy.

  - - Config structs:


- - - - Id
      - System Role (1, …,8)
      - OTP
      -  

  - 2) API - Admin      application - registration API and enrollment API. An authorized entity      would use the the API to register new entities.
  - Registrar entity needs      to be configured. After the registrar is up, it can support dynamic      enrollment.
  -  

 

- Sawtooth: 

- - Use Ledger for managing      services. Specific transaction family for registration and policies. 
  - Rights and privileges      based on validation information
  - Genesis validator -      retired after bootstrap - accepts persistent validator.
  - Follow-on registration -      validation using PoET.
  - Special privileges      constrained in time; does not extend beyond bootstrap.

 

- Common: Registration,     enrollment, entitlement
- Pros and Cons of     distributed launch vs  simpler single trusted bootstrap service?

 

 

 

- Mic’s proposal: The     ledger itself could serve as the registry
- AIs: Mic and Binh to post     documentation. Mic is on vacation for two weeks starting next. May be late     for text. Team to review and continue discussion over e-mail and next     meeting.
-  

 

8/11/16 Documentation Working Session - Dowe need notes, or shall we work on the doc?

 

Agenda: Work on Arch Doc: [https://docs.google.com/document/d/1bdr4MdnpUvv_3jN5DYSNp1ctjKGPH7K_yiMSQYcwBBo/edit#](https://docs.google.com/document/d/1bdr4MdnpUvv_3jN5DYSNp1ctjKGPH7K_yiMSQYcwBBo/edit)

 

Attendees:

- Ram Jagadeesan
- Mic Bowman
- Stan Liberman
- Hart Montgomery
- Binh Nguyen

 

Notes - captured on working doc. 

 

Binh and Mic volunteered to flesh out theConsensus section, and Ram, Hart and Stan volunteered to flesh out the SmartContract section.

 

 

 

 

 

8/3/16 Teleconference

 

Attendees:

- Ram Jagadeesan
- Mic Bowman
- Hart Montgomery
- Stanislav Liberman
- Alexander Yakovlev
- Craig Rowe
- Vipin Bharathan
- David Kravitz
- Jonathan Levi

 

 

 

 

Agenda:

       Documentation

       Security& Privacy

 

Documentation Plan:

       Startwith Google Doc for Architecture, and see at what point it’s mature enough forformal doc using Latex

       Starta Google Doc folder for multiple docs

Stan: Suggest a high-level architecturemodule definition for the documentation 

Ken: Prioritize top-10 securityrequirement 

Mic: Expediency of implementation vsarchitectural alignment

 

 

 

AI:

       Ramwill start Arch Google Doc, and an Arch-WG-doc folder

 

 

F2F 7/27/16 General Session

 

Attendees:

- Ram Jagadeesan
- Mic Bowman
- Binh Nguyen
- Tamas Blummer
- Hart Montgomery
- Stanislav Liberman
- David Kravitz
- Jonathan Levi
- Christopher Allen
- Chris Price

 

Regarding the information that persists…

We need to keep as part of the permanentrecord the endorser request and response, and the policy that was used toapprove based on the results. This information may be useful later for audit orendorser policy decisions.

 

Does the transactor get to choose theendorser set or does a more general policy (e.g. from the chaincode) determinethe endorser set? If the transactor chooses the endorser set then there must bea mechanism for dynamically creating the “privacy” capabilities. Per Hart: bothunlinkability and selection of endorsers might be requirements. Architecturemust accommodate both requirements.

 

DK - Audit is done through key-delegation.Doesn’t need to be explicit in “endorsement policy”

 

Security & Privacy Requirements:

 

Genesis - Bootstrap Requirements and TrustModel:

       Needinput on this.

 

Simplest starting-point: Is single entity- single trusted party (CCP) who is sole admin and validator, and writestransactions to the BC. Genesis ID - Root of trust - Bootstrap identity andpolicy system. Can delegate authority.

One common approach is to recordpublic-key in the genesis-block of the BC, and subsequent (validator/endorser)identity registrations/delegations could also be recorded in the BC.

 

Requirement for trusted setup - withouttrusting a single part? E.g. Bootstrapping a consortium BC.

 

Should the ledger be used to record.

 

Scope: Core Identity/Authorization forvalidators/endorsers and BC system entities. We need to define enrollment ofsystem entities. 

Could we leave theidentity/authorization/policies for the transactors/participants to thesmart-contract layer?

 

Req: Dynamic registration of new systementities

Req: Policy for system entities adds/drops

Req: Audit policy and explicit systemaudit roles/nodes registration that is visible? Auditor - visibility intotransaction details (whether or not transactors wants that).

R

 

 

7/26/16 F2F Meeting Documentation Session - 1 PM PT

 

Agenda: Outline of the documentation forconsensus layer, smart-contract layer and interface specifications

 

Attendees:

- Ram Jagadeesan
- Hart Montgomery
- Stanislav Liberman
- Mic Bowman
- Binh Nguyen
- Chris Price
- Nikilesh Subramoniapillai     Ajeetha

 

Recap of Consensus& Business Logic:****

Smart-contract layer: Validates and executes transactions, andcomputes state-deltas, according to validation policy, and maintains theglobal-state.

 

Consensus layer: Confirms the correctness of alltransactions in a proposed block, according to validation and consensuspolicies. Agreement is on order and correctness and hence on results ofexecution (implies agreement on global state). Interfaces and depends on smart-contractlayer to verify correctness of an ordered set of transactions in a block.

 

Process:

1.    Select initial state

2.    Viability Test - set of rules forcorrectness given current state (prior)

3.    Compute State Delta and set of events

4.    Order

5.    Verify Independence of State Updates(Viability/Correctness of the Block?)

6.    Commit transactions and fire events

 

 

- We assume that     transactions are atomiFunctional Description of Smart Contract Layer


- Determines the validity     of a transaction given a starting state. It must reject the transactions     found to be invalid.


- Part of the validity test     includes the permission test (e.g. authorized by asset owner)
- The input state includes     the data state for the smart contract (transaction family) and information     about the state of the chain (such as block number), 
- For valid transaction,     computes the delta on the state as a result of executing the transaction.     May generate a list of events that will fire when/if the transaction is     committed.


- c. If we have dependent     actions that must be committed together, assume they are captured in a     single smart contract.
- A node participates in     validating a transaction only if the node has permission and access to     perform the validation as specified in an “endorsement” policy. The     endorsement policy specifies the set of nodes that need to validate a     transaction.
- Endorsement policy     defines correctness

 

- From Smart Contract Layer     to Consensus

- - Accept/RejectInterfaces      of Smart Contract Layer


- Request to Smart Contract     Layer

- - Transaction
  - Transaction dependencies
  - State


- - Read and Write of State


- -  
  - State delta
  - Transaction
  - Transaction dependencies      (might be richer than input)

 

If (committed) State was the only context for transactionvalidation, then a chain of transaction could not be processed at a faster thanone-by-one at block creation rate. 

Read and Write State will be captured by interceptingrequests to State. Similar to transaction dependencies they formulate theassumptions made during validation. Consensus will be able to detect andexclude transactions that were valid under contradicting assumptions. 

 

Functional Description of Consensus Layer

- Confirms the correctness     of all transactions in a proposed block, according to endorsement and     consensus policies. 
- Agreement is on order and     correctness and hence on results of execution (implies agreement on global     state). 
- Interfaces and depends on     smart-contract layer to verify correctness of an ordered set of     transactions in a block.
- Provides proofs/hash of     global-state to allow late joining (or out of sync)  nodes to     catch-up.
- May support interfacing     to eventing function to support events associated with committed transactions     and block-level events
- Placeholder for Identity     of validators/consenters and associated policy

 

 

Interfaces to Consensus Layer

 

Detailed Process Flow Description

Message Sequence Chart

 

Next Steps/ToDos:

- Need to talk about state     sharing to endorsers and implications of endorsement policy.

 

 

7/20/16 Teleconfence

 

Attendees:

- Ram Jagadeesan
- Mic Bowman
- Hart Montgomery
- Chris Price
- Stanislav Liberman
- Vipin Bharathan

 

 

 

 

 

 

Agenda

- Documentation plan 

- Security & Privacy -     Functional requirements

- Security Review

- F2F Agenda

- Prioritizing other Agenda     topics:

- - Working with W3C, IETF      other standards bodies
  - Interworking between      ledgers/chains
  - UTXO vs account-state      models

 

Agenda for F2F:

- Documentation - Skeleton     - and outline - 3 hours
- Security & Privacy -     3 hours
- Storage layer - DB
- Prioritizing other topics

 

 

Documentation Plan:

Hart: Important to capture detaileddocumentation especially for security review pov.

Mic: Have a working session on documentingarch-wg conclusions

 

 

 

 

 

 

 

7/6/16 Teleconference

 

Attendees:

- Ram Jagadeesan
- Christopher Allen
- Hart Montgomery
- Marko Vukolic     (mvu@zurich.ibm.com)
- Tamas Blummer
- Stanislav Liberman

Recap of Consensus& Business Logic:****

Smart-contract layer: Validates and executes transactions, andcomputes state-deltas, according to validation policy, and maintains theglobal-state.

 

Consensus layer: Confirms the correctness of alltransactions in a proposed block, according to validation and consensus policies.Agreement is on order and correctness and hence on results of execution(implies agreement on global state). Interfaces and depends on smart-contractlayer to verify correctness of an ordered set of transactions in a block.

 

Process:

 

7.      Viability Test - set of rules forcorrectness given current state (prior)

8.      Compute State Delta

9.      Order

10.   Verify Independence of State Updates(Viability/Correctness of the Block?)

11.       Commit

Other Agenda Items****

- Report out on request to     do Consensus APIs from W3C Blockchain Workshop

- - [https://twitter.com/ChristopherA/status/748604981259943940](https://twitter.com/ChristopherA/status/748604981259943940)

  - Ethan Buchman <[ethan@tendermint.com](mailto:ethan@tendermint.com)>      or <[ethan@coinculture.info](mailto:ethan@coinculture.info)>

  - - [http://tendermint.com/blog/tendermint-socket-protocol/](http://tendermint.com/blog/tendermint-socket-protocol/)
    - [https://github.com/tendermint/tmsp](https://github.com/tendermint/tmsp)

- How to move forward on     academic review and security review requirements for cryptography,     architecture & APIs, and identity/privacy/confidentiality?

- - How about security      review requirements?

  - - Functional requirements       (a core architecture WG task)
    - Should we providing       guidance on our approaches for early academic and security reviews       before code audit. Security review framework?
    - Review and Audit (is       this an architecture WG task?)
    - What are the stages of security       review / levels in the release process?


- - - - Bitcoin is a running        network, Hyperledger is not

  - Fabric team desires to      submit papers to academic

  - - Can we get details on       what papers? Where being submitted? Can we do early review.

  - What are the      requirements for a public hyperledger blockchain instance? Brainstorm      around this and what it entails?

  - - Functional requirements       and format details

  -  

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

7/1/16 Teleconference

 

 

Attendees:

- Ram Jagadeesan
- Kostas Christidis
- Stanislav Liberman
- Hart Montgomery

 

 

Agenda:

- Consensus and     Smart-Contract layer discussion continued

 

 

 

 

Smart-contract layer: Validates andexecutes transactions, and computes state-deltas, according to validation policy,and maintains the global-state.

Consensus layer: Confirms the correctnessof all transactions in a proposed block, according to validation and consensuspolicies. Agreement is on order and correctness and hence on results ofexecution (implies agreement on global state). Interfaces and depends onsmart-contract layer to verify correctness of an ordered set of transactions ina block.

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

6/22/16 Teleconference

 

Attendees:

- Ram Jagadeesan
- Mic Bowman (intel)
- Craig Rowe
- Arnaud Le Hors (IBM)Binh     Nguyen
-  
- Vipin Bharathan
- Chris Price
- Hart Montgomery
- Sri Krishnamacharya

 

 

 

 

Viability Test - set of rules forcorrectness given current state (prior)

Compute State Delta

Order

Verify Independence of State Updates(Viability/Correctness of the Block?)

Commit

 

 

Immediate finality vs Probabilisticfinality with roll-backs/journalling

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

6/17 Teleconference

 

Attendees:

- Ram Jagadeesan, Cisco
- Christian Cachin, IBM
- Chris Price
- Alexander Yakovlev
- Mic Bowman
- Vipin Bharathan
- Hart Montgomery
- Tamas Blummer
- Christopher Allen

 

 

 

 

 

Goal:

- Pluggable consensus     module/layer - allow various consensus algorithms to be supported using a     “unified interface or framework”
- Requirements 1) Agree on     order 2) Agree on correctness 3) Support confidentiality
- Try to minimize the     dependencies between consensus and business-logic/smart-contract layer and     make the dependencies explicit
- Policy driven placement     of sub-functions - components.

 

 

Chris Allen - Opportunity for new attacksurfaces by separating “correctness/endorsement” from consensus?

HM: Decoupling is a security bonus ratherthan a minus.

 

Contract -> Meta-data : Deterministic,reversible, side-effects?

Bindings: e.g. business-logic computationis non-reversible (won’t work with probabilistic consensus approaches whichrequire rollbacks) 

 

MIC: Here’s one definition:

Formal requirements fora consensus protocol may include:

·        *Agreement*: All correct processesmust agree on the same value.

·        *Weak validity*: If all correctprocesses receive the same input value, then they must all output that value.

·        *Strong validity*: For each correctprocess, its output must be the input of some correct process.

·        *Termination*: All processes musteventually decide on an output value

Dependencies -correctness - smart-logic/endorsement/validation - depends on state:

Possible means to determine correctness:

- By formal specification     of acceptable states (e.g. database consistency constraints)
- By functional computation     (i.e. the contract itself determines correctness)
- By external observation     (e.g. through the aggregate vote of a set of endorsers)

 

 

 

Showing how Bitcoin’s Nakamoto consensusis equivalent to (distributed-computing) consensus:

- Juan A. Garay, Aggelos
  ​     Kiayias, Nikos Leonardos:
  ​     The Bitcoin Backbone Protocol: Analysis and Applications. EUROCRYPT (2)
  ​     2015: 281-310 
  ​     http://eprint.iacr.org/2014/765
- Andrew Miller’s paper: [https://socrates1024.s3.amazonaws.com/consensus.pdf](https://socrates1024.s3.amazonaws.com/consensus.pdf)
- Analysis of the
  ​     Blockchain Protocol in Asynchronous Networks
  ​     Rafael Pass and Lior Seeman and abhi shelat
  ​     https://eprint.iacr.org/2016/454
-  

 

CA: DAO bugs and R3 composability -business logic with deterministic proofs:[https://github.com/WebOfTrustInfo/ID2020DesignWorkshop/blob/master/topics-and-advance-readings/DexPredicatesForSmarterSigs.md](https://github.com/WebOfTrustInfo/ID2020DesignWorkshop/blob/master/topics-and-advance-readings/DexPredicatesForSmarterSigs.md) 

 

For next week's agenda: some questionsfrom identity WG on security and cryptographic review, and how that connects tostatements re: release quality (separate from exit criteria). For instance,formal review of the ECDSA derivations used in Membership Services that havenever been used before. Is this the role of Architecture or a separate group?So far requirements WG has not been at that level.

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

6/8 Teleconference

 

Attendees:

- Ram Jagadeesan
- Craig Rowe
- Jean Safar
- Stan Liberman
- Greg Haskins
- Tamas Blummer
- Arnaud  Le Hors
- Mic Bowman
- Chris Price
- Hart Montgomery
- Binh Nguyen
- Marko Vukolic
- Vipin Bharathan  

 

 

 

 

 

Agenda:

- IBM proposal for new     consensus protocol
- Generalization of our     basic approach to support “validating set”
- Confidentiality     Requirements
- Trust Model - Transitive     trust

 

 

IBM Proposal Discussion:

“Consensus service” is a common/utilityservice, that “channels” (private sub-groups - or virtual network) can use. Endorsement policy could specify only two endorsers - for bilateralcontract/tx.

Two levels of confidentiality 1)tx-payloadonly goes to endorsers, other peers do not see the payload - only hash oftx-payload is included in blob to other peers.

Partitioning: particular class of state -state is immutable - create new objects, 2) Semantic level of partitions -sequential, 3)Make dependencies explicit - longer term cryptographic

 

Granularity of data-model - single object.Leader based.

 

Committing peer - committing- tx upate canbe propagated in cipher-text.

Confidentiality flavors - endorsers seeeverything in plain-text.

 

 

Generalization of basic approach:

Validating-set: Set of validating peernodes that have cleartext access and authorization to execute and validatetransactions

Validation-policy: Rules on whatconstitutes a valid-tx (similar to endorsement policy)

 

Smart Contract Function:

Receives tx from communication layer(unicast from client-node)

If this peer is part of validating-set,executes the validation/business-logic and stores result in scratch-space, iftx is valid. Computes state-update, and optionally includes it in tx sent tonetwork. (In this model, it seems we may not need version-dependencies). Tx isrejected/tossed if not-valid.

Transmit tx to network (broadcast topeers) via communication layer

Block-creator (leader) role: Createsproposed block – ordered list of “valid" tx. Uses state-update informationto eliminate potentially conflicting txs (e.g. Double spend txs would beupdating using same key.). Sends block to Consensus layer.

Block-validator role: Executes each tx inreceived block that it is authorized to (I.e. This peer belongs to validatingset of tx) and appends its “validation(endorsement)” to each valid tx. Checksstate-update info for inconsistencies for other txs, that it can not execute.Sends validation responses to Consensus layer.

Block-committer: Commits all state-updateson completion of consensus

Consensus Function:

Block-creator (leader) role: Receivesproposed block from SC function and starts consensus protocol to peer-nodes(broadcast) via communication layer. Ensures validation-policy is enforced.

Block-validator role: Receivesproposed-block from peer via communication layer, and send to SC function forblock-validation – Uses response in Consensus process and confirms thatvalidation-policy is enforced (Additional round of communication may be neededfor confirmation.)

Output of Consensus is agreement onordered set of valid tx. If Block contains hash of global-state, also verifiesglobal state is consistent. If Consensus is not reached tx returned to“mempool”?

 

 

 

5/25 Teleconference

 

Attendees

- Christopher Allen
- Hart Montgomery
- Mic Bowman
- Ram Jagadeesan
- Greg Haskins
- Tamas Blummer
- Stanislav Liberman
- Marko Vukolic
- Vipin Bharathan
- Vivian Shen

 

Agenda:

1) Recap of working session discussions

2) Requirement for confidentialtransaction

3) Continue discussion on Consensus andSmart-Contract modules functional decomposition and interface definition.

 

 

 

Notes from offline working sessions:

Smart-Contract/Validation and Consensusfunctions description modeled after bitcoin blockchain and Sawtooth lake:

 

\1. Receives transaction (tx) fromcommunication layer (unicast from client-node)

\2. Validates tx – executes thevalidation/business-logic and stores result in scratch space, if tx is valid.If invalid tx is tossed

\3. Transmits tx to network (broadcast topeers) via communication layer

\4. Block-creator: creates blocks andvalidates – by executing tx in-order (check for inconsistencies/double-spendswithin block, and tosses any invalid txs). Block could contain the hash ofglobal-state.

\5. Sends validated block to Consensusmodule

\6. Block-Validator: Receives transactionfrom Consensus module and executes tx -in–order and validates block, sendsresponse to Consensus.

Consensus module:

\1. Block-creator: Receives validated blockfrom SC function and starts consensus protocol to peer-nodes (broadcast) viacommunication layer.

\2. Block-validator: Receivesproposed-block from peer via communication layer, and send to SC function forblock-validation – Uses response in Consensus process (e.g. Votes Yes if blockis valid)

\3. Output of Consensus is agreement onordered set of valid tx. If Block contains hash of global-state, also verifiesglobal state is consistent. If Consensus is not reached tx returned to“mempool”?

What are failure modes and how do werecover?

 

IBM fabric proposal to handle confidentialtransactions: 2-phase approach with endorsing peers  who endorse(pre-validate) tx that are received from submitting peer. Endorsers have clear-textaccess and can execute and validate tx. A submitting peer which receivessufficient number of endorsements to meet the endorsement policy will includetx in 2nd phase block-generation at consensus services. The consensus servicedoes not have clear-text access to tx data, and hence cannot validate tx – itonly creates an ordered list of tx for inclusion in a block. (Need a secondpass validation to eliminate double-spend tx’s within a proposed block). Thisproposal will be described shortly in fabric docs in the wiki.

 

![https://lh4.googleusercontent.com/Ypv19PNvFVm2g11C2FVQe-tZ-lCb8gyU-KItDLZFuUOjPe5s8k4_qkHD_lliOy6IagKmGjLDWqaUMLMozsuQDld_utKvhxA5empzc8AtgG5do3i7oLzZRyDIjwzIe6Ms-WCTnIx9](file:///C:/Users/IBM_AD~1/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

 

 

 

 

 

Confidentiality Requirement: Only asmaller subset of nodes should have access in clear-text to data that is neededto validate a tx. (forward secrecy/confidentiality)

 

Mic: 2-phase may have a performanceimpact, when we try to meet confidentiality requirements

Marko: Parallelization could improveperformance.

 

What happens when chain-code’s interactwith other chain-codes with different endorsement policies? Generallyproblems/complexity with crossing confidentiality domains.

 

 

 

(BTW, a link to Blockstream ElementsConfidential Transactions zero-knowledge method. It does have a computationalcost such that it can’t be use for all use cases. [https://elementsproject.org/elements/confidential-transactions/](https://elementsproject.org/elements/confidential-transactions/) )

 

CA: I am bothered a bit to know what usecases need what levels of confidentiality, and what the transaction speedrequirements are needed for those cases.

 

The idea of separatingcorrectness-testing/validation from consensus functions is desirable, whereeach node is not doing everything.

 

Should it be data-centric or code-centric?

 

Any requirement for confidentiality forcode?

 

Can endorsement be done on an enclave?

 

F2F Meeting 5/6/16

 

Attendees

- Christopher Allen,     Principal Architect Blockstream <ChristopherA@Blockstream.com>
- Ram Jagadeesan, Cisco
- Jan Willem Barnhoorn, ABN     AMRO
- Tim Blankers, ABN AMRO
- Vipin Bharathan, BNP     Paribas Americas
- Stanislav Liberman, CME     Group
- Takahiro Inaba, NTT
- Keith Smith, IBM
- Mark Moir, Oracle Labs
- Binh Nguyen, IBM
- Vani Komera, DTCC
- Murali, DTCC
- Mike Haley, AlphaPoint
- Mic Bowman, Intel
- Cian Montgomery, Intel
- James Mitchell, Intel
- Shawn Amundson, Intel
- Simon Schubert, IBM     Zurich (call-in)
- Tamas Blummer, Digital     Asset
- Renat Khasanshyn, Altoros
- Jatinder Bali, Citigroup
- Hart Montgomery, FLA     (call-in)
- Sumabala Nair, IBM

 

 

Agenda

- Intros
- Consensus layer/module -     interface and functional spec

 

 

Consensus - Agreement on log and agreementon state. Abstract representation for state (represent storage) - interface foradding pending tx, and committing a block. Claiming tx-block. Build_block,advance block through change, handle disputes. Init, and clean-up.

Quorum voting - messages that driveinternal state-machine, manages timing events (ripple-like - periodic kickoffof vote). 

POET dynamic adaptation - targetingparticular commit rate - sampling.

Quorum - 60%.

Timing-events - block-building. Tolerancefor commit times.

 

Incentives -  provided by transactionfamily.

 

 

 

Consensus Layer Interfaces:

       CommunicationLayer       (transport)

·        Register handler for message-type

       BusinessLogic / Smart Contract Layer

       StorageLayer

       

 

TX validation logic - needs internalinterface (double spend - need read-only interface, wrtite additional state).Similar to stored procedures in DB.

External - higher level application -work-flow.

 

1. Tx pre-filtering - is     this a sensible tx, viable candidate
2. Candidate block with tx
3. Test that block against     current state
4. Consensus process - vote     on (tx on block are sane, new consistent state)

 

 

h

Different Consensus & BFTs

 

Categories:

- Explicit Voting - Paxos     and BFT family - Permissioned voters. Needs to have identity functions.
- Implicit Voting - PoW,     PoS, PoET - permissionless voters - most don’t have finality due to     probability of forks. Needs to (temporarily) accommodate multiple parallel     blockchain heads due to probabilistic process.Need to support revisions     (handle forks).
-  


- Paxos Consensus family of     BFTs

- - (see list below)

- Nakamoto Consensus family

- - PoW: Proof of Work

  - - ASIC resistant PoW

  - PoET: Proof of Elapsed      Time

  - PoS: Proof of Stake

  - Casper: Combined PoW w/      PoS

  - Future forms: Proof of      Storage, Proof of Bandwidth, Proof of Transit

  - - Theoretical perfect       form may be Shannon’s Flow of Information

 

Last time there was a discussion aboutmany BFTs, each with different advantages and limitations. A partial list:

 

- The "Sieve"
  ​     protocol used in OBC  is described in here
  ​     [http://arxiv.org/abs/1603.07351](http://arxiv.org/abs/1603.07351)
- Overview Cachin/IBM PBFT:
  ​     [https://www.zurich.ibm.com/~cca/papers/pax.pdf](https://www.zurich.ibm.com/~cca/papers/pax.pdf)
- Microsoft PBFT: [http://research.microsoft.com/en-us/um/people/mcastro/publications/p398-castro-bft-tocs.pdf](http://research.microsoft.com/en-us/um/people/mcastro/publications/p398-castro-bft-tocs.pdf)
- Redundant BFT:
  ​     [http://pakupaku.me/plaublin/rbft/report.pdf](http://pakupaku.me/plaublin/rbft/report.pdf)
- Stellar Consensus:
  ​     [https://www.stellar.org/papers/stellar-consensus-protocol.pdf](https://www.stellar.org/papers/stellar-consensus-protocol.pdf)
- Tendermint Consensus:
  ​     [http://tendermint.com/docs/tendermint.pdf](http://tendermint.com/docs/tendermint.pdf)
- To an important point of
  ​     last meeting, here is an academic paper that simulated a large number of
  ​     BFTs, and reports "one-size-fits-all protocols may be hard if not
  ​     impossible to design in practice.”
  ​     [https://www.mpi-sws.org/~druschel/publications/BFTSim-nsdi08.pdf](https://www.mpi-sws.org/~druschel/publications/BFTSim-nsdi08.pdf)
- there are many more, and
  ​     consensus protocols for blockchain are an active topic of research. many
  ​     researchers in this domain at the 1-day workshop in July in Chicago 
  ​     [http://www.zurich.ibm.com/dccl/](http://www.zurich.ibm.com/dccl/)
- RAFT
  ​     [https://raft.github.io/](https://raft.github.io/)

 

Another way to think about these is aroundconsistency, liveness characteristics:

- Voting: Explicit Vote     Counting

- - Network has      permissioning and identity, achieves finality quickly, lower scalability

- Lottery: Implicit Vote     Counting

- - By inference require      revising, consensus converges over time but isn’t final 

 

What types of faults:

- Voting BFTs 

- - Perfect BFT - Failure      Tolerant

·        RAFT/Stellar - Failure Stop

 

- Lottery: Nakamoto -     Forking until convergence

 

Storage differences

- Lottery/Nakamoto requires     journaling, which introduces performance limitations
- Voting/BFT does not     require journaling, but journally is ok if performance 

 

Two APIs that support both Voting &Lottery forms:

 

- Intel’s API:
  ​     [https://slack-files.com/files-pri-safe/T0J024XGA-F16NA0JQ4/sawtooth_lake_ledger_apis.pdf?c=1462544535-4f0b271ce548ce2a59ce798c54c0bd9ef30ef87b](https://slack-files.com/files-pri-safe/T0J024XGA-F16NA0JQ4/sawtooth_lake_ledger_apis.pdf?c=1462544535-4f0b271ce548ce2a59ce798c54c0bd9ef30ef87b)

 

- TMSP TenderMint Socket
  ​     Protocol - Protocol between consensus & business logic
  ​     [http://tendermint.com/blog/tendermint-socket-protocol/](http://tendermint.com/blog/tendermint-socket-protocol/)

- -  Echo
  -  Flush
  -  Info
  -  SetOption
  -  Exception
  -  AppendTx
  -  CheckTx
  -  Commit
  -  Query
  -  InitChain
  -  BeginBlock
  -  EndBlock

 

Terminology

- Transactor
- Validator
- Confirmer

 

Tendermint          PBFT                   Intel       Ethereum

proposer              primary

validator       replica

propose step              pre-prepare phase

prevote step        prepare phase

precommit step   commit phase

round change             view change

 

 

Unresolved Issues

- Nondeterministic     transactions issues

- - Ordering consensus vs      Result consensus / Pre-validation vs Post-validations / optimistic      execution before validation

-  

 

Other Links:

 

Other topics:

- Smart Contract - Run-time
- Communication Protocol -     common message format for P2P interactions in Hyperledger
- API to connect     business-workflows with hyperledger

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

4/27/16

Agenda

- Intros
- Layering discussion
- Architecture WG plan 
- Prioritize topics. Next     meeting agenda
- F2F next week

 

 

Attendees

1. Ram Jagadeesan -     Distinguished Engineer, Cisco
2. Christopher Allen -     Blockstream - Principal Architect 
3. Chris Price - Northern     Trust
4. Hart Montgomery - Fujitsu     Labs - Cryptographic
5. Mic Bowman - DL Research     group Intel Labs
6. Stan Liberman - CME group     Tech Labs 
7. Vipin Bharathan - BNP 
8. Diego Masini - IBM, Almaden     Research team
9. Alexander Yakovlev -     National Settlement Depository - nsd.ru

 

 

 

 

 

Notes

 

Layers 

Christopher Allen: There are manydifferent consensus approaches, example with BFT alone - Stellar, IBM’s Paxos,Redundant BFT, Tendermint, etc. How can we be flexible given each has differentprofiles. One implement, Tendermint - shared TMSP (TenderMint Socket Protocol)as a protocol layer supporting multiple consensus at meetup. Intel has SawtoothLake - it implements of two radically different consensus mechanism -quasi-permissionless POET (aka it simulates nakamoto POW without POW) , andmore traditional Stellar-style BFT protocol. We need to make sure that we arenot locked into any particular consensus mechanism, or have a strong tie-inbetween business-logic and consensus.

 

Ram: Agree with the goals of having atruly modular and pluggable consensus module. It doesn’t seem the currentfabric implementation based on OBC actually achieves separation betweenconsensus and smart-contract/business-logic.

 

Vipin: Devils advocate - why do we needmultiple? Two classes PoW/Nakamoto-consensus and PBFT-like protocols.

 

Mic: Nakamoto lacks finality. Advantage ishigh probability order O(N) complexity. PBFT-like - multiple rounds,scalability is an issue - perhaps to hundreds of validators at best.

 

Christopher: Even PBFT-like family widevariations. 10 nodes vs 20 nodes, vs 50 nodes. Don’t know if one solution meetsfinality, correctness, liveness. Also different implementations have differentsecurity properties based on different threat models.

 

Two large families -> Pros and Cons forthe two families, as well as each protocol/algorithm.

 

CA: There exists a huge diversity ofrequirements. For instance identity shared between 53 countries in a federationcan’t be served by traditional Paxos BFT. Latency requirements for that werenot that stringent so can be done with other BFTs. Blockstream has Liquid - itdoes simple round-robin but only very small federations.

 

VB:Avoid the rabbit-hole of dealing withevery option.

 

RJ: Need to define a clean API to theconsensus function to allow experimentation and customization to meet differentrequirements. Our goal should be to specify clean API and functional definitionof the consensus function - what does it do, and how do other layers/functionsinterface with it. At some point in the future a small set of “standard” consensusprotocols may emerge. 

 

HM: Agree on flexible. Don’t need tochoose specific protocols.

 

Mic: Define state machine at each level.Msg that drive state changes. Events drive state changes internally. (Will sendout set of slides).

 

RJ: Need to start fleshing out API andfunctional spec of consensus. Need proposals from folks on API, Consensusfunctional definitions. Pros and Cons.

 

CA: Can also start playing with code -create a stubs to test, and try multiple consensus modules underneath.

 

Need to separate business-logic andconsensus. Library-ize transaction logic.Keep semantics outside consensus.

 

Mic posted slide deck - pls review.

 

Next steps: Tee up API and functionaldefinition of consensus function. Either at F2F or next meeting/call.

 

Arch WG plan:

- Prioritize and go through     high level issues while we wait for use-cases and requirements to firm up.
- Discuss architecture     approaches/options and pros and cons vs requirements.
- Holy grail would be one     unified flexible and extensible architecture - alternate could be     high-level framework which accommodates different approaches. 
- Define functional     decomposition into layers/modules - what they do and how they interface     with other functions. 

 

Topic for next meeting - ConsensusFunction and API continued. Pls review the deck posted by Mic on slack.

 

Looks like a few members of the team willbe at the F2F. Tentatively schedule Friday AM for a F2F with dial-in for remoteparticipants.

 

List of topics from kickoff meeting:

-  Layers, in     particular between Consensus and Business Logic

- - paxos, pbft, poet       / transaction rules, chain code, smart contract

- UTXO and Application     State Model

- Terminology Clarification     / Shared Language

- -  transaction

- Vertical / Domains /     Segment Differences

- -  maybe from use      cases?

- Modularity

- -  protocols vs      interfaces vs api vs code base

- Interoperability between     ledgers/chains

- Yellow Paper on     Architecture

- - Complementary to White      Paper

- Lessons from other     Architectures

- Working with Requirements     and Use Cases WGs

 

 

Terminology

- Transactor
- Validator
- Confirmer

 

Tendermint          PBFT                   Intel

proposer              primary

validator       replica

propose step              pre-prepare phase

prevote step        prepare phase

precommit step   commit phase

round change             view change
