# Foundry Smart Contract Lottery - Getting Started

This guide will help you get up and running with the Foundry Smart Contract Lottery repository. By the end, you'll have the tools installed, understand how to run the project locally, deploy smart contracts, and perform tests on different networks.

## Requirements

### Git
Ensure you have Git installed. You can verify the installation by running:
```bash
git --version
```
You should see a response like:
```
git version x.x.x
```

### Foundry
Foundry is used to compile and test smart contracts. Ensure you have it installed by running:
```bash
forge --version
```
You should see a response like:
```
forge 0.2.0 (816e00b 2023-03-16T00:05:26.396218Z)
```

## Quickstart

1. Clone the repository:
   ```bash
   git clone https://github.com/Cyfrin/foundry-smart-contract-lottery-cu
   ```

2. Navigate into the project directory:
   ```bash
   cd foundry-smart-contract-lottery-cu
   ```

3. Build the project:
   ```bash
   forge build
   ```

## Optional: Gitpod

If you don't want to install everything locally, you can use Gitpod to run the project in a browser-based IDE. 

To skip the local setup steps, simply:

- **Open in Gitpod**

## Usage

### Start a Local Node

To start a local Ethereum node, use the following command:
```bash
make anvil
```

### Install Chainlink Library (Optional)

If you're having issues installing the Chainlink library, you can run:
```bash
forge install smartcontractkit/chainlink-brownie-contracts@0.6.1 --no-commit
```

## Deployment

### Deploy to Another Network

You can deploy your smart contracts to other networks like Sepolia. More details below.
```bash
make deploy-sepolia
```

## Testing

We cover two of the four types of testing in this repo: Unit and Forked testing.

- **Unit Tests**
- **Forked Tests**

Run the tests:
```bash
forge test
```
Or run forked tests with a specific network (e.g., Sepolia):
```bash
forge test --fork-url $SEPOLIA_RPC_URL
```

### Test Coverage
To view test coverage:
```bash
forge coverage
```

## Deployment to Testnet or Mainnet

### Set Up Environment Variables

Before deploying to a testnet or mainnet, you'll need to configure environment variables in a `.env` file, similar to `.env.example`.

#### Required Variables:
- **PRIVATE_KEY**: Your account's private key. Make sure this key doesn’t have real funds for development.
- **SEPOLIA_RPC_URL**: The RPC URL for the Sepolia testnet (e.g., from Alchemy).
- **ETHERSCAN_API_KEY** (optional): Used to verify contracts on Etherscan.

### Get Testnet ETH

Obtain testnet ETH from [faucets.chain.link](https://faucets.chain.link) for testing.

### Deploy to Sepolia

To deploy to the Sepolia testnet:
```bash
make deploy-sepolia
```

This will set up a ChainlinkVRF subscription. If you already have a subscription, update it in the `scripts/HelperConfig.s.sol` file. The script will also automatically register your contract as a consumer.

### Register Chainlink Automation Upkeep

1. Visit [automation.chain.link](https://automation.chain.link) and register a new upkeep.
2. Choose "Custom logic" as your trigger mechanism.

## Scripts

After deploying to a network, you can interact with the deployed contracts via scripts.

For example, to enter the raffle locally:
```bash
cast send <RAFFLE_CONTRACT_ADDRESS> "enterRaffle()" --value 0.1ether --private-key <PRIVATE_KEY> --rpc-url $SEPOLIA_RPC_URL
```
## Estimate Gas

To estimate gas costs, you can run:
```bash
forge snapshot
```
This will generate a `.gas-snapshot` file with gas usage details.

