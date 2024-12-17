# Arbitrage API - Cryptoscan

Real-time cryptocurrency arbitrage opportunity detection service that monitors price differences across exchanges and networks

**Contacts**: https://t.me/dan_cryptoscan

What you get:

- Free setup into your hosting
- Free help to integrate app to your server
- Full access to the codebase and code updates
- Free updates for app, you can request for free updates via access to issues
- Full access to Project Time tracking by developers

## Features

- Real-time arbitrage opportunity detection
- WebSocket-based price updates
- Multi-exchange support
- Network-aware transfers
- Spread filtering capabilities
- Support for both spot and futures markets

## Architecture

The service consists of several key components:

### Network Management (`getNetwork.ts`)
- Maintains real-time network status across exchanges
- WebSocket connection to network updates
- Tracks deposit/withdrawal status and fees

### Arbitrage Detection
Two implementations available:
- Modern implementation (`getArbitrageNew.ts`) using BigNumber for precise calculations
- Classic implementation (`getArbitrage.ts`) with simpler order matching

### WebSocket Server (`websocket-server.ts`)
- Provides real-time updates to clients
- Supports spread-based filtering
- Built using Hono framework

## Installation

```bash
# Install dependencies
npm install

# Start the service
npm start
```

## Environment Variables

Create a `.env` file with required configuration:

```env
# Add any required environment variables here
```

## WebSocket API

### Connecting

Connect to the WebSocket server:
```javascript
const ws = new WebSocket('ws://localhost:3000');
```

### Message Format

Received messages follow this structure:
```typescript
interface ArbitrageMessage {
  exchangeFrom: string;
  exchangeTo: string;
  symbol: string;
  network: string;
  spread: number;
  buyPrice: number;
  sellPrice: number;
  totalAmount: number;
  totalBuyUSD: number;
  totalSellUSD: number;
  format: "hedge" | "transfer" | "delayed";
  withdrawFee: number;
  depositFee: number;
  isWithdrawEnabled: number;
  isDepositEnabled: number;
}
```

## Development

The project uses:
- TypeScript
- Bun runtime
- BigNumber.js for precise calculations
- Hono for WebSocket server
- Semantic Release for versioning

## License

ISC
# Arbitrage API

Real-time cryptocurrency arbitrage opportunity detection service that monitors price differences across exchanges and networks.

## Features

- Real-time arbitrage opportunity detection across multiple exchanges
- WebSocket-based price updates with automatic reconnection
- Multi-exchange and multi-network support
- Network-aware transfer cost calculations
- Configurable spread filtering (1-999%)
- Support for spot and futures markets
- Automatic deposit/withdrawal status tracking

## Architecture

The service consists of several key components:

### Network Management (`getNetwork.ts`)
- Maintains real-time network status across exchanges
- WebSocket connection with automatic reconnection
- Tracks deposit/withdrawal status and fees
- Caches network information for quick access

### Arbitrage Detection
Two implementations available:
- Modern implementation (`getArbitrageNew.ts`)
  - Uses BigNumber.js for precise calculations
  - Supports partial order matching
  - Real-time spread calculation
  - Handles multiple price levels
- Classic implementation (`getArbitrage.ts`)
  - Simple order book matching
  - Fee-aware calculations
  - Historical reference implementation

### WebSocket Server
- Built using Hono framework
- Provides real-time updates to clients
- Supports spread-based filtering
- Automatic client management

## Installation

```bash
# Install dependencies
npm install

# Start the service
bun start
```

## Configuration

The service supports configuration via environment variables:

```env
# Required environment variables
PORT=3000                    # Server port (default: 3000)
MIN_SPREAD=1                 # Minimum spread percentage
MAX_SPREAD=999              # Maximum spread percentage
```

## WebSocket API

### Connecting

```javascript
const ws = new WebSocket('ws://localhost:3000');
```

### Message Format

Received messages follow this structure:
```typescript
interface ArbitrageMessage {
  exchangeFrom: string;      // Source exchange
  exchangeTo: string;        // Target exchange
  symbol: string;           // Trading pair (e.g., "BTCUSDT")
  network: string;          // Transfer network ID
  spread: number;           // Profit percentage
  buyPrice: number;         // Entry price
  sellPrice: number;        // Exit price
  totalAmount: number;      // Trade volume
  totalBuyUSD: number;      // Required USD for entry
  totalSellUSD: number;     // Expected USD from exit
  format: "hedge" | "transfer" | "delayed";  // Trading strategy
  withdrawFee: number;      // Withdrawal fee
  depositFee: number;       // Deposit fee
  isWithdrawEnabled: number; // Withdrawal status
  isDepositEnabled: number;  // Deposit status
}
```

## Development

Built with:
- TypeScript for type safety
- Bun runtime for performance
- BigNumber.js for precise calculations
- Hono for WebSocket server
- Semantic Release for versioning

## License

ISC
