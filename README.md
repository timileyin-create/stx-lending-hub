# STX Lending Hub

A secure, decentralized lending protocol built on Stacks blockchain that enables Bitcoin-backed loans through STX collateralization. This protocol leverages Stacks' unique position as a Bitcoin L2 to provide transparent and efficient lending services.

![STX Lending Hub](https://images.unsplash.com/photo-1639322537228-f710d846310a?auto=format&fit=crop&q=80&w=1200&h=400)

## Features

- **Bitcoin-backed Security**: Utilizes Stacks' Bitcoin L2 capabilities for secure lending
- **Dynamic Interest Rates**: Algorithmic interest rate model based on market conditions
- **Flexible Collateralization**: Supports up to 500% collateral ratio
- **Automated Liquidations**: Protects protocol stability through efficient liquidation mechanisms
- **Transparent Parameters**: All protocol parameters are publicly visible and verifiable

## Protocol Parameters

- Maximum Collateral Ratio: 500%
- Minimum Collateral Ratio: 110%
- Default Collateral Requirement: 150%
- Liquidation Threshold: 130%
- Protocol Fee: 1% (adjustable up to 10%)

## Core Functions

### User Operations

#### Deposit

```clarity
(define-public (deposit))
```

- Deposits STX tokens as collateral
- Amount determined by transaction value
- Updates user's collateral position
- Returns deposited amount

#### Borrow

```clarity
(define-public (borrow (amount uint)))
```

- Borrows STX against deposited collateral
- Requires minimum collateralization ratio (150% by default)
- Updates user's borrowed amount
- Returns borrowed amount

#### Repay

```clarity
(define-public (repay (amount uint)))
```

- Repays borrowed STX
- Reduces user's outstanding debt
- Updates protocol statistics
- Returns repaid amount

#### Withdraw

```clarity
(define-public (withdraw (amount uint)))
```

- Withdraws STX collateral
- Requires maintaining minimum collateral ratio
- Updates user's position
- Returns withdrawn amount

### Liquidation Mechanism

```clarity
(define-public (liquidate (user principal)))
```

- Liquidates under-collateralized positions
- Triggers at 130% collateral ratio
- Transfers collateral to liquidator
- Clears user's position

### Read-Only Functions

#### Get User Position

```clarity
(define-read-only (get-user-position (user principal)))
```

Returns:

- Total collateral
- Total borrowed amount
- Loan count

#### Get Protocol Stats

```clarity
(define-read-only (get-protocol-stats))
```

Returns:

- Total deposits
- Total borrows
- Current protocol parameters

### Administrative Functions

#### Set Minimum Collateral Ratio

```clarity
(define-public (set-minimum-collateral-ratio (new-ratio uint)))
```

- Updates minimum required collateral ratio
- Range: 110% to 500%
- Owner-only function

#### Set Liquidation Threshold

```clarity
(define-public (set-liquidation-threshold (new-threshold uint)))
```

- Updates liquidation trigger threshold
- Must be below minimum collateral ratio
- Owner-only function

#### Set Protocol Fee

```clarity
(define-public (set-protocol-fee (new-fee uint)))
```

- Updates protocol fee percentage
- Maximum: 10%
- Owner-only function

## Security Features

1. **Access Control**

   - Owner-only administrative functions
   - Protected parameter updates
   - Anti-self-liquidation measures

2. **Safety Checks**

   - Minimum collateral requirements
   - Maximum parameter bounds
   - Balance validations

3. **Error Handling**
   - Comprehensive error codes
   - Explicit failure conditions
   - Safe arithmetic operations

## Position Management

### Collateral Ratio Calculation

```clarity
(define-private (get-collateral-ratio (collateral uint) (debt uint)))
```

- Calculates current collateral ratio
- Handles zero debt cases
- Used for borrowing and liquidation checks

### Interest Calculation

```clarity
(define-private (calculate-interest (principal uint) (rate uint) (blocks uint)))
```

- Computes interest per block
- Accounts for protocol fee
- Updates interest on position changes

## Error Codes

- `ERR-NOT-AUTHORIZED (u100)`: Unauthorized operation attempt
- `ERR-INSUFFICIENT-COLLATERAL (u101)`: Collateral below required ratio
- `ERR-INVALID-AMOUNT (u102)`: Invalid transaction amount
- `ERR-LOAN-NOT-FOUND (u103)`: Non-existent loan reference
- `ERR-LOAN-ACTIVE (u104)`: Active loan state conflict
- `ERR-INSUFFICIENT-BALANCE (u105)`: Insufficient funds for operation
- `ERR-LIQUIDATION-FAILED (u106)`: Failed liquidation attempt
- `ERR-INVALID-PARAMETER (u107)`: Invalid parameter value

## Best Practices for Users

1. **Maintaining Healthy Positions**

   - Keep collateral ratio above 150%
   - Monitor market conditions
   - Repay loans promptly

2. **Avoiding Liquidation**

   - Add collateral when ratio drops
   - Repay partial debt to improve ratio
   - Set up monitoring alerts

3. **Efficient Borrowing**
   - Calculate optimal borrow amount
   - Consider interest accumulation
   - Plan for market volatility

## Development and Testing

1. Clone the repository
2. Deploy contract to Stacks network
3. Interact using Stacks wallet
4. Test all functions thoroughly

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting pull requests.
