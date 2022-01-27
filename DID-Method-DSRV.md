# DSRV DID Method

## Summary
The purpose of DSRV DID is to be able to prove ownership of addresses of various heterogeneous blockchains through a single DID. Through this, users can submit and use proof that they control a specific address, such as moving assets through a blockchain bridge operated by a third party, or withdrawing from a centralized exchange that requires KYC.

## DSRV DID Scheme
DSRV decentralized identifiers(DID) is of the following format:
```
dsrv-did = "did:dsrv:" + dsrv-specific-id-string
dsrv-specific-id-string = Cosmos address without prefix
```

## Example
DSRV DID Example:
```
did:dsrv:1nyznmezcm7zkjw0glt3y4y4tnhagw6yg00ru87
```

## CRUD


### Create
* Documents are created through [@dsrv/kms](https://www.npmjs.com/package/@dsrv/kms) and is not saved at the time of creation.
* Identifiers are generated according to the Cosmos address system and can be verified using `blockchainAccountId`.

DSRV DID Document Example:
```json
{
    "@context": ["https://www.w3.org/ns/did/v1"],
    "id": "did:dsrv:1nyznmezcm7zkjw0glt3y4y4tnhagw6yg00ru87",
    "verificationMethod": [
        {
            "id": "did:dsrv:1nyznmezcm7zkjw0glt3y4y4tnhagw6yg00ru87#controller",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:dsrv:1nyznmezcm7zkjw0glt3y4y4tnhagw6yg00ru87",
            "blockchainAccountId": "cosmos:dsrv:1nyznmezcm7zkjw0glt3y4y4tnhagw6yg00ru87"
        }
    ]
}
```

### Read
* Only Revoke status of DSRV DID Identifier can be read through API or Registry(Blockchain).
* The issuer can include an API that can inquire the status of did when issuing VC.
* The status of the identifier is verified through the blockchain.
* Alternatively, the status can be checked through the API included in the VC.

### Update
* DID Document does not support update.

### Delete (Revoke)
* There are cases where the DID is revoked by itself,
* And there are cases where the issuer revokes a specific DID.
* In the case of self-revoke of DID, it is recorded and announced on the blockchain, so it is a permanent revoke.
* When the issuer revokes the DID, it is recorded on the blockchain and announced, so it is also a permanent revoke.
* And there is a temporary revocation announcing the revocation through the issuer's API.
* Therefore, the resolver must search the API and the blockchain together.


## Security and Privacy Considerations
* DID Document and Iddentifier are created through the wallet [@dsrv/kms](https://www.npmjs.com/package/@dsrv/kms), and security is maintained as long as your private key is not exposed.
* DID Document does not contain personal information.

## References
[1]. W3C Decentralized Identifiers (DIDs) v1.0, https://w3c.github.io/did-core/