---
id: pos-concepts
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - PoS
  - stake
---

##  {#overview}





##  {#pos-features}





###  {#epochs}











###  {#staking}



````js
const StakingContractFactory = await ethers.getContractFactory("Staking");
let stakingContract = await StakingContractFactory.attach(STAKING_CONTRACT_ADDRESS)
as
Staking;
stakingContract = stakingContract.connect(account);

const tx = await stakingContract.stake({value: STAKE_AMOUNT})
````



:::info

:::

###  {#unstaking}





````js
const StakingContractFactory = await ethers.getContractFactory("Staking");
let stakingContract = await StakingContractFactory.attach(STAKING_CONTRACT_ADDRESS)
as
Staking;
stakingContract = stakingContract.connect(account);

const tx = await stakingContract.unstake()
````



##  {#epoch-blocks}













```bash
polygon-edge genesis --epoch-size 50 ...
```



##  {#contract-pre-deployment}




