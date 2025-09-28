# 🚀 Solana Copy Trading Bot

A high-performance Rust-based copy trading bot for Solana blockchain that automatically replicates trades from target wallets across multiple DEX platforms including Pump.fun and Raydium.

## ✨ Features

### 🔄 **Copy Trading**
- **Real-time Monitoring**: Monitors target wallets via WebSocket connections
- **Automatic Execution**: Instantly replicates buy/sell transactions
- **Multi-DEX Support**: Works with Pump.fun and Raydium DEX
- **Slippage Protection**: Configurable slippage tolerance

### ⚡ **Performance Optimizations**
- **Jito Integration**: Uses Jito bundles for MEV protection and faster execution
- **Priority Fees**: Configurable compute unit pricing for transaction prioritization
- **Async Architecture**: Built with Tokio for high-performance async operations

### 🛡️ **Security & Reliability**
- **Private Key Management**: Secure wallet key handling
- **Transaction Simulation**: Pre-flight transaction validation
- **Error Handling**: Comprehensive error handling and logging
- **Bundle Confirmation**: Waits for bundle confirmation with timeout

### 📊 **Trading Features**
- **Buy/Sell Operations**: Support for both buy and sell transactions
- **Token Management**: Automatic ATA (Associated Token Account) creation
- **Pool Detection**: Automatic pool discovery via RPC and API
- **Bonding Curve Support**: Full Pump.fun bonding curve integration

## 🏗️ Architecture

```
src/
├── common/          # Shared utilities and configurations
│   ├── logger.rs    # Logging system
│   └── utils.rs     # Common utilities and AppState
├── core/            # Core trading functionality
│   ├── token.rs     # Token operations and ATA management
│   └── tx.rs        # Transaction building and execution
├── dex/             # DEX-specific implementations
│   ├── pump_fun.rs  # Pump.fun integration
│   └── raydium.rs   # Raydium AMM integration
├── engine/          # Trading engine
│   └── swap.rs      # Swap execution logic
└── services/        # External services
    └── jito.rs      # Jito bundle service
```

## 🚀 Quick Start

### Prerequisites

- **Rust** (latest stable version)
- **Solana CLI** tools
- **RPC Endpoint** (HTTPS and WSS)
- **Private Key** for trading wallet

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/mooncitydev/solana-copytrading-bot.git
   cd solana-copytrading-bot
   ```

2. **Install dependencies**
   ```bash
   cargo build --release
   ```

3. **Configure environment variables**
   ```bash
   # Required environment variables
   export RPC_HTTPS="https://your-rpc-endpoint.com"
   export RPC_WSS="wss://your-wss-endpoint.com"
   export PRIVATE_KEY="your_base58_private_key"
   
   # Optional configuration
   export UNIT_PRICE="1"           # Compute unit price
   export UNIT_LIMIT="300000"      # Compute unit limit
   export HTTP_PROXY="http://proxy:port"  # HTTP proxy (optional)
   export LOG="debug"              # Log level
   ```

4. **Run the bot**
   ```bash
   cargo run --release
   ```

## ⚙️ Configuration

### Environment Variables

| Variable | Required | Description | Default |
|----------|----------|-------------|---------|
| `RPC_HTTPS` | ✅ | Solana RPC HTTPS endpoint | - |
| `RPC_WSS` | ✅ | Solana WebSocket endpoint | - |
| `PRIVATE_KEY` | ✅ | Base58 encoded private key | - |
| `UNIT_PRICE` | ❌ | Compute unit price for priority fees | `1` |
| `UNIT_LIMIT` | ❌ | Compute unit limit | `300000` |
| `HTTP_PROXY` | ❌ | HTTP proxy URL | - |
| `LOG` | ❌ | Log level (debug/info/error) | `info` |

### Swap Configuration

The bot supports configurable swap parameters:

```rust
pub struct SwapConfig {
    pub slippage: u64,        // Slippage in basis points
    pub swap_direction: SwapDirection,  // Buy or Sell
    pub use_jito: bool,       // Enable Jito bundles
}
```

## 🔧 Usage

### Basic Copy Trading

The bot automatically:
1. **Monitors** target wallets via WebSocket
2. **Detects** new transactions
3. **Analyzes** transaction details
4. **Executes** matching trades on your wallet
5. **Confirms** transaction success

### Supported DEX Platforms

#### 🎯 Pump.fun
- Bonding curve trading
- Virtual SOL/token reserves
- Automatic pool completion detection
- PDA (Program Derived Address) management

#### 🔄 Raydium
- AMM pool trading
- Market order support
- Pool state management
- API integration for pool discovery

## 📈 Performance Tips

### Optimize for Speed
- Use **Jito bundles** for MEV protection
- Set appropriate **priority fees**
- Use **fast RPC endpoints**
- Enable **WebSocket** for real-time updates

### Risk Management
- Set reasonable **slippage tolerance**
- Monitor **gas costs**
- Use **test wallets** for initial testing
- Implement **position sizing**

## 🛠️ Development

### Building from Source

```bash
# Debug build
cargo build

# Release build (optimized)
cargo build --release

# Run tests
cargo test

# Check code
cargo check
```

### Adding New DEX Support

1. Create new module in `src/dex/`
2. Implement swap interface
3. Add to DEX router
4. Update configuration

## 📝 Logging

The bot includes comprehensive logging:

```rust
let logger = Logger::new("[SWAP] => ".to_string());
logger.log("Transaction executed successfully".to_string());
logger.debug("Debug information".to_string());
logger.error("Error occurred".to_string());
```

## ⚠️ Disclaimer

**IMPORTANT**: This software is for educational purposes only. Trading cryptocurrencies involves substantial risk of loss. The authors are not responsible for any financial losses. Use at your own risk.

## 🤝 Support & Contact

For support, questions, or collaboration:

**📱 Telegram**: [@moooncity](https://t.me/moooncity)

Feel free to reach out for:
- Technical support
- Feature requests
- Bug reports
- Collaboration opportunities

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Solana Foundation for the excellent blockchain infrastructure
- Jito Labs for MEV protection solutions
- Raydium for AMM implementation
- Pump.fun for innovative bonding curve mechanics

---

**Happy Trading! 🚀**

*Remember: Always trade responsibly and never invest more than you can afford to lose.*
