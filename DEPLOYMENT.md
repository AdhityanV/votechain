# Smart Contract Deployment Guide

## Prerequisites

1. **MetaMask Wallet**: Install MetaMask browser extension
2. **Sepolia ETH**: Get test ETH from [Sepolia Faucet](https://sepoliafaucet.com/)
3. **Remix IDE**: Use [Remix](https://remix.ethereum.org/) for easy deployment

## Deployment Steps

### Option 1: Using Remix IDE (Recommended)

1. **Open Remix IDE**: Go to https://remix.ethereum.org/

2. **Create Contract File**:
   - Create a new file called `Voting.sol`
   - Copy the contract code from `contracts/Voting.sol`

3. **Compile Contract**:
   - Go to "Solidity Compiler" tab
   - Select compiler version `0.8.19` or higher
   - Click "Compile Voting.sol"

4. **Deploy Contract**:
   - Go to "Deploy & Run Transactions" tab
   - Select "Injected Provider - MetaMask" as environment
   - Make sure you're connected to Sepolia network
   - Select "Voting" contract
   - Click "Deploy"
   - Confirm transaction in MetaMask

5. **Copy Contract Address**:
   - After deployment, copy the contract address
   - You'll need this for the frontend

### Option 2: Using Hardhat (Advanced)

1. **Install Hardhat**:
   ```bash
   npm install --save-dev hardhat @nomicfoundation/hardhat-toolbox
   ```

2. **Initialize Hardhat**:
   ```bash
   npx hardhat init
   ```

3. **Configure Network** (in `hardhat.config.js`):
   ```javascript
   require("@nomicfoundation/hardhat-toolbox");
   
   module.exports = {
     solidity: "0.8.19",
     networks: {
       sepolia: {
         url: "https://rpc.sepolia.org",
         accounts: ["YOUR_PRIVATE_KEY"] // Never commit this!
       }
     }
   };
   ```

4. **Deploy**:
   ```bash
   npx hardhat run scripts/deploy.js --network sepolia
   ```

## After Deployment

1. **Set Contract Address in Frontend**:
   - Open VoteChain in your browser
   - Click "Set Contract Address" button in header
   - Paste your deployed contract address
   - Click "Save"

2. **Test VoteChain**:
   - Connect your MetaMask wallet
   - Switch to Sepolia network
   - As admin, add candidates and authorize voters
   - Test voting functionality

## Contract Features

- **Admin Functions**: Add candidates, authorize voters, end election
- **Voter Functions**: Cast votes (only authorized voters)
- **View Functions**: Get candidates, results, voter info
- **Events**: Real-time updates for all actions

## Security Notes

- Only the deployer (admin) can add candidates and authorize voters
- Voters can only vote once
- Election can be ended by admin only
- All votes are transparent and verifiable on blockchain

## Troubleshooting

- **Transaction Failed**: Check you have enough Sepolia ETH
- **Contract Not Found**: Verify contract address is correct
- **Network Issues**: Ensure you're on Sepolia testnet
- **MetaMask Issues**: Try refreshing page and reconnecting wallet