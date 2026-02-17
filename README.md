# Solc LSP InternalCompilerError

```sh
lsp-bench replay --server "solc --lsp" --project v4-core --input '{"id":1,"jsonrpc":"2.0","method":"textDocument/rename","params":{"newName":"NewName","position":{"character":15,"line":109},"textDocument":{"uri":"file:///Users/meek/developer/mmsaki/solidity-lsp-benchmarks/v4-core/src/libraries/Pool.sol"}}}'
```

Install [lsp-bench](https://github.com/mmsaki/solidity-lsp-benchmarks/releases/tag/v0.2.2) from github releases or crates.io

```
cargo install lsp-bench
```

## Step to reproduce

Clone uniswap/v4-core in the root here

```
git clone https://github.com/uniswap/v4-core.git
