---
id: chainlink-vrf
title: Chainlink VRF
sidebar_label: Chainlink VRF
description: Создайте свое следующее блокчейн-приложение на Polygon.
keywords:
  - docs
  - matic
  - chainlink
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

Нативная генерация случайных чисел в детерминистической системе невозможна. Поэтому нам нужно использовать оракулы для генерирования случайных чисел. Большинство стандартных методов, таких как генерирование случайного числа из хэша блока, полагается на честность майнеров. В результате возникает среда, в которой не отсутствует доверие, что нарушает цель применения смарт-контрактов.

Мы работаем с [Chainlink VRF](https://docs.chain.link/docs/get-a-random-number) (функция подтверждаемой случайности) для создания криптографически доказуемых случайных чисел. Для этого мы отправляем запрос на нод Chainlink VRF, и он отправляет в ответ случайное число.

После развертывания кода ниже, нам нужно отправить на наш контракт немного LINK. Chainlink VRF принимает LINK как оплату оракула, аналогично тому, как сеть Polygon принимает Polygon как оплату за транзакции.
```
pragma solidity 0.6.6;

import "@chainlink/contracts/src/v0.6/VRFConsumerBase.sol";

contract RandomNumberConsumer is VRFConsumerBase {

    bytes32 internal keyHash;
    uint256 internal fee;

    uint256 public randomResult;

    /**
     * Constructor inherits VRFConsumerBase
     *
     * Network: Kovan
     * Chainlink VRF Coordinator address: 0xdD3782915140c8f3b190B5D67eAc6dc5760C46E9
     * LINK token address:                0xa36085F69e2889c224210F603D836748e7dC0088
     * Key Hash: 0x6c3699283bda56ad74f6b855546325b68d482e983852a7a82979cc4807b641f4
     */
    constructor()
        VRFConsumerBase(
            0xdD3782915140c8f3b190B5D67eAc6dc5760C46E9, // VRF Coordinator
            0xa36085F69e2889c224210F603D836748e7dC0088  // LINK Token
        ) public
    {
        keyHash = 0x6c3699283bda56ad74f6b855546325b68d482e983852a7a82979cc4807b641f4;
        fee = 0.1 * 10 ** 18; // 0.1 LINK (varies by network)
    }

    /**
     * Requests randomness from a user-provided seed
     */
    function getRandomNumber(uint256 userProvidedSeed) public returns (bytes32 requestId) {
        require(LINK.balanceOf(address(this)) >= fee, "Not enough LINK - fill contract with faucet");
        return requestRandomness(keyHash, fee, userProvidedSeed);
    }

    /**
     * Callback function used by VRF Coordinator
     */
    function fulfillRandomness(bytes32 requestId, uint256 randomness) internal override {
        randomResult = randomness;
    }
}
```

Вот детали VRF тестовой сети Polygon Mumbai. Для работы с mainnet Polygon свяжитесь с vrf@chain.link.

| Позиция | Значение |
|------|-------|
| Токен LINK | 0x326C977E6efc84E512bB9C30f76E30c160eD06FB |
| Координатор VRF | 0x8C7382F9D8f56b33781fE506E897a4F1e2d17255 |
| Хэш ключа | 0x6e75b569a01ef56d18cab6a8e71e6600d6ce853834d4a5748b720d06f878b3a4 |
| Комиссия | 0,0001 LINK |
