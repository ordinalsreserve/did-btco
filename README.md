
# Bitcoin Ordinals DID Method

The Bitcoin Ordinals DID method is a decentralized identifiers (DIDs) solution that leverages the Bitcoin blockchain and ordinal theory. By uniquely identifying individual satoshis, this method enables creating, resolving, updating, and deactivating DIDs without altering the Bitcoin network or requiring additional sidechains or tokens.

## DID Syntax and DID Document

DIDs in this method have a specific syntax, which includes a method-specific identifier derived from the Bitcoin address and the ordinal position of a satoshi. The syntax can be represented as did:btco:<satoshi>.

A DID Document contains a DID's public key, authentication information, and service endpoints. The data model follows the W3C DID Core Specification, using JSON or JSON-LD as the serialization format.

## Creating a DID Document

1. Select a unique identifier using ordinal theory to determine a specific satoshi within the Bitcoin blockchain.
2. Create a public/private key pair for cryptographic operations and authentication.
3. Define any necessary service endpoints for communication or interaction with the DID.
4. Create a DID Document with the required properties following the DID Core Specification.
5. Inscribe this document (long form json or short form text) onto the satoshi with the ordinal number mentioned in the identifier.

## Resolving a DID Document

1. Retrieve the inscription data from the satoshi associated with the method-specific identifier.
2. If this utxo has been spent, look for the next DID Document by finding another inscription in the spending transaction.

## Updating a DID Document

Perform a Bitcoin transaction that sends the inscription to the control of a new public key (burns the current DID Document).
In the same transaction, inscribe the new DID Document.
The control will effectively transfer to this new DID.

## Deactivating a DID

Perform a Bitcoin transaction that updates the DID but does not transfer control to a new DID.

In summary, the Bitcoin Ordinals DID method provides a practical and secure solution for managing digital identities within the decentralized identity ecosystem. By leveraging the existing Bitcoin blockchain and ordinal theory, this method enables a range of innovative use cases and applications.
