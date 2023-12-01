
# BTC Ordinals DID Method

> Latest version: [0.1.0](./spec.md)

The BTC Ordinals DID method is a decentralized identifiers (DIDs) method that leverages the BTC blockchain and ordinal theory. By uniquely identifying individual satoshis, this method enables creating, resolving, updating, and deactivating DIDs without altering the BTC network or requiring additional sidechains or tokens.

## Implementations

- [btc-ordinal-dids](https://github.com/aviarytech/btc-ordinal-dids) - Typescript and bun implementation that relies on the [ord](https://github.com/ordinals/ord) explorer and wallet

## DID Syntax and DID Document

DIDs in this method have a specific syntax, which includes a method-specific identifier derived from the ordinal position of a satoshi. The syntax can be represented as did:btco:<satoshi> and <satoshi> can be in it's name, number or decimal format as described by [Ordinal Theory](https://docs.ordinals.com/overview.html).

A DID Document contains a DID's public keys, authentication information, and service endpoints. The data model follows the W3C DID Core Specification, using JSON or JSON-LD as the serialization format.

## Operations

### Creating a DID Document

1. Select a unique identifier using ordinal theory to determine a specific satoshi within the BTC blockchain.
2. Create a public/private key pair for cryptographic operations and authentication.
3. Define any necessary service endpoints for communication or interaction with the DID.
4. Create a DID Document with the required properties following the DID Core Specification.
5. Inscribe a text document with the DID onto the satoshi with the ordinal number mentioned in the identifier and using the DID Document as metadata.

### Resolving a DID Document

1. Retrieve the content from the most recent inscription on the satoshi associated with the method-specific identifier.
2. If the content is a valid DID retrieve the metadata and CBOR decode it as JSON to retrieve the current document.
3. Ensure the document `id` property matches the inscription content.
4. Ensure the inscription is on the sat specified in the method-specific identifier.

### Updating a DID Document

1. Perform the same operation as creation however perform a reinscription onto the specified sat.

### Deactivating a DID

1. Perform an update with the inscription content `🔥` and no metadata.

## Conclusion

The BTC Ordinals DID method provides a practical and secure solution for managing digital identities within the decentralized identity ecosystem. By leveraging the existing BTC blockchain and ordinal theory, this method enables a range of innovative use cases and applications.
