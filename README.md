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

Responses

```
  server solc --lsp
  method textDocument/semanticTokens/full
  file /Users/meek/developer/argotorg/lsp-ice/v4-core/src/libraries/Pool.sol

Spawning server...
Initializing...
Opening file...
Sending request...

{
  "error": {
    "code": -32603,
    "message": "Unhandled exception: /solidity/libsolidity/interface/CompilerStack.cpp(1249): Throw in function const SourceUnit &solidity::frontend::CompilerStack::ast(const std::string &) const\nDynamic exception type: boost::wrapexcept<solidity::langutil::InternalCompilerError>\nstd::exception::what: Parsing not yet performed.\n[solidity::util::tag_comment*] = Parsing not yet performed.\n"
  },
  "id": 2,
  "jsonrpc": "2.0"
}
```

```
  server solc --lsp
  method textDocument/rename
  file /Users/meek/developer/mmsaki/solidity-lsp-benchmarks/v4-core/src/libraries/Pool.sol

Spawning server...
Initializing...
Opening file...
Sending request...

{
  "error": {
    "code": -32603,
    "message": "Unhandled exception: /solidity/libsolidity/interface/CompilerStack.cpp(1249): Throw in function const SourceUnit &solidity::frontend::CompilerStack::ast(const std::string &) const\nDynamic exception type: boost::wrapexcept<solidity::langutil::InternalCompilerError>\nstd::exception::what: Parsing not yet performed.\n[solidity::util::tag_comment*] = Parsing not yet performed.\n"
  },
  "id": 2,
  "jsonrpc": "2.0"
}
```
