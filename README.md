# Solc LSP InternalCompilerError

```sh
lsp-bench replay --server "solc --lsp" --project v4-core --input '{"id":1,"jsonrpc":"2.0","method":"textDocument/rename","params":{"newName":"NewName","position":{"character":15,"line":109},"textDocument":{"uri":"file:///Users/meek/developer/mmsaki/solidity-lsp-benchmarks/v4-core/src/libraries/Pool.sol"}}}'
```

Install lsp-bench from [github releases](https://github.com/mmsaki/solidity-lsp-benchmarks/releases/tag/v0.2.2) or crates.io

```
cargo install lsp-bench
```

## Step Up

1. Clone uniswap/v4-core in the root here

```
git clone https://github.com/uniswap/v4-core.git
```

2. Run LSP benchmark

```
lsp-bench --config test.yaml
```

or

```sh
# InternalCompilerError 1
lsp-bench replay --server "solc --lsp" --project v4-core --input '{"id":1,"jsonrpc":"2.0","method":"textDocument/rename","params":{"newName":"NewName","position":{"character":15,"line":109},"textDocument":{"uri":"file:///Users/meek/developer/mmsaki/solidity-lsp-benchmarks/v4-core/src/libraries/Pool.sol"}}}'
# InternalCompilerError 2
lsp-bench replay --server "solc --lsp" --project v4-core --input "{\"id\":1,\"jsonrpc\":\"2.0\",\"method\":\"textDocument/semanticTokens/full\",\"params\":{\"textDocument\":{\"uri\":\"file:///Users/meek/developer/argotorg/lsp-ice/v4-core/src/libraries/Pool.sol\"}}}"
```
