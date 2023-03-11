# EVM Staking Vault Factory

## Deployments

```
### BSC Testnet

0x25ae56cE7EAbC7d8306090C9FCD11E3C0ea7727f

```

# Functions

## Vault Factory Public Functions

```js

    function create(
        StakingUtils.StakingConfiguration memory config,
        StakingUtils.TaxConfiguration memory taxConfig,
        StakingUtils.LockConfiguration memory lockConfig
    ) public payable

          - Deploys a new vault

    StakingUtils.StakingConfiguration {
        int256 rewardRate; // Vault reward rate in rewrdTokens/blocl
        uint256 minStake;  // Min stake amoint
        uint256 maxStake;  // Max stake amoint
        ERC20 stakingToken; // Staking token
        ERC20 rewardsToken; // Rewards token
    }

    StakingUtils.TaxConfiguration {
        uint256 stakeTax; // Tax taken by the vault creator on each stake (150 = 1.5%)
        uint256 unStakeTax; //  Tax taken by the vault creator on each un stake (100 = 1%)
        uint256 hpayFee; // Fee Taken by the service provider --> is Set this to 0 always
        address feeAddress; // The address where the creator receives his fees
        address hpayFeeAddress; // service provider fee address --> Is Set this to 0 always
        ERC20 hpayToken; // Dummy token, please set this to address(0)
    }

     StakingUtils.LockConfiguration {
        uint256 lockTime; // Fixed amount of days that the tokens must be locked for. The offset starts at the vault start time
        uint256 earlyUnlockPenalty;  // Fee to be paid by early unlocks (100 = 1%)
        bool allowEarlyUnlock; // Early unlocks are disabled
    }


    ---------------------------------------------------------------------------------------------

    function getAll(uint32 startingIndex, uint256 length) public view returns (address[] memory)

        - Returns all the deployed vaults

    ---------------------------------------------------------------------------------------------

    function getVaultAt(uint32 _index) public view returns (address);

        - Returns the vault at given index

    ---------------------------------------------------------------------------------------------

    function hasVault(address _addr) public view returns (bool);

        - Checks if a vault exists

    ---------------------------------------------------------------------------------------------
    function totalVaults() public view returns (uint256);

        - Returns the total number of deployed vaults

    ---------------------------------------------------------------------------------------------

    function version() public pure returns (uint256);

      - Returns current version of the factory
```

## Vault Public Functions

```js
    function topUpRewards(uint256 amount) public virtual

        - Used to top up rewards. Cannot be caled after the vault is stareted

    ---------------------------------------------------------------------------------------------

    function blocksLeft() public view virtual returns (uint256)

        - Returns the blocks left until the rewards runs out

    ---------------------------------------------------------------------------------------------

    function earned(address account) public view returns (uint256)

        - Returns the amount earned by a speciffic account

    ---------------------------------------------------------------------------------------------

    function stake(uint256 _amount) public virtual

        - Stake an amount

    ---------------------------------------------------------------------------------------------

    function compound() external virtual

        - Compounds the senders earnings

    ---------------------------------------------------------------------------------------------

    function withdraw(uint256 _amount) ;

        - Withdraw a speciffic ammount. If _amount is 0, the full deposit is withdrawn

    ---------------------------------------------------------------------------------------------

    function claim() external virtual;

        - Claims earnings

    ---------------------------------------------------------------------------------------------
    function setRewardRate(uint256 rate) external virtual onlyRole(MANAGER_ROLE)

        - Set rewards

    ---------------------------------------------------------------------------------------------

    function start() external onlyRole(MANAGER_ROLE);

        - Starts the vault

    ---------------------------------------------------------------------------------------------

    function getInfo() public view virtual returns (uint256[7] memory) {
        return [
            _rewardSupply,
            _totalSupply,
            blocksLeft(),
            configuration.rewardRate,
            configuration.maxStake,
            configuration.minStake
        ];
    }

        - Returns vault speciffic info

    ---------------------------------------------------------------------------------------------

    function userInfo(address account) public view virtual returns (uint256[2] memory) {
        return [reward, balance];
    }

        - Returns user user speciffic info
```
