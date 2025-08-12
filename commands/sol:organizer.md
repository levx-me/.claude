# Claude Command: Solidity Organizer

Maintains well-organized structures for solidity contracts.

## Usage

```
/sol:organizer
```

## Process

1. Scan every solidity file under `src/` and/or `contracts/` except interfaces.
2. If the contract is inheriting interfaces directly, scan every public variables and check if they override interface functions. If not,  add matching view function to the interface.
3. If the contract is inheriting interfaces directly, move events and errors into interfaces.
4. Make public functions into external if it's not used inside the same contract.
5. Remove unused imports.
6. Scan every solidity file under `src/` and/or `contracts` including interfaces and check if they follow convenstions below.

| Inheriting directly meaning when the interface filename is I + <contract filename>. e.g. ERC20 inherits IERC20

## Implementation File Conventions

### File Structure
Implementation files (contracts) follow a consistent organizational pattern with specific section ordering:

```solidity
/*//////////////////////////////////////////////////////////////
                            SECTION_NAME
//////////////////////////////////////////////////////////////*/
```

### Standard Section Order for Implementation Files
1. **TYPES** - Structs, enums, and custom types
2. **STORAGE** - State variables, constants, immutables
3. **MODIFIERS** - Access control and validation modifiers  
4. **CONSTRUCTOR** - Contract initialization
5. **VIEW FUNCTIONS** - Read-only functions (often subdivided by category)
   - LOCAL VIEW FUNCTIONS
   - REMOTE VIEW FUNCTIONS  
   - REMOTE ROOT VIEW FUNCTIONS
   - REMOTE STATE VIEW FUNCTIONS
6. **LOGIC** - State-changing functions (often subdivided by category)
   - LOCAL STATE LOGIC
   - REMOTE STATE LOGIC
   - SYNC LOGIC
7. **INTERFACE IMPLEMENTATIONS** - Functions implementing specific interfaces
   - IGatewayApp IMPLEMENTATION
   - ILiquidityMatrixHook IMPLEMENTATION

### Implementation File Patterns
- Events and errors should be defined in interfaces, not implementation files
- Public functions should be external unless used internally
- Functions prefixed with `_` should be internal/private
- State variables should be grouped logically in STORAGE section
- Using statements go after contract declaration, before first section

## Interface File Conventions

### File Structure
Interface files follow a simpler but consistent structure:

### Standard Section Order for Interface Files
1. **TYPES** - Structs, enums used by interface functions
2. **ERRORS** - All custom errors for the contract
3. **EVENTS** - All events emitted by the contract
4. **VIEW FUNCTIONS** - Read-only functions (subdivided by category):
   - VERSION FUNCTIONS
   - LOCAL VIEW FUNCTIONS
   - REMOTE VIEW FUNCTIONS
   - REMOTE ROOT VIEW FUNCTIONS
   - REMOTE STATE VIEW FUNCTIONS
5. **LOGIC** - State-changing functions (subdivided by category):
   - LOCAL STATE LOGIC
   - REMOTE STATE LOGIC
   - SYNC LOGIC

### Interface File Patterns
- All events and errors should be defined in interfaces
- Functions should be grouped by logical functionality
- Include comprehensive natspec documentation
- Use consistent naming: `VIEW FUNCTIONS` for read-only, `LOGIC` for state-changing
