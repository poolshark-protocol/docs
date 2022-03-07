# Core ERC-20

The core ERC-20 contract provides the base functionality required by the protocol, plus extra functions that can be utilized by modules to optimize gas usage, while still providing a full feature set of asset management.

In order to add additional functionality, modules must be authorized to interact with the core ERC-20 contract functionality. This is currently managed and operated by an admin function, but could be subject to decentralized governance in the future.

## Check Module Authorized Status
``` mermaid
graph LR
  A[User] --->|calls| B{Module};
  B --->|calls| C{Core};
  C --->|checks| D[Authorized?];
  D -->|Yes| C;
  D ---->|No| B;
```

## Authorize New Module
``` mermaid
graph LR
  A[Admin] --->|calls| B{core.updateModule};
  B -->|updates| C[authorizedModules];
  C --->|sets true/false| D[moduleAddress];
```
