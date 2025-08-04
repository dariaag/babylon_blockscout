<h1 align="center">Blockscout</h1>
<p align="center">Blockchain Explorer for inspecting and analyzing EVM Chains.</p>
<div align="center">

[![Blockscout](https://github.com/blockscout/blockscout/actions/workflows/config.yml/badge.svg)](https://github.com/blockscout/blockscout/actions)
[![Discord](https://dcbadge.vercel.app/api/server/blockscout?style=flat)](https://discord.gg/blockscout)

</div>


Blockscout provides a comprehensive, easy-to-use interface for users to view, confirm, and inspect transactions on EVM (Ethereum Virtual Machine) blockchains. This includes Ethereum Mainnet, Ethereum Classic, Optimism, Gnosis Chain and many other **Ethereum testnets, private networks, L2s and sidechains**.

See our [project documentation](https://docs.blockscout.com/) for detailed information and setup instructions.

For questions, comments and feature requests see the [discussions section](https://github.com/blockscout/blockscout/discussions) or via [Discord](https://discord.com/invite/blockscout).

## About Blockscout

Blockscout allows users to search transactions, view accounts and balances, verify and interact with smart contracts and view and interact with applications on the Ethereum network including many forks, sidechains, L2s and testnets.

Blockscout is an open-source alternative to centralized, closed source block explorers such as Etherscan, Etherchain and others.  As Ethereum sidechains and L2s continue to proliferate in both private and public settings, transparent, open-source tools are needed to analyze and validate all transactions.

## Supported Projects

Blockscout currently supports several hundred chains and rollups throughout the greater blockchain ecosystem. Ethereum, Cosmos, Polkadot, Avalanche, Near and many others include Blockscout integrations. A comprehensive list is available at [chains.blockscout.com](https://chains.blockscout.com). If your project is not listed, contact the team in [Discord](https://discord.com/invite/blockscout).

## Getting Started

## Babylon Edge Devnet Configuration

This repository contains a pre-configured Blockscout instance for the **Babylon Edge Devnet** (Chain ID: 6901).

### Key Configuration Changes

- **RPC Endpoint**: `https://evm-rpc.edge-devnet.babylonlabs.io`
- **Chain ID**: `6901` (Babylon Edge devnet)
- **Indexing Start**: Block `201719`
- **Continuous Indexing**: No end block limit - indexes all new blocks as they are produced

### Quick Start

1. **Clone the repository**:
   ```bash
   git clone https://github.com/dariaag/babylon_blockscout.git
   cd babylon_blockscout
   ```

2. **Start the services**:
   ```bash
   cd docker-compose
   docker-compose up -d
   ```

3. **Access the explorer**:
   - Frontend: http://localhost
   - API: http://localhost/api/v2

4. **Check the logs**:
   ```bash
   docker-compose logs backend
   ```

5. **Monitor indexing progress**:
   ```bash
   docker exec db psql -U blockscout -d blockscout -c "SELECT COUNT(*) as block_count FROM blocks;"
   ```

### Configuration Files Modified

- `docker-compose/docker-compose.yml` - Updated RPC URLs and chain ID
- `docker-compose/envs/common-blockscout.env` - Set Babylon Edge devnet configuration
- `docker-compose/services/backend.yml` - Added explicit environment variables
- `docker-compose/services/user-ops-indexer.yml` - Updated RPC URL

### Troubleshooting

**If blocks aren't syncing**:
1. Check the backend logs: `docker-compose logs backend`
2. Verify RPC connectivity: `docker exec backend curl -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' https://evm-rpc.edge-devnet.babylonlabs.io`
3. Clear database if needed: `docker exec db psql -U blockscout -d blockscout -c "DELETE FROM logs; DELETE FROM blocks;"`

**Reset to start from a specific block**:
1. Update `FIRST_BLOCK` in `docker-compose/envs/common-blockscout.env`
2. Clear the database
3. Restart: `docker-compose down && docker-compose up -d`

### General Deployment Options

For other networks, see the [project documentation](https://docs.blockscout.com/) for instructions:

- [Manual deployment](https://docs.blockscout.com/for-developers/deployment/manual-deployment-guide)
- [Docker-compose deployment](https://docs.blockscout.com/for-developers/deployment/docker-compose-deployment)
- [Kubernetes deployment](https://docs.blockscout.com/for-developers/deployment/kubernetes-deployment)
- [Manual deployment (backend + old UI)](https://docs.blockscout.com/for-developers/deployment/manual-old-ui)
- [Ansible deployment](https://docs.blockscout.com/for-developers/ansible-deployment)
- [ENV variables](https://docs.blockscout.com/setup/env-variables)
- [Configuration options](https://docs.blockscout.com/for-developers/configuration-options)

## Acknowledgements

We would like to thank the EthPrize foundation for their funding support.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution and pull request protocol. We expect contributors to follow our [code of conduct](CODE_OF_CONDUCT.md) when submitting code or comments.

## License

[![License: GPL v3.0](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

This project is licensed under the GNU General Public License v3.0. See the [LICENSE](LICENSE) file for details.
