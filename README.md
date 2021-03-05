# Lucky Financial

https://lucky.financial Feel free to read the code. More details coming soon.

## Deployed Contracts

### BSC MAINNET

- GoodFortuneToken - https://bscscan.com/token/0xb2Ba6fa707948f9A0BC420C35b78e5020A07bc4d
- MasterChefV2 - https://bscscan.com/address/0x9D34e58F1792bFa62ABEb08816E10B5B3aB1eac6
- Timelock - https://bscscan.com/address/0x9074EF83B3a8BF6885C1930BA177d781a1bbb1D1
- MultiCall - https://bscscan.com/address/0x1ee38d535d541c55c9dae27b12edf090c608e6fb
^ Original Multicall all Pancake Forks Use.

## Deployment

### ENV Variables
Create a `.env` file with the following content:
```
BSC_MAINNET_PRIVATE_KEY = <private_key>
BSC_TESTNET_PRIVATE_KEY = <private_key>
BSC_API_KEY = <bscscan_api_key>
```

### Deploy Contracts
- Mainnet
```sh
make deploy
```
- Testnet
```sh
make test-deploy
```
- Mainnet reset
```sh
make deploy-force
```
- Testnet reset
```sh
make test-deploy-force
```

- deploy GoodFortuneToken
- deploy MasterChefV2
- deploy Timelock
- mint GoodFortuneToken
- transfer ownership of GoodFortuneToken to MasterChefV2

### Verify Contracts
- Mainnet
```sh
make verify
```
- Testnet
```sh
make test-verify
```

### Add Pools to MasterChefV2
- Mainnet
```sh
make console
```
- Testnet
```sh
make test-console
```

```js
let chef = await MasterChefV2.deployed();
chef.add(uint256 _allocPoint, IBEP20 _lpToken, uint16 _depositFeeBP, bool _withUpdate);
```

depositFeeBP: 100 = 1%, 10000 = 100%

- add LP and Token pools to MasterChefV2 - https://github.com/luckyfinance-dev/lucky-contracts/wiki/POOLS---Farming-and-Staking

### Transfer MasterChefV2
- transfer ownership of MasterChefV2 to Timelock
- Mainnet
```sh
make console
```
- Testnet
```sh
make test-console
```

```js
let chef = await MasterChefV2.deployed();
let time = await Timelock.deployed();
chef.transferOwnership(time.address);
```

### Truffle Flaterener For BSC TestNet Verification
```js
truffle-flattener contracts/MasterChefV2.sol|pbcopy
```
remove multiple instances of License from flattener to verify code ownership