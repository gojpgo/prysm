# Modifications Made in the Pectra Branch

The idea of this repository is to pull latest changes of prysm into this fork repository and use the develop branch for it. Then, the develop branch can be merged locally into the pectra branch which contains further adjustments if necessary. The public pectra branch of this repository can be used by build pipelines.

## Changes of the prysm repository
- using latest go-ethereum module (ran go mod tidy)
- once a new go.sum has been created, check go.sum for the `github.com/ethereum/go-ethereum v1.15.0` entry (*not the entry that contanins v1.15.0/go.mod*) and take the checksum (e.g. `h1:LLb2jCPsbJZcB4INw+E/MgzUX5wlR6SdwXcv09/1ME4=`) and copy the checksum into the go_repository entry (in the file `deps.bzl`) which contains the `importpath = "github.com/ethereum/go-ethereum"`. Make sure to overwrite the checksum of the `sum` value in the go_repository.
- changed the `cmd/prysmctl/testnet/BUILD.bazel` file and added the line `"@com_github_ethereum_go_ethereum//params:go_default_library"`.
- changed the `cmd/prysmctl/testnet/generate_genesis.go` and added the line `gen.Config.BlobScheduleConfig = p.DefaultBlobSchedule` as well as the import path `p "github.com/ethereum/go-ethereum/params"`.
- after changing the import paths, you can compile new changes with `bazel build //cmd/...` (and clean false bazel loads with `bazel clean --expunge`).
- now you can run the code using the `bazel run` commands.

# Prysm: An Ethereum Consensus Implementation Written in Go

[![Build status](https://badge.buildkite.com/b555891daf3614bae4284dcf365b2340cefc0089839526f096.svg?branch=master)](https://buildkite.com/prysmatic-labs/prysm)
[![Go Report Card](https://goreportcard.com/badge/github.com/prysmaticlabs/prysm)](https://goreportcard.com/report/github.com/prysmaticlabs/prysm)
[![Consensus_Spec_Version 1.4.0](https://img.shields.io/badge/Consensus%20Spec%20Version-v1.4.0-blue.svg)](https://github.com/ethereum/consensus-specs/tree/v1.4.0)
[![Execution_API_Version 1.0.0-beta.2](https://img.shields.io/badge/Execution%20API%20Version-v1.0.0.beta.2-blue.svg)](https://github.com/ethereum/execution-apis/tree/v1.0.0-beta.2/src/engine)
[![Discord](https://user-images.githubusercontent.com/7288322/34471967-1df7808a-efbb-11e7-9088-ed0b04151291.png)](https://discord.gg/prysmaticlabs)
[![GitPOAP Badge](https://public-api.gitpoap.io/v1/repo/prysmaticlabs/prysm/badge)](https://www.gitpoap.io/gh/prysmaticlabs/prysm)

This is the core repository for Prysm, a [Golang](https://golang.org/) implementation of the [Ethereum Consensus](https://ethereum.org/en/developers/docs/consensus-mechanisms/#proof-of-stake) [specification](https://github.com/ethereum/consensus-specs), developed by [Offchain Labs](https://www.offchainlabs.com). See the [Changelog](https://github.com/prysmaticlabs/prysm/releases) for details of the latest releases and upcoming breaking changes.

### Getting Started

A detailed set of installation and usage instructions as well as breakdowns of each individual component are available in the [official documentation portal](https://docs.prylabs.network). If you still have questions, feel free to stop by our [Discord](https://discord.gg/prysmaticlabs).

### Staking on Mainnet

To participate in staking, you can join the [official eth2 launchpad](https://launchpad.ethereum.org). The launchpad is the only recommended way to become a validator on mainnet. You can explore validator rewards/penalties via Bitfly's block explorer: [beaconcha.in](https://beaconcha.in), and follow the latest blocks added to the chain on [beaconscan](https://beaconscan.com).


## Contributing
### Branches
Prysm maintains two permanent branches:

* [master](https://github.com/prysmaticlabs/prysm/tree/master): This points to the latest stable release. It is ideal for most users.
* [develop](https://github.com/prysmaticlabs/prysm/tree/develop): This is used for development, it contains the latest PRs. Developers should base their PRs on this branch.

### Guide
Want to get involved? Check out our [Contribution Guide](https://docs.prylabs.network/docs/contribute/contribution-guidelines/) to learn more!

## License

[GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)

## Legal Disclaimer

[Terms of Use](/TERMS_OF_SERVICE.md)
