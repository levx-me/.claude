# Claude Command: Solidity Commenter

Adds or updates well-organized natspec comments for solidity contracts.

## Usage

```
/sol:commenter
```

## Process

1. Scan every solidity file under `src/` and/or `contracts/` except interfaces.
2. Add or update contract-level natspec comment to each contract. If current comment is correct, don't update.
3. Scan every function in that contract and do:
  - If that function was inherited from interfaces directly and the interface function already has a natspec comment, update natspec comment  to @inheritdoc. If that function already had comment but the parent interface doesn't have it then move it to the interface. If the function comment is missing, create natspec comment that should be exposed in the interface level and add it to the interface function.
  - public variables are functions so find the matching function in the interface and do like above.
  - If that function was not inherited, add or update the natspec comment respecting the implementation.
  - Don't add comments to internal or private functions.

| Inheriting directly meaning when the interface filename is I + <contract filename>. e.g. ERC20 inherits IERC20
