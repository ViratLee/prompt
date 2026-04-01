# Test Plan: Finance Page - Swap Product

## Overview
Test plan for validating the Finance page functionality of the Swap product, covering token swapping, balance displays, transaction history, and related financial operations.

---

## Scope

### In Scope
- Token swap functionality
- Balance display and updates
- Price/rate calculations
- Transaction history
- Slippage settings
- Wallet integration

### Out of Scope
- Wallet connection flow (covered separately)
- Smart contract unit tests
- Performance/load testing

---

## Test Scenarios

### 1. Token Swap Functionality

| ID | Scenario | Priority |
|----|----------|----------|
| SW-001 | Swap tokens with valid amounts | High |
| SW-002 | Swap with insufficient balance - error displayed | High |
| SW-003 | Swap with minimum allowed amount | Medium |
| SW-004 | Swap with maximum allowed amount | Medium |
| SW-005 | Reverse swap direction (flip tokens) | High |
| SW-006 | Swap same token to itself - should be blocked | Medium |
| SW-007 | Cancel swap before confirmation | Medium |

### 2. Balance Display

| ID | Scenario | Priority |
|----|----------|----------|
| BAL-001 | Display correct token balances on page load | High |
| BAL-002 | Update balance after successful swap | High |
| BAL-003 | Show zero balance for tokens not owned | Medium |
| BAL-004 | Refresh balance manually | Low |
| BAL-005 | Display balance in correct decimal places | High |

### 3. Price/Rate Calculations

| ID | Scenario | Priority |
|----|----------|----------|
| PRC-001 | Display accurate swap rate | High |
| PRC-002 | Update rate on amount change | High |
| PRC-003 | Show price impact percentage | Medium |
| PRC-004 | Display minimum received amount | High |
| PRC-005 | Rate refresh on timer | Medium |
| PRC-006 | Handle rate unavailable gracefully | Medium |

### 4. Slippage Settings

| ID | Scenario | Priority |
|----|----------|----------|
| SLP-001 | Set custom slippage tolerance | Medium |
| SLP-002 | Use preset slippage values (0.1%, 0.5%, 1%) | Medium |
| SLP-003 | Warn on high slippage (>5%) | Medium |
| SLP-004 | Reject invalid slippage input | Low |
| SLP-005 | Persist slippage settings | Low |

### 5. Transaction History

| ID | Scenario | Priority |
|----|----------|----------|
| TXN-001 | View recent swap transactions | Medium |
| TXN-002 | Filter transactions by date | Low |
| TXN-003 | View transaction details | Medium |
| TXN-004 | Link to blockchain explorer | Low |
| TXN-005 | Show pending transaction status | High |

### 6. Token Selection

| ID | Scenario | Priority |
|----|----------|----------|
| TOK-001 | Search token by name | High |
| TOK-002 | Search token by contract address | Medium |
| TOK-003 | Select token from favorites | Medium |
| TOK-004 | Display token icons and symbols | Low |
| TOK-005 | Import custom token | Low |

### 7. Error Handling

| ID | Scenario | Priority |
|----|----------|----------|
| ERR-001 | Network connectivity loss during swap | High |
| ERR-002 | Transaction timeout | High |
| ERR-003 | Insufficient gas fees | High |
| ERR-004 | Wallet disconnection mid-swap | Medium |
| ERR-005 | Invalid input amounts (negative, special chars) | Medium |

---

## Test Environment

- **Browsers**: Chrome, Firefox, Safari, Edge
- **Networks**: Mainnet, Testnet (Goerli/Sepolia)
- **Wallets**: MetaMask, WalletConnect, Coinbase Wallet
- **Devices**: Desktop, Mobile responsive

---

## Test Data Requirements

| Data | Description |
|------|-------------|
| Test wallets | Wallets with various token balances |
| Token pairs | Common pairs (ETH/USDC, ETH/DAI) |
| Edge amounts | Min/max values, decimal limits |

---

## Tags for Execution

```gherkin
@smoke       # Critical path tests
@regression  # Full test suite
@swap        # Swap-specific tests
@balance     # Balance-related tests
@negative    # Error/edge case tests
```

---

## Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| Testnet instability | Use multiple test networks |
| Price volatility | Use stablecoins for consistent testing |
| Gas price spikes | Run tests during low-traffic periods |

---

## Acceptance Criteria

- [ ] All High priority tests pass
- [ ] No critical/blocking defects
- [ ] 90% of Medium priority tests pass
- [ ] Error messages are user-friendly
