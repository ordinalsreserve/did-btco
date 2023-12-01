# BTC Ordinals DID Method Specification (v0.1.0)

December 1st 2023

Authors:
- Brian Richter (Aviary Tech)

Discussions: https://github.com/ordinalsreserve/did-btco/discussions

Issues: https://github.com/ordinalsreserve/btco/issues


# 1. Introduction

The "BTC Ordinals DID Method" is a Decentralized Identifier (DID) method that combines the security of the BTC blockchain with ordinal theory to create a decentralized identity management system. Key features include:

* Utilizing the BTC blockchain for trust and consensus
* Incorporating ordinal theory for efficient DID management
* Supporting standard DID operations (creation, resolution, updating, deletion)
* Compliance with the W3C DID Core Specification for interoperability

This technical specification provides a detailed understanding of the method and serves as a guide for developers, implementers, and users.


# 2. Terminology

- ***Decentralized Identifier (DID):*** A globally unique identifier that is created, resolved, updated, and revoked independently of any centralized authority, enabling decentralized digital identity management.

- ***DID Document***: A JSON or JSON-LD document containing the public keys, authentication protocols, and service endpoints associated with a specific DID, allowing it to be used for cryptographic operations and communication.

- ***BTC Blockchain***: A decentralized, distributed ledger that records transactions made using BTC cryptocurrency, providing a secure and transparent mechanism for transferring value and establishing consensus.

- ***Ordinal Theory***: A framework for assigning individual identities to satoshis (the smallest unit of BTC), allowing them to be tracked, transferred, and assigned with meaning without requiring any changes to the BTC network. Ordinal theory enables the creation of unique BTC-native digital artifacts, such as inscriptions that can be held in BTC wallets and transferred using BTC transactions.

- ***Satoshis***: The atomic, native currency unit of the BTC network. One BTC can be subdivided into 100,000,000 satoshis, but no further.

- ***Inscriptions***: Unique digital artifacts created using ordinal theory, allowing satoshis to be inscribed with arbitrary content, making them collectible and tradable as curios. Inscriptions are as durable, immutable, secure, and decentralized as BTC itself.

- ***Namespace***: A part of the DID that identifies the specific DID method being used, such as "btco" for the BTC Ordinals DID Method.

- ***Verifiable Credential***: A standardized, tamper-evident digital assertion of a claim about an entity (such as an individual, organization, or device), issued by an authority and cryptographically verifiable by a recipient. Verifiable Credentials can be used as a building block in DID-based identity systems to enable trusted interactions and assertions of attributes, qualifications, or authorizations.

- ***W3C DID Core Specification***: A set of guidelines and requirements published by the World Wide Web Consortium (W3C) that define the core structure, syntax, and operations of DIDs.

# 3. Method Syntax and Structure
The syntax for the BTC Ordinals DID method follows the generic DID scheme as defined by the W3C DID Core Specification, with the addition of the method-specific identifier and optional components.

`did:btco:<method-specific-identifier>[/<path>][?<query>][#<fragment>]`

*did*: The standard prefix indicating a Decentralized Identifier.

**btco**: The namespace for the BTC Ordinals DID method.

**\<method-specific-identifier>**: A unique identifier generated using ordinal theory and representing a specific satoshi or a group of satoshis within the BTC blockchain. This identifier should be derived from the satoshi's properties, such as its inscription or other attributes.

**/<path> (optional)**: An optional path component that may be used to reference a specific part of the DID document or related resources.

**?<query> (optional)**: An optional query component that may be used to provide additional information or request specific data from the DID document or related resources.

**#<fragment> (optional)**: An optional fragment component that may be used to reference a specific section within the DID document.

Here's an example of a BTC Ordinals DID:

`did:btco:1066296127976657`

# 4. DID Document

The DID Document for the BTC Ordinals DID method contains the essential information for using a DID, such as public keys, authentication protocols, and service endpoints.

## 4.1. Data Model and Serialization Formats

The BTC Ordinals DID method follows the W3C DID Core Specification's data model, using JSON or JSON-LD as the serialization format for DID documents.

## 4.2. Creating a DID Document

To create a DID Document for the BTC Ordinals DID method:

1. Select a unique identifier from your available outputs by using ordinal theory to determine a specific satoshi within the BTC blockchain (e.g., 1066296127976657, bwtowpglzpd or 53585.3880634312).
2. Create a public/private key pair for cryptographic operations and authentication.
3. Define any necessary service endpoints for communication or interaction with the DID.
4. Create a `application/json` DID Document with the required properties, such as id, verificationMethod, authentication, keyAgreement, and service, following the DID Core Specification.
5. Create a `text/plain` document with ordinal number, name or decimal mentioned in the identifier (ie. `did:btco:1066296127976657`, `did:btco:bwtowpglzpd` or `did:btco:53585.3880634312`).
6. Inscribe the text document onto the satoshi with the json document as metadata.

### 4.2.1 Example JSON metadata

```
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://w3id.org/security/suites/ed25519-2020/v1",
    "https://w3id.org/security/suites/x25519-2020/v1"
  ],
  "id": "did:btco:bwtowpglzpd",
  "verificationMethod": [
    {
      "id": "did:btco:bwtowpglzpd#0",
      "type": "Ed25519VerificationKey2020",
      "controller": "did:btco:bwtowpglzpd",
      "publicKeyMultibase": "z6Mkhh1e5CEYYq6JBUcTZ6Cp2ranCWRrv7Yax3Le4N59R6dd"
    },
    {
      "id": "did:btco:bwtowpglzpd#1",
      "type": "X25519KeyAgreementKey2020",
      "controller": "did:btco:bwtowpglzpd",
      "publicKeyMultibase": "z6LSghwSE437wnDE1pt3X6hVDUQzSjsHzinpX3XFvMjRAm7y"
    }
  ],
  "keyAgreement": [
    "did:btco:bwtowpglzpd#1"
  ],
  "authentication": [
    "did:btco:bwtowpglzpd#0"
  ],
  "assertionMethod": [
    "did:btco:bwtowpglzpd#0"
  ],
  "service": [
    {
      "routingKeys": [],
      "accept": [
        "didcomm/v2"
      ],
      "type": "DIDCommMessaging",
      "id": "did:btco:bwtowpglzpd#2",
      "serviceEndpoint": "https://alice.did.fmgp.app/"
    }
  ]
}
```

### 4.2.2 Example inscription text

`did:btco:bwtowpglzpd`

## 4.3. Resolve a DID Document

To resolve a DID Document, retrieve the content from the most recent inscription on the satoshi associated with the method-specific identifier. If the content is a valid DID retrieve the metadata and CBOR decode it as JSON to retrieve the current document. Ensure the document `id` property matches the inscription content and that the inscription is on the sat specified in the method-specific identifier.

## 4.4. Updating a DID Document

To update a DID Document, perform the same operation as creation in 4.2 however perform a reinscription onto the specied sat. This may include updating public keys, authentication protocols, or service endpoints. To revoke a verification method an update operation is completed which removes it from the DID Document.

## 4.5. Deactivating a DID

To deactivate a DID, perform an update with the inscription content `🔥` and no metadata.

# 5. Cryptographic Operations

This section describes the cryptographic algorithms and key management processes used for signing, encrypting, and verifying DID-related data in the BTC Ordinals DID method. It also discusses specific security considerations, such as key rotation, key recovery, or handling compromised keys.

## 5.1. Flexible Cryptographic Algorithms

The BTC Ordinals DID method is designed to support a variety of cryptographic algorithms, allowing users to choose from different suites based on their security, performance, and compatibility requirements. This flexibility enables the BTC Ordinals DID method to cater to diverse use cases and user preferences while ensuring that it remains relevant and adaptable to evolving security standards and technologies.

Some examples of the cryptographic algorithms that can be used in the BTC Ordinals DID method include:

- Digital signature algorithm:
  - ECDSA (Elliptic Curve Digital Signature Algorithm) with the secp256k1 curve (used in BTC),
  - EdDSA (Edwards-curve Digital Signature Algorithm) with the Ed25519 curve,
  - Other signature algorithms that provide an appropriate level of security and compatibility.

- Key agreement algorithm:
  - ECDH (Elliptic Curve Diffie-Hellman) with the secp256k1 curve
  - ECDH with X25519

- Encryption algorithm:
  - AES (Advanced Encryption Standard) with a 256-bit key size
  - ChaCha20-Poly1305

The examples provided here are not an exhaustive list, and other algorithms that meet the necessary security and compatibility requirements may also be used.

## 5.2. Key Management

Key management in the BTC Ordinals DID method involves the following processes:

### 5.2.1 Key generation:

Generating public/private key pairs involves selecting an appropriate digital signature algorithm (e.g., ECDSA with secp256k1, EdDSA with Ed25519) and generating a key pair according to the chosen algorithm's specifications. Ensure that the key pairs are generated using a cryptographically secure random number generator, and adhere to the recommended key lengths for the chosen algorithm to maintain a high level of security.

### 5.2.2 Key rotation:

The key rotation process involves generating a new public/private key pair, creating an updated DID Document that includes the new key information, and inscribing the new DID Document as described in Section 4.4. This process transfers control of the DID to the new key pair.

### 5.2.3 Key recovery:

Key recovery in the BTC Ordinals DID method can be challenging, as the security of the DID relies on the private key's secrecy. One potential approach for key recovery is to use a Shamir's Secret Sharing scheme (SSS), splitting the private key into multiple shares that can be distributed to trusted parties. To recover the private key, a predefined threshold of shares must be combined. This approach allows for key recovery while maintaining security, as long as the threshold of shares is not compromised.

However, using a key recovery method like SSS introduces additional complexity in key management and requires careful handling of the key shares to maintain their confidentiality and availability. It is essential to consider the trade-offs of using such a recovery method and implement additional security measures to protect the key shares from unauthorized access or loss.

### 5.2.4 Handling compromised keys:

If a key is compromised, it is crucial to revoke the compromised key and update the DID Document as soon as possible by perform an update as described in Section 4.4. Notify any relying parties of the key compromise and the updated DID Document to ensure the continued security of the DID and its associated services. Additionally, it is recommended to perform a thorough security review to identify and mitigate any potential vulnerabilities that led to the key compromise.

## 5.3. Security Considerations

This section discusses specific security considerations for the BTC Ordinals DID method, including key storage and protection, key usage policies, and the security and privacy of service endpoints.

### 5.3.1 Key storage and protection

Storing and protecting private keys is crucial for ensuring the security of a DID. Some best practices for key storage and protection include:

- Using hardware wallets to store private keys securely, isolated from potentially vulnerable software environments.
- Storing keys in secure enclaves or trusted execution environments, which provide a higher level of protection against unauthorized access.
- Implementing strong encryption and access control mechanisms for key storage, such as encrypting key material with a passphrase or using multi-factor authentication for key access.

### 5.3.2 Key usage policies

Key usage policies and limitations play a critical role in the security and usability of the BTC Ordinals DID method. Some considerations for key usage policies include:

- Implementing key expiration policies, where keys are automatically considered invalid after a predefined period or after a certain number of uses.
- Defining key usage restrictions, such as limiting a key's ability to perform specific actions or interact with specific services.
- Regularly reviewing and updating key usage policies to ensure they remain relevant and effective in the context of evolving security threats and user needs.

### 5.3.3 Security and privacy of service endpoints

The security and privacy of service endpoints defined in the DID Document are essential to protecting the integrity and confidentiality of DID-related data and interactions. To enhance the security and privacy of service endpoints:

- Use encrypted communication channels, such as HTTPS or other secure transport protocols, to protect data in transit between the endpoint and its users.
- Minimize the exposure of sensitive data in service endpoints, avoiding the unnecessary collection, storage, or transmission of personal or confidential information.
- Implement robust access control mechanisms for service endpoints, ensuring that only authorized parties can access the services and data provided by the endpoint.

### 5.3.4 Risks of Ledger Attacks on BTC Ordinals DID Method

The BTC Ordinals (btco) DID Method can be impacted if the BTC blockchain is successfully attacked, posing potential threats to end-users and developers. Given the BTC network's current advanced levels of security, these attacks are so improbable that DIDs can be considered exceptionally safe.

## 6. Privacy Considerations

This section discusses privacy considerations for the BTC Ordinals DID method, including potential privacy risks and mitigations, as well as best practices for preserving privacy when using this DID method.

## 6.1. Identifier Correlation

The potential privacy risks associated with identifier correlation can be mitigated by the BTC Ordinals DID method through:

-	Using unique identifiers for different contexts, reducing the ability to link activities across various services or applications.
-	Minimizing the amount of public information in DID Documents, limiting the data that can be used to correlate identifiers and user activities.

## 6.2. Transaction Linkability

To address the privacy implications of transaction linkability within the BTC Ordinals DID method:

- Keep UTXOs managing DIDs to addresses specific to DIDs.
- Avoid using the same address for regular BTC payments.

## 6.3. Metadata Leakage

To address the potential privacy risks associated with metadata leakage, the BTC Ordinals DID method recommends:

- Including only necessary information to gain a cryptographic trust relationship.
- Use encryption for sensitive information, ensuring that only authorized parties can access and interpret the data.

## 6.4. Data Minimization

The data minimization practices adopted by the BTC Ordinals DID method to preserve user privacy include:

- Storing only the minimum amount of data required for DID operations, avoiding unnecessary information that could compromise privacy.
- Refrain from storing personally identifiable information in DID Documents or transactions, reducing the risk of identity exposure.

## 6.5. Best Practices for Privacy Preservation

Best practices for preserving privacy when using the BTC Ordinals DID method include:

- Regularly rotating keys to minimize the risk of key compromise and the exposure of DID-related activities.
- Using privacy-enhancing technologies such as VPNs or Tor to obfuscate the origin of DID-related transactions and communications.
- Keeping software up-to-date, including wallets, node software, and other tools used in the management of the BTC Ordinals DID method, to maintain the highest level of security and privacy protection.

# 7. Implementations

- [BTC Ordinals DIDs](https://github.com/aviarytech/btc-ordinal-dids) is a typescript library that uses [bun](https://bun.sh) to complete DID operations using a local Ord server and wallet

# 8. Cost Considerations

This section explores the cost implications of using the BTC Ordinals DID method, specifically addressing the BTC transaction fees associated with creating, updating, and deactivating DIDs using this method.

## 8.1. Transaction Fees

BTC transaction fees associated with creating, updating, and deactivating DIDs using the BTC Ordinals DID method are determined by factors such as network congestion and transaction size. These fees can have a significant impact on users, especially during periods of high network activity. To minimize fees, users can time transactions during periods of lower network congestion when fees are generally lower.

- Example CREATE operation (537 byte DID document at $38,700 USD/BTC)
 - 5 sat/vb = 2,005 sats = $0.78
 - 15 sat/vb = 6,015 sats = $2.33
 - 51 sat/vb = 20,451 sats = $7.92

## 8.2. Cost Comparisons with Other DID Methods

The cost implications of the BTC Ordinals DID method can be compared to other DID methods, highlighting its relative advantages or disadvantages:

- Ethereum and other ledger-based DID methods: These methods have similar cost structures, as they involve on-chain transaction fees for creating, updating, and deactivating DIDs.
- Sidechain ledger-based DID methods: These methods are generally cheaper than layer 1 ledger DIDs. However, they may have other costs associated with maintaining sidechain nodes.
-	IPFS-based DID methods (e.g., did:ipid): These methods generally have lower transaction fees, as they rely on a distributed file system instead of a blockchain for storing DID documents. However, they may have other costs associated with maintaining IPFS nodes and storing data on the network.
-	Centralized DID methods (e.g., did:web): Centralized DID methods often have minimal transaction fees, as they use traditional web infrastructure. However, they sacrifice decentralization and may have other costs related to web hosting services.

When evaluating the cost trade-offs of different DID methods, it is essential to consider the specific use case and requirements, such as the desired level of decentralization, security, and the frequency of DID-related operations.

# 9. Trade-offs

## 9.1 Advantages

### 9.1.1 Zero Counterparty Risk

Counterparty risk refers to the risk associated with the other party involved in a financial contract or transaction not meeting their obligations. This risk is completely eliminated with BTC Ordinals DID method as it does not rely on any secondary or tertiary networks (i.e., sidechains, L2 tokens) unlike other common BTC DID methods (ION). By directly using BTC's blockchain, the requirement for trust in an additional party is eradicated, thus removing the counterparty risk. It removes the need for trust in sidechains' security or any other second-layer solution, as the identity verification is directly anchored on the main blockchain.

### 9.1.2 Greatest Network Effects Possible

BTC, being the largest and most well-known blockchain, already has an extensive network of users. By using BTC Ordinals DID method, a user or organization can take advantage of this existing network effect. As more people use BTC for their digital identity needs, the value and utility of the BTC Ordinals DID method grow as well. Furthermore, as BTC has the most significant computational power backing its network, it also offers the highest level of security, which can be crucial for maintaining and protecting digital identities.

## 9.2 Disadvantages

### 9.2.1 Slow Transaction Speed

The BTC network adds a new block of transactions to its blockchain approximately every 10 minutes. This is part of BTC's consensus mechanism, designed to maintain security and prevent double-spending. But it can make the process of anchoring and verifying identities using the BTC Ordinals DID method slow, especially when compared to traditional centralized systems. Real-time or near-instantaneous verification might be critical in certain use cases, which could make this method less suitable.

### 9.2.2 High Transaction Costs

BTC transaction fees fluctuate based on the network's usage. When more people are using BTC, the demand for block space increases, and users must pay higher fees to incentivize miners to include their transactions in the next block. As such, the cost of creating and managing decentralized identifiers (DIDs) using the BTC Ordinals method can increase with the network's usage, making it expensive during periods of high activity.

# 9. Conclusion

This technical specification has introduced the BTC Ordinals DID method, a novel approach to decentralized identifiers utilizing the BTC blockchain and ordinal theory. By uniquely identifying individual satoshis, this method enables the creation, resolution, updating, and deactivation of DIDs without altering the BTC network or requiring additional sidechains or tokens.

In summary, the BTC Ordinals DID method offers a unique, secure, and practical solution for managing digital identities within the decentralized identity ecosystem, with the potential to enable a range of innovative use cases and applications.

# 10. References

## 10.1. Normative References

W3C. (2021). Decentralized Identifiers (DIDs) v1.0. Retrieved from https://www.w3.org/TR/did-core/

Ordinals Project. (n.d.). Ord Handbook. Retrieved from https://docs.ordinals.com/

## 10.2. Informative References

Satoshi Nakamoto. (2008). Bitcoin: A Peer-to-Peer Electronic Cash System. Retrieved from https://bitcoin.org/bitcoin.pdf
