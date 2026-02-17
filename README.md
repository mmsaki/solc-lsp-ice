# Solc LSP InternalCompilerError

<https://www.youtube.com/watch?v=nwLf5o3cBlk>

`solc --lsp` crashes with an `InternalCompilerError` when performing a **rename** (`textDocument/rename`) or requesting **semantic tokens** (`textDocument/semanticTokens/full`) on [`./Pool.sol`](./Pool.sol).

## Reproduce

1. Install solc v0.8.33

```
pip install solc-select
solc-select install 0.8.33
solc-select use 0.8.33
```

2. Clone this repo

```
git clone https://github.com/mmsaki/solc-lsp-ice.git
```

3. Open `src/libraries/Pool.sol` in any editor configured to use `solc --lsp` as the language server

4. Try to **rename** any symbol (e.g. the contract name or a function parameter) — the LSP server crashes with:

```
InternalCompilerError: Parsing not yet performed.
```

## Error Response

```json
{
  "error": {
    "code": -32603,
    "message": "Unhandled exception: /solidity/libsolidity/interface/CompilerStack.cpp(1249): Throw in function const SourceUnit &solidity::frontend::CompilerStack::ast(const std::string &) const\nDynamic exception type: boost::wrapexcept<solidity::langutil::InternalCompilerError>\nstd::exception::what: Parsing not yet performed.\n[solidity::util::tag_comment*] = Parsing not yet performed.\n"
  },
  "id": 2,
  "jsonrpc": "2.0"
}
```

## Affected LSP Methods

| Method | Result |
|---|---|
| `textDocument/rename` | InternalCompilerError |
| `textDocument/semanticTokens/full` | InternalCompilerError |

## Environment

- **solc**: 0.8.33

## Automated Reproduction (optional)

You can also reproduce this with [lsp-bench](https://github.com/mmsaki/solidity-lsp-benchmarks):

```
cargo install lsp-bench
lsp-bench --config test.yaml
```

> **Note:** If using the `replay` CLI command directly, update the `uri` path to match your local system.
> Replace `/path/to/solc-lsp-ice` with the absolute path to where you cloned this repo.

```sh
# InternalCompilerError 1 — rename
lsp-bench replay --server "solc --lsp" --project . --input '{"id":1,"jsonrpc":"2.0","method":"textDocument/rename","params":{"newName":"NewName","position":{"character":15,"line":109},"textDocument":{"uri":"file:///path/to/solc-lsp-ice/src/libraries/Pool.sol"}}}'
# InternalCompilerError 2 — semantic tokens
lsp-bench replay --server "solc --lsp" --project . --input '{"id":1,"jsonrpc":"2.0","method":"textDocument/semanticTokens/full","params":{"textDocument":{"uri":"file:///path/to/solc-lsp-ice/src/libraries/Pool.sol"}}}'
```
