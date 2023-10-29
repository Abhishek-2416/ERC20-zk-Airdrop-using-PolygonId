## On-chain ZK Verification

**The on-chain verification workflow allows Dapps to verify users' credentials inside a Smart Contract. Zero-Knowledge Proof cryptography enables this verification to happen in a private manner, namely without revealing any personal information of the user (prover).**

This flow is especially needed when further on-chain logic wants to be implemented on successful verification such as:

- Distribute a token airdrop only to human-verified accounts
- Allow voting to accounts members of your DAO
- Block airdrops to users that belong to a specific country
- Allow trading only to accounts that passed the KYC verification

**On-chain interaction between a Verifier and a user's Wallet follows this workflow:**

- First we need to write a **Verifier Smart Contract** and deploy it 
- The Verifier designs a **Request** for the users which has to be recorded on-chain inside the Verifier Smart Contract
- The Request is delivered to the user using a QR code 
- The user should then scan the QR code using his/her mobile ID wallet and parses the request
- Then the user fetches the revoaction status of the requested Credential from the issuer of the credential (this is just to know the status of the proof ig)
- Then the user generates a zk proof on mobile according to the request of the website starting from the credentials held in the wallet. This also contains the zk proof that the credential is not revoked
- The user then send the zk proof to the Verifier Smart Contract
- The Verifier Smart Contract verifies the zk Proof
- The Verifier Smart Contract checks the State of the Issuer of the credential and the State of the users are still valid and have not been revoked
- If the verification is successfull then the Verifier executes the logic defined in the Smart Contract

## Implement an ERC20 ZK Airdrop

- In This we will first create a ERC20 ZK Airdrop Contract.
- For this we will have to create a **Query** which will have the condition which is to be born before 01/01/2001
- Users that can prove that they were born before that date will be able to get the airdrop. Otherwise, they will not. The proof submitted to the Smart Contract will not reveal any information about the specific date of birth of the user as we are using zero knowledge.   

### 1. Creating a custom Schema

**To Use the Existing Schemas**
- We can go on the https://schema-builder.polygonid.me/ 
- Documentation https://devs.polygonid.com/docs/issuer/schema-builder/

**To Build Custom Schema**

Tutorials
- How to build basic schema https://www.youtube.com/watch?v=66b_jJYW78A
- Advanced features of building schema https://www.youtube.com/watch?v=YZEg3iIQFhE

Documentation https://devs.polygonid.com/docs/issuer/schema/

**A schema type is made of two documents:**

- JSON-LD Context, which contains a description of the type and its fields. 
- JSON Schema which contains the validation rules for the Issuer Node

### 2. Creating a Query 

Documentation
- Query Builder https://devs.polygonid.com/docs/verifier/query-builder/
- Zk Query Language https://devs.polygonid.com/docs/verifier/verification-library/zk-query-language/  
  
To create an Query

- To create a Query we need to go to https://schema-builder.polygonid.me/query-builder 
- After going this website we need to enter the specified values from our schema 
- After we get the Query which will be in the JSON format we need to **Copy and paste the code snippet to the GetAuthRequest function in the verifier API.**

### Setting Up the Issuer Node

- To set up the issuer node simple clone the repository https://github.com/Abhishek-2416/PolygonId-IssuerNode
- After doing this make the changes as mentioned in the top at the readme of the abhove repository
- Follow the video https://www.youtube.com/watch?v=w0anLue7yZI to know how to set up the node 




