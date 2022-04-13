# xAnchor Contracts

xAnchor has 3 major components on the Terra-side, in addition to a bridge deployed on each foreign chain that relays operations to and from the Terra-side xAnchor contracts.

Most useful to developers building dApps on foreign chains will be the cross-chain contracts that can be interacted with:

| Network   | Component                                             | Contract Address                             |
| --------- | ----------------------------------------------------- | -------------------------------------------- |
| Avalanche | [xAnchor Bridge (AVAX)](xanchor-bridge-evm-chains.md) | `0x95aE712C309D33de0250Edd0C2d7Cb1ceAFD4550` |

Internal and intermediate xAnchor contracts:

| Network | Component                                                                          | Contract Address                               |
| ------- | ---------------------------------------------------------------------------------- | ---------------------------------------------- |
| Terra   | [xAnchor Core](xanchor-terra-side-contracts/xanchor-core.md)                       | `terra1vrf4kaj2mtck028a7ghhz505ae0vyvz5mr3ju3` |
| Terra   | [xAnchor Wormhole Bridge](xanchor-terra-side-contracts/xanchor-wormhole-bridge.md) | `terra1pw4qm09m256m3wz25n4whnuqck7rcn6wvvjzyj` |
| Terra   | [Address Proxy](xanchor-terra-side-contracts/address-proxy.md)                     | One-per-user                                   |
