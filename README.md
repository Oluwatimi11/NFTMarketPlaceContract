# NFT Marketplace Contract v2.0 - README

## Overview
The **NFT Marketplace Contract v2.0** is a highly secure and decentralized smart contract for trading NFTs (Non-Fungible Tokens). It offers comprehensive error handling, security features, and configurable parameters to facilitate seamless NFT transactions. This contract is built on the **Clarity** language and follows the **SIP-009 NFT standard**.

## Features
- **Secure NFT Listings:** Users can list NFTs for sale with customizable pricing, royalties, and expiration settings.
- **Price Reduction Mechanism:** Enables dynamic price adjustments over time to encourage sales.
- **Batch Operations:** Supports bulk purchases with a limit of 50 NFTs per batch.
- **Royalty Payments:** Ensures original creators receive royalties on secondary sales.
- **Platform Fee Management:** Allows contract owner to set platform fees up to 5%.
- **Whitelisted NFT Contracts:** Restricts transactions to approved NFT contracts for security.
- **Error Handling:** Implements detailed error codes for precise debugging.
- **Administrative Controls:** Includes emergency pause and unpause features for contract security.

## Constants & Configuration
- **Contract Owner:** The deployer of the contract.
- **Max Batch Size:** 50 (Maximum NFTs purchasable in a single batch).
- **Min Listing Price:** 1000 microSTX.
- **Max Royalty:** 20% (2000 basis points).
- **Max Platform Fee:** 5% (500 basis points).
- **Price Reduction Interval:** 86,400 seconds (24 hours).
- **Min & Max Price Reduction Rate:** 5% to 30%.

## Error Codes
| Code | Description |
|------|------------|
| 100  | Unauthorized access |
| 101  | NFT not listed |
| 102  | Invalid payment |
| 103  | NFT already listed |
| 104  | Empty batch transaction |
| 105  | Batch size exceeded |
| 106  | Price below minimum |
| 107  | Marketplace paused |
| 108  | Invalid royalty percentage |
| 109  | Invalid NFT contract |
| 110  | NFT transfer failed |
| 111  | Payment failed |
| 112  | Price too high |
| 113  | Invalid price reduction rate |
| 114  | Listing expired |
| 115  | Self-transfer not allowed |

## Data Structures
- **Listed NFTs:** Stores NFT listings with price, seller, royalty, expiration, and reduction rate.
- **Marketplace Stats:** Tracks total volume and last update time.
- **Whitelisted NFT Contracts:** Maintains a list of approved NFT contracts.
- **State Variables:**
  - `marketplace-paused`: Boolean flag for contract pause.
  - `platform-fee-percentage`: Platform fee in basis points.
  - `total-volume-locked`: Total value of locked NFTs.
  - `last-price-check`: Tracks last price calculation.

## NFT Interface (SIP-009 Compliant)
```clarity
transfer(from, to, tokenId) -> bool
get-owner(tokenId) -> principal
get-token-uri(tokenId) -> optional(string-ascii 256)
```

## Functions

### Public Functions
- `create-secure-listing(nft-contract, nft-id, initial-price, creator-royalty, price-reduction-rate, listing-duration) -> bool`
  - Lists an NFT for sale with security checks.
- `secure-batch-purchase(nft-contract, nft-ids) -> bool`
  - Allows batch purchases up to the max batch size.
- `set-platform-fee(new-fee-percentage) -> bool`
  - Updates platform fee within allowed limits.
- `whitelist-nft-contract(contract-principal) -> bool`
  - Adds an NFT contract to the whitelist.
- `emergency-pause() -> bool`
  - Pauses all marketplace activities.
- `emergency-unpause() -> bool`
  - Resumes marketplace activities.

### Read-Only Functions
- `get-listed-nft(nft-contract, nft-id) -> map`
  - Fetches details of a listed NFT.
- `get-current-price(nft-contract, nft-id) -> uint`
  - Computes the current price based on time-based reductions.

## Security Features
- **Role-Based Access Control:** Only the contract owner can manage platform fees and whitelist contracts.
- **Transaction Safety:** Prevents unauthorized transactions and self-transfers.
- **Atomic Operations:** Ensures that payments and NFT transfers succeed together or fail entirely.
- **Emergency Controls:** Contract owner can pause/unpause trading during security events.

## Usage Guidelines
### 1. Whitelisting NFT Contracts
- Only whitelisted NFT contracts can be listed for sale.
- Contract owner manages the whitelist.

### 2. Creating Listings
- Must meet minimum price and royalty constraints.
- Price reductions follow configured intervals.

### 3. Purchasing NFTs
- Payments are distributed to seller, creator (royalty), and platform fee.
- Batch purchases optimize multiple transactions.

### 4. Admin Functions
- Set platform fees within allowed limits.
- Pause/unpause marketplace for security.

## Conclusion
The **NFT Marketplace Contract v2.0** ensures **secure, fair, and flexible** NFT trading with robust security mechanisms. Users can confidently trade NFTs while creators and sellers benefit from structured revenue sharing and transparent pricing models.

