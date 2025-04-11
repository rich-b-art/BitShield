# BitShield Privacy Pool

A privacy-preserving pool implementation for Stacks Layer 2, enabling confidential token transfers while maintaining Bitcoin's security guarantees.

## Overview

BitShield Privacy Pool is a sophisticated smart contract that enables private token transfers on the Stacks blockchain while leveraging Bitcoin's security model. It uses zero-knowledge proofs and Merkle trees to provide transaction privacy without compromising security.

## Features

- **Zero-Knowledge Privacy**: Enables private token transfers using zero-knowledge proofs
- **Merkle Tree Implementation**: Efficient commitment scheme for transaction verification
- **SIP-010 Compliance**: Full compatibility with Stacks' fungible token standard
- **Configurable Deposits**: Customizable deposit limits for risk management
- **Emergency Controls**: Admin recovery and pause mechanisms for security
- **Comprehensive Validation**: Robust input validation and security checks

## Technical Architecture

### Core Components

1. **Merkle Tree System**

   - Height: 20 levels
   - Efficient parent updating mechanism
   - Secure hash combination using SHA-256

2. **Storage Management**

   - Deposit records tracking
   - Nullifier status monitoring
   - Merkle node management

3. **Token Integration**
   - SIP-010 trait implementation
   - Secure transfer mechanisms
   - Balance management

### Security Features

- **Access Control**

  - Contract owner authorization
  - Pause functionality
  - Emergency recovery system

- **Transaction Privacy**

  - Zero-knowledge proof verification
  - Nullifier tracking
  - Commitment validation

- **Input Validation**
  - Token verification
  - Amount validation
  - Proof verification
  - Nullifier checks

## Smart Contract Interface

### Public Functions

#### Deposits

```clarity
(define-public (make-deposit
    (commitment (buff 32))
    (amount uint)
    (token <ft-trait>))
```

Creates a new deposit in the privacy pool.

#### Withdrawals

```clarity
(define-public (process-withdrawal
    (nullifier (buff 32))
    (root (buff 32))
    (proof (list 20 (buff 32)))
    (recipient principal)
    (token <ft-trait>)
    (amount uint))
```

Processes withdrawals with zero-knowledge proof verification.

#### Administrative

```clarity
(define-public (admin-recovery
    (token <ft-trait>)
    (recipient principal)
    (amount uint))
```

Emergency recovery function for contract owner.

### Read-Only Functions

- `get-contract-status`: Returns current contract state
- `get-current-root`: Retrieves current Merkle root
- `check-nullifier-status`: Checks nullifier usage
- `get-deposit-details`: Retrieves deposit information

## Error Handling

| Error Code | Description              |
| ---------- | ------------------------ |
| u1001      | Not authorized           |
| u1002      | Invalid amount           |
| u1003      | Insufficient balance     |
| u1004      | Invalid commitment       |
| u1005      | Nullifier already exists |
| u1006      | Invalid proof            |
| u1007      | Merkle tree full         |
| u1008      | Transfer failed          |
| u1009      | Unauthorized withdrawal  |
| u1010      | Invalid input            |

## Configuration

- Maximum deposit amount: 1,000,000 tokens
- Merkle tree height: 20 levels
- Zero value: 32-byte buffer of zeros

## Security Considerations

1. **Transaction Privacy**

   - Zero-knowledge proofs ensure transaction privacy
   - Nullifier system prevents double-spending
   - Merkle tree maintains efficient verification

2. **Access Control**

   - Contract owner privileges
   - Pause mechanism for emergency situations
   - Recovery function for critical scenarios

3. **Input Validation**
   - Comprehensive commitment validation
   - Strict nullifier checks
   - Proof verification system

## Best Practices for Integration

1. **Deposit Process**

   - Generate secure commitments
   - Verify amount limits
   - Ensure token approval

2. **Withdrawal Process**

   - Generate valid zero-knowledge proofs
   - Verify Merkle root
   - Handle nullifier management

3. **Error Handling**
   - Implement proper error catching
   - Validate all inputs
   - Handle response types correctly

## Development and Testing

To work with the BitShield Privacy Pool:

1. Deploy the contract to Stacks blockchain
2. Initialize with appropriate token contract
3. Test deposit and withdrawal flows
4. Verify security mechanisms
