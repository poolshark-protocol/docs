# Trustless Code Storage

## What It Does

The code storage layer directly relates to the [execution layer](execution.md). The code that the execution layer uses exists on IPFS, which is immutable, the IPFS hash resolves to a precompiled [AssemblyScript](https://www.assemblyscript.org/) file, compiled into [Wasm](https://webassembly.org/) binary instructions which can then be executed on.

[DIAGRAM HERE: SHOWING RETRIEVAL OF POLYWRAP RESOLVER FROM IPFS]

--8<-- "docs/commons/abbreviations.md"