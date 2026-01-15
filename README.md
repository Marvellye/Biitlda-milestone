# 🚀 Jericho - Multi-Chain AI-Powered Crypto Assistant

**The future of decentralized finance meets conversational AI. Connect, transact, and manage crypto assets seamlessly across multiple blockchain networks with natural language commands.**

Built for the **Mantle Hackathon**, Jericho is a cutting-edge platform that brings blockchain accessibility to everyday users through intuitive chat interfaces—Telegram, WhatsApp, and Web.

---

## ✨ Features

- **Multi-Channel Support**: Telegram, WhatsApp, Web, and more
- **AI-Powered Transactions**: Natural language commands powered by Gemini & OpenRouter
- **Secure Wallet Management**: Military-grade encryption for private keys
- **Multi-Chain Ready**: Support for Avalanche, Ethereum, Mantle, and more via integrated providers
- **Real-Time Payments**: Integrate Paystack & Ramp for fiat onboarding
- **User-Friendly Dashboard**: Interactive web interface for wallet management
- **Production-Ready**: Fully tested and audited encryption workflows

---

## 🛠️ Tech Stack

- **Backend**: Node.js + Express
- **Database**: Supabase (PostgreSQL)
- **AI Integration**: Gemini, OpenRouter
- **Payment Processing**: Paystack, Ramp
- **Messaging**: Telegram Bot API, Twilio WhatsApp
- **Blockchain**: Web3.js, Ethers.js

---

## 🚀 Quick Start

### Prerequisites
- Node.js 16+
- PostgreSQL or Supabase account
- API keys: Telegram, Twilio, Gemini, OpenRouter, Paystack, Ramp

### Installation

1. **Clone and Install**
   ```bash
   git clone <repo-url>
   cd crypto-bot
   npm install
   ```

2. **Environment Setup**
   
   Create a `.env` file in the project root:
   ```env
   # Database
   SUPABASE_URL=your_supabase_url
   SUPABASE_KEY=your_supabase_key
   
   # Encryption (must be 32+ bytes)
   ENCRYPTION_KEY=your_32byte_encryption_key_here
   
   # AI Services
   GEMINI_API_KEY=your_gemini_key
   OPENROUTER_API_KEY=your_openrouter_key
   
   # Messaging
   TELEGRAM_BOT_TOKEN=your_telegram_bot_token
   TWILIO_ACCOUNT_SID=your_twilio_sid
   TWILIO_AUTH_TOKEN=your_twilio_token
   TWILIO_PHONE_NUMBER=your_twilio_number
   
   # Payments
   PAYSTACK_SECRET_KEY=your_paystack_key
   RAMP_API_KEY=your_ramp_key
   
   # Server
   PORT=3000
   NODE_ENV=development
   ```

3. **Database Setup**
   
   Initialize your Supabase database with the required tables:
   - `users` - User profiles and authentication
   - `wallets` - Encrypted wallet private keys and metadata
   - `transactions` - Transaction history
   - `balances` - User account balances

4. **Start the Server**
   ```bash
   npm start
   ```

   The server will run on `http://localhost:3000`

---

## 🧪 Testing

Run the included smoke tests to verify your setup:

```bash
# Test wallet encryption roundtrip (create + decrypt)
node tests/decrypt_roundtrip.js

# Verify wallet integrity across database
node tests/scan_wallets.js

# Test transaction failure with invalid keys (should fail gracefully)
node tests/send_with_bad_key.js

# Check wallet balances
node tests/list_wallet_balances.js

# Test USDT balance retrieval
node tests/test_usdt_balance.js
```

---

## 📋 API Endpoints

### Wallet Management
- `POST /wallet/create` - Create a new wallet for a user
- `GET /wallet/:address` - Get wallet details
- `POST /wallet/send` - Send crypto transaction

### User Management
- `POST /user/register` - Register new user
- `GET /user/:id` - Get user profile
- `POST /user/update` - Update user settings

### Payments
- `POST /paystack/webhook` - Paystack payment notifications
- `POST /whatsapp/webhook` - WhatsApp message webhooks
- `POST /twilio/webhook` - Twilio SMS/WhatsApp webhooks

---

## 🔐 Security & Encryption

Jericho implements battle-tested encryption for private key management:

- **Encryption Standard**: AES-256-GCM
- **Key Format**: `iv:tag:encrypted`
- **ENCRYPTION_KEY Requirements**: Minimum 32 bytes (256-bit)

### Wallet Encryption Verification

```bash
# Scan all wallets for encryption integrity
node tests/scan_wallets.js
```

If any wallet shows as invalid or undecryptable:
1. Verify `ENCRYPTION_KEY` matches the original value
2. Recreate wallet for affected user if necessary
3. Migrate user funds to new wallet

---

## 🌍 Deployment

### Deploy to Heroku

```bash
# Install Heroku CLI if needed
npm install -g heroku

# Login to Heroku
heroku login

# Create app
heroku create your-Jericho-app

# Set environment variables
heroku config:set SUPABASE_URL=your_url
heroku config:set SUPABASE_KEY=your_key
heroku config:set ENCRYPTION_KEY=your_32byte_key
# ... set remaining env vars

# Deploy
git push heroku main
```

### Deploy to Docker

```dockerfile
FROM node:16-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

Build and run:
```bash
docker build -t Jericho .
docker run -p 3000:3000 --env-file .env Jericho
```

### Deploy to AWS Lambda

Use the serverless framework for API Gateway integration:

```bash
npm install -g serverless
serverless create --template aws-nodejs
```

---

## 📱 Using the Bot

### Telegram
1. Find `@YourJerichoName` on Telegram
2. Start with `/start`
3. Create wallet: "Create my wallet"
4. Send crypto: "Send 0.5 AVAX to 0x..."

### WhatsApp
Text your bot number with natural language requests:
- "What's my balance?"
- "Send 100 USDT to address"
- "Show my transactions"

### Web Dashboard
Open `http://localhost:3000` to access the interactive dashboard

---

## 🐛 Troubleshooting

### "Invalid private key" Error

**Solution:**
1. Verify `ENCRYPTION_KEY` is set and 32+ bytes
2. Run `node tests/scan_wallets.js` to identify problematic wallets
3. Check logs for "Failed to decrypt private key" messages
4. Recreate wallet if necessary

### Transaction Failures

- Verify wallet has sufficient balance
- Check network connectivity
- Ensure blockchain RPC endpoints are accessible
- Review provider configuration in `config/providers.js`

### Database Connection Issues

- Confirm Supabase credentials in `.env`
- Test connection: `node tests/list_wallet_balances.js`
- Check firewall/VPN settings

---

## 📞 Support & Contributing

Have ideas or found bugs? We're open to contributions!

- **Issues**: Report bugs via GitHub Issues
- **Features**: Submit feature requests with use cases
- **Security**: Please report security issues privately

---

## 📄 License

MIT License - See LICENSE file for details

---

**Built with ❤️ for the Mantle Hackathon**
