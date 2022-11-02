---
id: web-wallet-v2-guide
title: Руководство по использованию веб-кошелька
description: Научитесь использовать Polygon Wallet Suite.
keywords:
  - wallet
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Мы переработали интерфейс Polygon Wallet Suite и внесли отличные исправления в UX, ускорили процессы депозита и вывода, добавили превосходный модуль отслеживания депозитов и выводов и добавили в приложение уведомления для правильного отображения состояния.

:::note

Большая часть используемых нами изображений поступает из среды тестовой сети. Версия Mainnet может показать некоторые незначительные отличия.

:::

:::note

Чтобы начать процедуру депозита и вывода средств, вы можете выбрать кошелек Polygon или мост Polygon на странице назначения. Мы начнем это руководство со ссылки на кошелек.

:::

## Вход в Polygon Wallet Suite {#logging-into-the-polygon-wallet-suite}

Информацию по подключению Polygon к Metamask можно найти в этом [руководстве](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/).

Чтобы войти в Polygon Wallet Suite, вам потребуется перейти по следующему URL: https://wallet.polygon.technology/.

Чтобы войти в версию Polygon Wallet Suite в тестовой сети, перейдите по следующему URL: https://wallet-dev.polygon.technology/.

Чтобы научиться подключать Polygon к Metamask, используйте это [руководство](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/).

После подключения аккаунта к веб-кошельку вы перейдете на страницу назначения с разными способами взаимодействия с ним. Цепочка Polygon POS в настоящее время предлагает следующие сервисы:
- Кошелек Polygon для отправки, получения и хранения активов в сети Polygon
- Мост Polygon для вывода и депозита через сети.
- Стейкинг Polygon: главный пункт назначения для стейкинга и получения вознаграждений с $MATIC
- и дашборд виджетов.

<img src={useBaseUrl("img/wallet/wallet-landing-page.png")} width="100%" height="100%"/>

Нажмите на кошелек Polygon или мост Polygon, и вы увидите остаток всех токенов в кошельке Polygon через мосты (PoS и Plasma).

<!-- <img src={useBaseUrl("img/wallet/wallet-one.png")} width="100%" height="100%"/> -->

## Внесение средств из Ethereum в Polygon {#depositing-funds-from-ethereum-to-polygon}

:::tip Видеоруководство

Вы можете следовать указаниям видеоруководства или этого пошагового руководства.

<video loop autoplay width="70%" height="70%" controls="true" >
  <source type="video/mp4" src="/img/wallet/depositMatic.mp4"></source>
  <p>Ваш браузер не поддерживает этот видео элемент.</p>
</video>
:::

### Пошаговое руководство {#step-by-step-guide}

Нажмите кнопку «Move Funds to Polygon Mainnet» (Переместить средства в Polygon Mainnet) или ссылку «Deposit» (Депозит) для любого типа токенов в разделе «Your tokens on Polygon Mainnet» (Ваши токены в Polygon Mainnet).
<img src={useBaseUrl("img/wallet/deposit-wallet.png")} width="100%" height="100%" />

Вы будете переадресованы на страницу моста, где вам нужно будет ввести сумму депозита.
<img src={useBaseUrl("img/wallet/bridge.png")} width="100%" height="100%"/>

Вы сможете увидеть выбранный тип моста в «Transfer Mode» (Режим трансфера). Вы можете изменить «Transfer Mode» (Режим трансфера), если хотите внести средства через определенный тип моста (PoS или Plasma).

:::note

**Режим трансфера** будет включен в зависимости от выбранного токена.

:::

После добавления суммы, которую вы хотите внести, вы можете нажать кнопку «Transfer» (Трансфер).

После нажатия на «Transfer» (Трансфер) вам нужно будет нажать кнопку «Continue» (Продолжить) во всплывающем окне «Important (Deposit Disclaimer)» (Важно (отказ от ответственности при депозите)).

<img src={useBaseUrl("img/wallet/Wallet-5.png")} width="50%" height="50%"/>

После нажатия кнопки «Continue» (Продолжить) вы увидите всплывающее окно «Transfer Overview» (Обзор трансфера) с информацией о приблизительном количестве газа, который потребуется для транзакции:

<img src={useBaseUrl("img/wallet/Wallet-6.png")} width="50%" height="50%" />

Нажмите кнопку «Continue» (Продолжить) во всплывающем окне «Transfer Overview» (Обзор трансфера), и вы увидите всплывающее окно, аналогичное тому, где вы можете посмотреть детали транзакции.

<img src={useBaseUrl("img/wallet/Wallet-7.png")} width="50%" height="50%" />

Нажмите кнопку «Continue» (Продолжить) во всплывающем окне «Confirm Transfer» (Подтвердить трансфер).

После нажатия кнопки «Continue» (Продолжить) вам нужно будет подтвердить все ваши транзакции в MetaMask, чтобы транзакция была успешной.

После подтверждения транзакции вы увидите всплывающее окно «Transfer in Progress» (Выполняется трансфер), где отображается статус депозита.
 Для отображения токенов в Polygon потребуется примерно 7-8 минут.

<img src={useBaseUrl("img/wallet/Wallet-8.png")} width="50%" height="50%"/>

Транзакция будет завершена после истечения требуемого периода времени.

<img src={useBaseUrl("img/wallet/Wallet-11.png")} width="50%" height="50%" />

:::note

Вы всегда сможете проверить прошлые транзакции, нажав на вкладку «Transactions» (Транзакции) слева.

:::

## Вывод средств из Polygon обратно в Ethereum через мост PoS {#withdrawing-funds-from-polygon-back-to-ethereum-on-pos-bridge}

:::tip Видеоруководство

Вы можете следовать указаниям видеоруководства или этого пошагового руководства.

<video loop autoplay width="70%" height="70%" controls="true" >
  <source type="video/mp4" src="/img/wallet/withdraw-POS.mp4"></source>
  <p>Ваш браузер не поддерживает этот видео элемент.</p>
</video>
:::

### Пошаговое руководство {#step-by-step-guide-1}

Вывод средств из Polygon обратно в Ethereum mainnet через мост PoS представляет собой простой процесс из 2 шагов. Для возврата средств в Ethereum потребуется около 3 часов. Для вывода средств следует нажать на ссылку «Withdraw» (Вывод) на любом токене PoS в разделе «Your tokens on Polygon Mainnet» (Ваши токены в Polygon Mainnet).

<img src={useBaseUrl("img/wallet/withdraw-POS-1.png")} width="100%" height="100%"/>

Вы будете переадресованы на страницу моста, где вам нужно будет ввести сумму для вывода.

<img src={useBaseUrl("img/wallet/withdraw-POS-2.png")} width="100%" height="100%" />

:::note

**Режим трансфера** будет включен в зависимости от выбранного токена.

:::

После добавления суммы, которую вы хотите вывести, вы можете нажать кнопку «Transfer» (Трансфер).

После нажатия на кнопку «Transfer» (Трансфер) вам нужно будет нажать кнопку «Continue» (Продолжить) во всплывающем окне «Important (Withdraw Disclaimer)» (Важно (отказ от ответственности при выводе)).

<img src={useBaseUrl("img/wallet/Wallet-14.png")} width="50%" height="50%" />

После нажатия кнопки «Continue» (Продолжить) вы увидите всплывающее окно «Transfer Overview» (Обзор трансфера) с информацией о приблизительном количестве газа, требуемого для транзакции.

<img src={useBaseUrl("img/wallet/Wallet-15.png")} width="50%" height="50%"/>

Нажмите кнопку «Continue» (Продолжить) во всплывающем окне «Transfer Overview» (Обзор трансфера), и вы увидите всплывающее окно, аналогичное тому, где вы могли посмотреть детали транзакции.

<img src={useBaseUrl("img/wallet/Wallet-16.png")}  width="50%" height="50%"/>

Нажмите кнопку «Continue» (Продолжить) во всплывающем окне «Transfer Overview» (Обзор трансфера).
 После нажатия кнопки «Continue» (Продолжить) вам нужно будет подтвердить транзакцию в MetaMask, чтобы она была успешной.
 После одобрения транзакции вы увидите на экране всплывающее окно:

<img src={useBaseUrl("img/wallet/Wallet-17.png")} width="50%" height="50%"/>

Первая транзакция предназначена для инициирования вывода.

Вам необходимо дождаться, пока не поступит checkpoint. Для этого может потребоваться до 3 часов.

<img src={useBaseUrl("img/wallet/Wallet-19.png")} width="50%" height="50%"/>

После поступления checkpoint вам нужно будет подтвердить вторую транзакцию.
 Когда вы подтвердите вторую транзакцию, вы получите средства обратно в Ethereum.

## Вывод средств из Polygon обратно в Ethereum через мост Plasma {#withdrawing-funds-from-polygon-back-to-ethereum-on-plasma-bridge}

:::tip Видеоруководство

Вы можете следовать указаниям видеоруководства или этого пошагового руководства.

<video loop autoplay width="70%" height="70%" controls="true" >
  <source type="video/mp4" src="/img/wallet/WithdrawMatic.mp4"></source>
  <p>Ваш браузер не поддерживает этот видео элемент.</p>
</video>
:::

Вывод средств из Polygon обратно в Ethereum mainnet с помощью моста Plasma представляет собой процесс из 3 шагов, однако здесь также используется период запроса.

Для вывода средств следует нажать ссылку «Withdraw» (Вывод) на любом токене типа Plasma в разделе «Your tokens on Polygon Mainnet» (Ваши токены в Polygon Mainnet).

<img src={useBaseUrl("img/wallet/withdraw-plasma-1.png")} width="100%" height="100%"/>

Вы будете переадресованы на страницу моста, где вам нужно будет ввести сумму для вывода.

<img src={useBaseUrl("img/wallet/withdraw-plasma-2.png")} width="100%" height="100%"/>

После добавления суммы, которую вы хотите вывести, вы можете нажать кнопку «Transfer» (Трансфер).
 После нажатия на кнопку «Transfer» (Трансфер) вам нужно будет нажать кнопку «Continue» (Продолжить) во всплывающем окне «Important (Withdraw Disclaimer)» (Важно (отказ от ответственности при выводе)).

<img src={useBaseUrl("img/wallet/Wallet-24.png")} width="50%" height="50%" />

После нажатия кнопки «Continue» (Продолжить) вы увидите всплывающее окно «Transfer Overview» (Обзор трансфера) с информацией о приблизительном количестве газа, требуемого для транзакции.

<img src={useBaseUrl("img/wallet/Wallet-25.png")} width="50%" height="50%"/>

Нажмите кнопку «Continue» (Продолжить) во всплывающем окне «Transfer Overview» (Обзор трансфера), и вы увидите всплывающее окно, аналогичное тому, где вы можете посмотреть детали транзакции.

<img src={useBaseUrl("img/wallet/Wallet-26.png")} width="50%" height="50%" />

Нажмите кнопку «Continue» (Продолжить) во всплывающем окне «Confirm Transfer» (Подтвердить трансфер).

Чтобы транзакция была успешно выполнена, вам нужно будет подтвердить все транзакции в кошельке MetaMask после того, как вы нажмете кнопку «Continue» (Продолжить). Это будет первая из 3 транзакций, которые нужно будет выполнить.

<img src={useBaseUrl("img/wallet/plasma-progress.png")} width="50%" height="50%"/>

Первая транзакция предназначена для инициирования вывода.
 После инициирования транзакции вывода необходимо дождаться, пока не поступит checkpoint. Для этого может потребоваться до 3 часов.

<img src={useBaseUrl("img/wallet/checkpoint-arrived.png")} width="50%" height="50%"/>


После поступления checkpoint вам нужно будет подтвердить новую транзакцию, чтобы начать 7-дневный период запроса.

<img src={useBaseUrl("img/wallet/challenge-completed.png")} width="50%" height="50%"/>

Чтобы получить средства обратно в Ethereum, вам нужно будет подтвердить транзакцию один последний раз.
 После подтверждения всех транзакций вы получите свои средства обратно в Ethereum.

<img src={useBaseUrl("img/wallet/transfer-completed.png")} width="50%" height="50%"/>

:::tip

Если у вас имеются вопросы, создайте запрос здесь: <ins>https://support.polygon.technology/support/home</ins>

:::
