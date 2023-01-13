---
id: wallet-bridge-faq
title: ওয়ালেট <> ব্রিজ FAQ-সমূহ
description: আপনার পরবর্তী ব্লকচেইন অ্যাপটি Polygon-এ তৈরি করুন।
keywords:
  - docs
  - matic
  - wallet
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## আমি কোথায় MATIC ওয়েব ওয়ালেটটি ব্যবহার করতে পারি? {#where-can-i-use-the-matic-web-wallet}
[https://wallet.polygon.technology/](https://wallet.polygon.technology/)

## আমি কীভাবে টোকেন চুক্তি খুঁজে পেতে পারি? {#how-do-i-find-the-token-contract}

 [কাস্টম টোকেন যোগ করা](../faq/adding-a-custom-token) নিবন্ধ দেখুন

## কোন ওয়ালেট বর্তমানে সমর্থিত? {#which-wallets-are-currently-supported}

- Metamask
- Coinbase ওয়ালেট
- ওয়ালেট কানেক্ট

আমরা শীঘ্রই আরো ওয়ালেট যোগ করা হবে।

## কিভাবে Plasma PoS থেকে আলাদা? {#how-is-plasma-different-from-pos}

Plasma-তে অতিরিক্ত নিরাপত্তা থাকে। 
দেখুন: [https://docs.polygon.technology/docs/develop/ethereum-polygon/getting-started](https://docs.polygon.technology/docs/develop/ethereum-polygon/getting-started)

## কোন টোকেন শুধুমাত্র Plasma-তে পাওয়া যায়? {#what-tokens-are-only-available-on-plasma}

Polygon টোকেন

## আমি কিভাবে Polygon ওয়ালেটে জমা করব এবং উইথড্র করব? {#how-do-i-deposit-to-polygon-wallet-and-also-withdraw}

এই ব্লগ ও ভিডিও জমা করা এবং উইথড্র শুরু করার জন্য একটি নিখুঁত নির্দেশনা:

ডকুমেন্টেশন: [https://docs.polygon.technology/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/#depositing-funds-from-ethereum-to-matic](https://docs.polygon.technology/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/#depositing-funds-from-ethereum-to-matic)

ভিডিও: [https://www.youtube.com/playlist?list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9](https://www.youtube.com/playlist?list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9)

## Metamask-এ Polygon মেইননেটে কিভাবে স্যুইচ করবেন? {#how-to-switch-to-polygon-mainnet-in-metamask}

ধরে নিচ্ছি যে আপনি আগে থেকেই আপনার Metamask ওয়ালেটে Polygon মেইননেটের জন্য নেটওয়ার্ক এবং কাস্টম RPC যোগ করেছেন এখানে আপনি কিভাবে স্যুইচ করতে পারেন:

1. আপনার Metamask ওয়ালেট খুলুন এবং চিত্রে দেখানো হিসাবে প্রসারিত করতে নেটওয়ার্ক ড্রপডাউনে ক্লিক করুন:

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-1.png")} width="30%" height="30%" />

1. একবার উইন্ডোটি প্রসারিত হলে আপনি স্যুইচ করতে Polygon মেইননেট নির্বাচন করতে পারেন:

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-2.png")} width="357" height="600" />

আপনি এখন Polygon মেইননেটে স্যুইচ করেছেন।

আপনি Metamask-এ কিভাবে নেটওয়ার্ক যুক্ত করবেন তার নির্দেশাবলী খুঁজছেন তাহলে আপনি এই লিঙ্কটি দেখতে পারেন: [https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/)

## Walletlink এ Polygon মেইননেট কিভাবে বেছে নেবেন? {#how-to-choose-polygon-mainnet-in-walletlink}

[এখানে](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-wallets#configure-polygon-on-walletlink) প্রদত্ত নির্দেশনা অনুসরণ করুন

## আমি WETH জমা করেছি কিন্তু আমি এটি Metamask-এ দেখতে পাচ্ছি না। আমি কী করব? {#i-have-deposited-weth-but-i-don-t-see-it-on-metamask-what-do-i-do}

আপনাকে ম্যানুয়ালি Metamask-এ WETH-এর কাস্টম টোকেন ঠিকানা যোগ করতে হবে।

Metamask খুলুন এবং **টোকেন ইম্পোর্ট করুন** ক্লিক করতে নিচে স্ক্রোল করুন।

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-3.png")} width="357" height="600" />


তারপরে, প্রাসঙ্গিক চুক্তির ঠিকানা, প্রতীক এবং দশমিক নির্ভুলতা যোগ করুন। চুক্তির ঠিকানা (এই ক্ষেত্রে PoS-WETH) এই লিঙ্কে পাওয়া যাবে: [https://docs.polygon.technology/docs/develop/network-details/mapped-tokens/](https://docs.polygon.technology/docs/develop/network-details/mapped-tokens/)। Polygon মেইননেটে ব্যালেন্স দেখতে আপনাকে চাইল্ড টোকেন ঠিকানা যোগ করতে হবে। WETH-এর জন্য নির্ভুলতার দশমিক 18 (সাধারণত, বেশিরভাগ টোকেনের ক্ষেত্রে নির্ভুলতার দশমিক 18)।

একবার আপনি সমস্ত ক্ষেত্র পূরণ করলে, আপনি **কাস্টম টোকেন যোগ করুন** এ ক্লিক করতে পারেন এবং আপনার টোকেন যোগ করা হবে।

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-4.png")} width="357" height="600" />


## আমি কি আমার টোকেন Polygon থেকে অন্য কোনো ওয়ালেট/এক্সচেঞ্জে পাঠাতে পারি? {#can-i-send-my-tokens-from-polygon-to-any-other-wallet-exchange}

আপনি Polygon UI থেকে এক্সচেঞ্জ/ওয়ালেটে সরাসরি টোকেন পাঠাতে পারবেন না। আপনাকে প্রথমে Polygon থেকে Ethereum-এ উইথড্র করতে হবে এবং তারপর আপনার এক্সচেঞ্জ ঠিকানায় পাঠাতে হবে (যদি না আপনার এক্সচেঞ্জ/ওয়ালেট স্পষ্টভাবে নেটওয়ার্ক সমর্থন করে)।

## আমি সরাসরি একটি এক্সচেঞ্জ/ওয়ালেটে ফান্ড পাঠাতে ভুল করেছি। আপনি কি সাহায্য করতে পারেন? {#i-made-a-mistake-of-sending-funds-to-an-exchange-wallet-directly-can-you-help}

দুর্ভাগ্যবশত, আমরা এই ধরনের ক্ষেত্রে সহায়তা করতে পারি না। শুধুমাত্র Ethereum সমর্থন করে এমন এক্সচেঞ্জগুলিতে সরাসরি ফান্ড পাঠাবেন না, আপনাকে প্রথমে Polygon থেকে Ethereum-এ উইথড্র করতে হবে এবং তারপর আপনার এক্সচেঞ্জ ঠিকানায় পাঠাতে হবে।

## আমার লেনদেন অনেক দিন ধরে মুলতুবি আছে, আমি কী করতে পারি? {#my-transaction-is-pending-for-too-long-what-can-i-do}

লেনদেন জমা দেওয়ার সময় কম গ্যাসের দাম সেট করার কারণে ব্লকচেইনে লেনদেন বাদ দেওয়া হতে পারে। Ethereum-এ ভিড়ের কারণে গ্যাসের দাম হঠাৎ বেড়ে গেলে সেগুলিও বাদ দেওয়া হতে পারে। আরেকটি সম্ভাবনা হল আপনি হয়তো আপনার ওয়ালেট থেকে লেনদেনটি বাতিল করেছেন বা লেনদেনটি পরিবর্তন করেছেন। এই সমস্ত ক্ষেত্রে, ওয়ালেট ওয়েব আপনাকে প্রগ্রেস মেসেজে লেনদেন দেখাবে এবং এটি আপনাকে আরও অপেক্ষা করতে বাধ্য করবে৷

আপনার লেনদেন এক ঘণ্টার বেশি আটকে থাকলে, একটি "আবার চেষ্টা করুন" বোতাম দেখানো হবে। এটি ভালো, এর অর্থ হলো আপনি নেটওয়ার্ককে আপনার জন্য লেনদেনটি পুনরায় চেষ্টা করার জন্য অনুরোধ করতে পারেন৷ আপনি এরপর যা করতে পারেন তা হলো একই লেনদেন পুনরায় চেষ্টা করতে "আবার চেষ্টা করুন" বোতামে ক্লিক করুন৷ যদি আপনার জমা করা লেনদেন আটকে থাকে, তাহলে আপনার জমা করা প্রক্রিয়া পুনরায় শুরু করা হবে এবং যদি আপনার উইথড্র করা লেনদেন আটকে থাকে, আপনি শেষ যে ধাপটি সফলভাবে সম্পন্ন করেছেন সেখান থেকে আপনি আপনার উইথড্র করা চালিয়ে যেতে পারবেন।

আপনি যদি "আবার চেষ্টা করুন" বোতামটি নিয়ে এগিয়ে যেতে সমস্যার সম্মুখীন হন এবং আপনি MetaMask ওয়ালেট ব্যবহার করছেন, তাহলে আপনার MetaMask-এর কার্যকলাপ বিভাগে প্রচুর সারিবদ্ধ লেনদেন আটকে আছে কিনা তা আপনাকে পরীক্ষা করতে হতে পারে। এই ক্ষেত্রে, MetaMask ওয়ালেট পুনরায় ইনস্টল করা এবং তারপরে আপনার লেনদেনের সাথে এগিয়ে যাওয়া সহায়ক হতে পারে। এছাড়াও, আপনি একটি পৃথক ব্রাউজার থেকে লেনদেন শুরু করার চেষ্টা করতে পারেন।

নিচের ভিডিওটি দেখলে "আবার চেষ্টা করুন" বৈশিষ্ট্যটি কিভাবে ব্যবহার করবেন সে সম্পর্কে আরও স্পষ্টতা দিতে পারে৷

[https://youtu.be/0b4yjR_naEQ](https://youtu.be/0b4yjR_naEQ)

## Polygon সমর্থিত এক্সচেঞ্জের তালিকা কী কী? {#what-are-the-list-of-supported-exchanges-on-polygon}

নিচে সেন্ট্রালাইজড এক্সচেঞ্জের তালিকা রয়েছে যা বর্তমানে Polygon-কে সমর্থন করে এবং এছাড়াও এমন সব টোকেন এইসব এক্সচেঞ্জ সমর্থন করে।

AscendEX - USDC, EASY, MATIC

MXC - MATIC, QUICK, PlotX, Dfyn

Okcoin - ETH, USDT, LINK, MKR, USDC, DAI, USDK, COMP, YFI, SNX, YFII, ও UNI। (টোকেন শুধুমাত্র Okcoin থেকে Polygon চেইনে সরানো যেতে পারে। Polygon থেকে Okcoin টোকেন ট্রান্সফার করা বর্তমানে সমর্থিত নয়)

Okex - BAL, BAT, CEL, COMP, CRV, DAI, ETH, GHST, GUSD, LINK, MKR, PAX, SNX, SUSHI, TUSD, UNI, USDC-ERC20, USDT-ERC20, USDK, wBTC, YFI, YFII, ZRX ( টোকেনগুলি শুধুমাত্র Okex থেকে Polygon চেইনে সরানো যেতে পারে৷ Polygon থেকে Okex টোকেন ট্রান্সফার করা বর্তমানে সমর্থিত নয়)

Bitforex - MATIC

উপরের তালিকায় স্পষ্টভাবে উল্লেখ করা হয়নি এমন অন্য কোনো এক্সচেঞ্জে টোকেন পাঠালে ফান্ডের ক্ষতি হতে পারে। আপনি যদি Polygon সমর্থন করে না এমন কোনো এক্সচেঞ্জে ফান্ড উইথড্র করতে চান, তাহলে আপনাকে প্রথমে Ethereum-এ টোকেন উইথড্র করতে হবে এবং তারপর আপনার Ethereum ওয়ালেট ব্যবহার করে এক্সচেঞ্জে পাঠাতে হবে। এই ভিডিওটি দেখায় কিভাবে Polygon থেকে Ethereum এ ফান্ড উইথড্র করা যায় - [https://www.youtube.com/watch?v=DgpHY95qrbQ&list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9&index=5](https://www.youtube.com/watch?v=DgpHY95qrbQ&list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9&index=5)

এছাড়াও আপনি এই নির্দেশনা [এখান](https://docs.matic.today/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/) থেকে অনুসরণ করতে পারেন।

## আমি লগ ইন করতে পারছি না, আমি কী করব? {#i-am-not-able-to-login-what-do-i-do}

[https://docs.polygon.technology/docs/validate/delegator-faq/#my-metamask-is-stuck-at-confirming-after-login-what-do-i-do-or-nothing-happens-when-i-try-to-login](https://docs.polygon.technology/docs/validate/delegator-faq/#my-metamask-is-stuck-at-confirming-after-login-what-do-i-do-or-nothing-happens-when-i-try-to-login)

## Polygon কি হার্ডওয়্যার ওয়ালেট সমর্থন করে? {#does-polygon-support-hardware-wallets}
হ্যাঁ, হার্ডওয়্যার ওয়ালেট সমর্থিত।

## আমি আমার Polygon ওয়ালেট দিয়ে কী করতে পারি? {#what-can-i-do-with-my-polygon-wallet}

- Polygon-এ যেকোনো অ্যাকাউন্টে ফান্ড পাঠান।
- Ethereum থেকে Polygon-এ ফান্ড জমা করুন (ব্রিজ ব্যবহার করে)।
- Polygon থেকে Ethereum-এ ফান্ড উইথড্র করুন (ব্রিজ ব্যবহার করে)।

## আমার টোকেন তালিকায় দেখাচ্ছে না। আমি কার সাথে যোগাযোগ করতে পারি? {#my-token-is-not-visible-in-the-list-who-should-i-contact}

ডিসকর্ড বা টেলিগ্রামে Polygon টিমের সাথে যোগাযোগ করুন এবং আপনার টোকেন তালিকাভুক্ত করুন। এটি করার আগে আপনার টোকেন ম্যাপ করা আছে কিনা দেখে নিন। যদি এটি ম্যাপ করা না হয়, তাহলে [https://mapper.polygon.technology/ ](https://mapper.polygon.technology/)-এ অনুগ্রহ করে একটি অনুরোধ করুন

## অনুসরণ করার জন্য কিছু সেরা অনুশীলন কী? {#what-are-some-best-practices-to-follow}

- আপনি যখন Polygon থেকে Ethereum-এ ফান্ড পাঠাতে চান, তাহলে উইথড্র্র করা কার্যকারিতা ব্যবহার করুন। পাঠানোর কার্যকারিতা ব্যবহার করবেন না। এর ফলে ফান্ডের ক্ষতি হতে পারে।
- আপনি শুধুমাত্র স্ট্যাক করতে অংশগ্রহণ করতে চাইলে Polygon মেইননেটে জমা করবেন না।
- MetaMask থেকে গ্যাসের লিমিট পরিবর্তন করবেন না।

## জমা করা নিশ্চিত হলেও ব্যালেন্স আপডেট না হলে আমি কী করব? {#what-do-i-do-if-the-deposit-is-confirmed-but-the-balance-is-not-getting-updated}

জমা করা লেনদেনের জন্য 22-30 মিনিট সময় লাগতে পারে। কিছু সময় অপেক্ষা করুন এবং "ব্যালেন্স রিফ্রেশ করুন" এ ক্লিক করুন।

## চেকপয়েন্টটি না ঠিক হলে আমার কী করা উচিত? {#what-should-i-do-if-the-checkpoint-is-not-happening}

Ethereum-এ নেটওয়ার্ক কনজেশনের ভিত্তিতে চেকপয়েন্টগুলি কখনও কখনও 45 মিনিট থেকে 1 ঘণ্টার বেশি সময় নেয়, আমরা টিকিট খোলার আগে কিছুক্ষণ অপেক্ষা করার পরামর্শ দিই।

## উইথড্র্র করা লেনদেন বাতিল করা সম্ভব? {#is-it-possible-to-cancel-a-withdraw-transaction}

না, আপনাকে পরবর্তী পদক্ষেপ সম্পূর্ণ করতে হবে। যদি বর্তমানে গ্যাসের দাম খুব বেশি হয়, তাহলে অনুগ্রহ করে অপেক্ষা করুন এবং দাম কমলে পরে চেষ্টা করুন।

## কেন MATIC টোকেন PoS-এ সমর্থিত নয়? {#why-is-the-matic-token-is-not-supported-on-pos}

MATIC হলো Polygon-এর নেটিভ টোকেন এবং এটির একটি চুক্তির ঠিকানা রয়েছে - Polygon চেইনে 0x000000000000000000000000000000000000000000000001010 আছে। এটি গ্যাসের পেমেন্ট করতেও ব্যবহৃত হয়। PoS ব্রিজে MATIC টোকেন ম্যাপ করার ফলে MATIC-এর Polygon চেইনে একটি অতিরিক্ত চুক্তির ঠিকানা থাকবে। এটি আগে থেকে থাকা চুক্তির ঠিকানার থেকে আলাদা হবে কারণ এই নতুন টোকেন ঠিকানাটি গ্যাসের জন্য অর্থ প্রদানের জন্য ব্যবহার করা যাবে না এবং Polygon চেইনে একটি সাধারণ ERC20 টোকেন হিসাবে থাকতে হবে। তাই এই বিভ্রান্তি এড়াতে এটি শুধুমাত্র Plasma-তে MATIC বজায় রাখার সিদ্ধান্ত নিয়েছে।

## আমি কিভাবে টোকেন ম্যাপ করব? {#how-do-i-map-tokens}

ম্যাপ করার অনুরোধ [https://mapper.polygon.technology/](https://mapper.polygon.technology/)-এ জানান

## লেনদেন খুব বেশি সময় নিলে বা গ্যাসের দাম খুব বেশি হলে আমি কী করব? {#what-do-i-do-if-the-transaction-is-taking-too-long-or-if-the-gas-price-is-too-high}

নেটওয়ার্ক কনজেশনের উপর ভিত্তি করে লেনদেনের সময় এবং গ্যাসের দাম পরিবর্তিত হয়। যদি উচ্চ গ্যাসের মূল্য পরিশোধ করা হয়, তাহলে লেনদেন দ্রুত নিশ্চিত হয়।

## আমি কি গ্যাসের সীমা বা গ্যাসের দাম পরিবর্তন করতে পারি? {#can-i-change-the-gas-limit-or-the-gas-price}

চুক্তিতে কল করা ফাংশনের নির্দিষ্ট প্রয়োজনীয়তা অনুসারে গ্যাসের সীমা অনুমান করা হয় এবং অ্যাপ্লিকেশন দ্বারা সেট করা হয়। এটি সম্পাদনা করা ঠিক হবে না। লেনদেন ফি বাড়ানো বা কমানোর জন্য শুধুমাত্র গ্যাসের দাম পরিবর্তন করা যেতে পারে।

## লেনদেন বাতিল হয়ে গেলেও ওয়েব ওয়ালেট লেনদেন সম্পূর্ণ হয়েছে দেখালে আমার কী করা উচিত? {#what-should-i-do-if-the-transaction-was-cancelled-but-the-web-wallet-shows-transaction-is-completed}

আমাদের সাহায্যকারী টিমের সাথে যোগাযোগ করুন।

## আমি কোথা থেকে সাহায্যের জন্য অনুরোধ করব? {#where-do-i-raise-a-support-ticket}
https://support.polygon.technology/support/home

## আমি যে পরিমাণ টাকা উইথড্র্র করতে চাই তার থেকে গ্যাসের দাম বেশি। {#the-gas-price-is-more-than-the-amount-i-seek-to-withdraw}

Plasma ব্রিজের সাথে একটি উইথড্র্র করা লেনদেন 3টি ধাপে বিভক্ত, একটি যা Polygon মেইননেটে হয় এবং দুটি ধাপ যা Ethereum মেইননেটে সম্পন্ন করা হয়। PoS ব্রিজে, উইথড্র্র করা লেনদেন দুইটি ধাপে ঘটে: Polygon নেটওয়ার্কে টোকেন বার্ন করা এবং Ethereum নেটওয়ার্কে প্রুফ জমা দেওয়া। Polygon মেইননেটে, চার্জ খুবই কম এবং আপনি যে লেনদেন খরচ দেখতে পাচ্ছেন তার সিংহ ভাগ হলো Ethereum মাইনার দ্বারা নিয়ন্ত্রিত Ethereum নেটওয়ার্কে গ্যাসের দাম৷ যেমনটি আশা করা যায়, এই চার্জটি আমাদের নিয়ন্ত্রণের বাইরে, এবং দামের উপর আমাদের খুব বেশি প্রভাব নেই। যদি আপনার টোকেন বার্ন করা হয়, তাহলে আপনাকে উইথড্র্র করার প্রক্রিয়া করতে হবে, তবে আমরা প্রক্রিয়া বিপরীত করতে পারি না।


## আমি কি নিজের উইথড্র্র করা লেনদেন বাতিল করতে পারি? {#can-i-cancel-my-withdrawal-transaction}

দুর্ভাগ্যবশত, প্রক্রিয়াটি শুরু হলে এবং টোকেন বার্ন হয়ে গেলে Polygon উইথড্র্র করা বাতিল করতে পারে না। একটি বার্ন হ্যাশ তৈরি করা হয় এবং লেনদেনের পরবর্তী পর্যায়ে অবিলম্বে আসে। যদি বার্ন লেনদেন এখনও মুলতুবি থাকে, আপনি নিম্নলিখিত নির্দেশনার মাধ্যমে একটি বাতিলকরণের সুবিধা দিতে পারেন

[Metamask](https://metamask.zendesk.com/hc/en-us/articles/360015489251-How-to-Speed-Up-or-Cancel-a-Pending-Transaction) <br />
[Walletlink](https://www.techdreams.org/crypto-currency/how-to-cancel-a-pending-ethereum-transaction-on-coinbase-wallet/10159-20210412)


## আমার লেনদেন আটকে গেছে। {#my-transaction-is-stuck}

আমরা কিছু সাধারণ ত্রুটির তালিকা করেছি যা ইউজাররা সম্মুখীন হতে পারেন৷ আপনি ত্রুটির ছবির নিচে সমাধানটি খুঁজে পেতে পারেন। যদি আপনাকে একটি ভিন্ন ত্রুটি দেখানো হয়, অনুগ্রহ করে আমাদের সমস্যা সমাধানের টিমের সাথে [সাপোর্ট টিকিটের অনুরোধ করুন।](https://support.polygon.technology/support/home)

  - ### সাধারণ ত্রুটি {#common-errors}
ক। উইথড্র্র করা প্রাথমিক পর্যায়ে আটকে গেছে।

    <img src={useBaseUrl("img/wallet-bridge/plasma-progress-stuck.png")} width="357" height="800"/>

    এটি সাধারণত ঘটে যখন লেনদেন প্রতিস্থাপিত হয় এবং ওয়ালেট ওয়েব অ্যাপ্লিকেশন প্রতিস্থাপিত লেনদেন হ্যাশ শনাক্ত করতে সক্ষম হয় না। নির্দেশাবলী অনুসরণ করুন [https://withdraw.polygon.technology/](https://withdraw.polygon.technology/) এবং আপনার উইথড্র্র করা সম্পূর্ণ করুন।

খ। RPC ত্রুটি

    <img src={useBaseUrl("img/wallet-bridge/checkpoint-rpc-error.png")} width="357" height="600"/>

    আপনি যে বর্তমানে RPC ত্রুটি সম্মুখীন হন তা একটি RPC ওভারলোডের কারণে হতে পারে।

    অনুগ্রহ করে আপনার RPC পরিবর্তন করার চেষ্টা করুন এবং লেনদেন করা এগিয়ে যান। আপনি আরো তথ্যের জন্য এই লিঙ্কটি [এখানে](https://docs.polygon.technology/docs/develop/network-details/network#matic-mainnet) অনুসরণ করতে পারেন।

  গ.

  <img src={useBaseUrl("img/wallet-bridge/checkpoint-stumbled-error.png")} width="357" height="600"/>

  এটি সাধারণত একটি মাঝেমধ্যে ঘটা ত্রুটি যা স্বয়ংক্রিয়ভাবে সমাধান হয়ে যায়। যদি আপনি এখনও একই ত্রুটি পেয়ে থাকেন যখন পদক্ষেপ পুনরায় আরম্ভ করা, এটি আরও সমস্যার জন্য সমস্ত প্রাসঙ্গিক তথ্যের সাথে [সাপোর্ট করার অনুরোধ করার টিকিট ](https://support.polygon.technology/)-এর আর্জি জানান।

## আমি Polygon ওয়ালেট থেকে সরাসরি এক্সচেঞ্জ/ওয়ালেটে ফান্ড পাঠানোর সময় ভুল করেছি। আপনি কি সাহায্য করতে পারেন? {#i-made-the-mistake-of-sending-funds-to-an-exchange-wallet-directly-from-polygon-wallet-can-you-help}

দুঃখজনক, আমরা আপনাকে অবহিত করার জন্য দুঃখিত যে আপনি যদি Polygon নেটওয়ার্ক থেকে কোনো অসমর্থিত এক্সচেঞ্জ/ওয়ালেটে টোকেন পাঠিয়ে থাকেন তাহলে আমরা হয়তো সাহায্য করতে পারব না।

এই ক্ষেত্রে একটি এক্সচেঞ্জের কী করতে হবে তা এখানে (যদিও নিশ্চিত না যে এটি চালাতে সাহায্যকারী আধিকারিকদের কতটা নমনীয়তা আছে)। অনুমান করা এক্সচেঞ্জ সাপোর্ট এক্সিকিউটিভ অ্যাকাউন্টের প্রাইভেট কী অ্যাক্সেস করেছে, তারা Polygon থেকে তাদের অ্যাকাউন্ট থেকে আপনার (ব্যবহারকারীর) Polygon ঠিকানায় ফান্ড ট্রান্সফার করতে পারে।

এটি মনে রাখা গুরুত্বপূর্ণ, আপনাকে শুধুমাত্র Ethereum সমর্থন করে এমন এক্সচেঞ্জগুলিতে সরাসরি ফান্ড পাঠাতে হবে না। সঠিক পদ্ধতি হলো আপনাকে প্রথমে Polygon থেকে Ethereum-এ উইথড্র করতে হবে এবং তারপর আপনার এক্সচেঞ্জ ঠিকানায় এটি পাঠান।

## আমি একটি অপর্যাপ্ত ব্যালেন্স ত্রুটি দেখি। {#i-m-shown-an-insufficient-balance-error}

Polygon নেটওয়ার্কে উইথড্র করা এবং জমা করা সস্তা। বোঝা উচিত যে Ethereum মেইননেটে কিছু ETH ব্যালেন্স পেয়ে অপর্যাপ্ত ব্যালেন্স ত্রুটি দূর করা যেতে পারে। এটি সাধারণত একটি অপর্যাপ্ত ব্যালেন্সের সমস্যা দূর করে।

যদি এটি Polygon মেইননেটে একটি লেনদেন হয়, তাহলে আমাদের প্রয়োজন হবে যে আপনার পর্যাপ্ত পরিমাণে MATIC টোকেন রয়েছে।

## আমি কিভাবে চেইন জুড়ে সম্পদ ব্রিজ করব? {#how-do-i-bridge-assets-across-chains}

[https://wallet.polygon.technology/bridge/](https://wallet.polygon.technology/bridge/) (ETH <-> Polygon) <br/>
[https://xpollinate.io/](https://xpollinate.io/) (BSC <-> Polygon <-> xDai) <br/>
[https://exchange.chainswap.com/](https://exchange.chainswap.com/) (ETH <-> Polygon/BSC) <br/>
[https://anyswap.exchange/bridge](https://anyswap.exchange/bridge) (ETH <-> Polygon <-> BSC/xDai) <br/>
[https://app.0.exchange/#/home](https://app.0.exchange/#/home)(ETH <-> Polygon <-> Avalanche <-> BSC)

যোগ করার জন্য, আমরা কোনো এক্সটার্নাল পরিষেবা সমর্থন করি না, দয়া করে আপনার নিজের গবেষণা সবসময় নিশ্চিত করুন

## আমি ভুল ঠিকানায় একটি ট্রান্সফার করেছি। আমি কিভাবে ফান্ড পুনরুদ্ধার করব? {#i-made-a-transfer-to-the-wrong-address-how-do-i-retrieve-the-funds}

দুর্ভাগ্যবশত, কিছুই করা যাবে না। শুধুমাত্র সেই নির্দিষ্ট ঠিকানায় ব্যক্তিগত কীগুলির মালিক সেই এসেটগুলি সরাতে পারে৷


## আমার লেনদেন এক্সপ্লোরারের উপর দৃশ্যমান হয় না। আমি কী করব? {#my-transactions-are-not-visible-on-the-explorer-what-should-i-do}

এটি সম্ভবত Polygonscan সহ একটি সূচি সমস্যা। বিশদে জানতে [সাপোর্ট টিমের](https://support.polygon.technology/support/home) সাথে যোগাযোগ করুন।
আপনি এই ব্লক এক্সপ্লোরার ব্যবহার করতে পারেন

[https://polygon-explorer-mainnet.chainstacklabs.com](https://polygon-explorer-mainnet.chainstacklabs.com/) <br />
[https://explorer-mainnet.maticvigil.com](https://explorer-mainnet.maticvigil.com/) <br />
[https://explorer.matic.network](https://explorer.matic.network/) <br />
[https://backup-explorer.matic.network](https://backup-explorer.matic.network/)


## আমি Ethereum এ একটি জমা করা শুরু করেছি কিন্তু এটি এখনও মুলতুবি হিসাবে দেখায়৷ আমি কী করব? {#i-initiated-a-deposit-on-ethereum-but-it-still-shows-as-pending-what-should-i-do}

আপনার সরবরাহ করা গ্যাস সম্ভবত খুব কম। আপনার কিছুক্ষণ অপেক্ষা করা উচিত এবং লেনদেনটি পুনরায় করা উচিত যদি এটি মাইন না হয়। অতিরিক্ত সাহায্যের ক্ষেত্রে, অনুগ্রহ করে আপনার ওয়ালেট ঠিকানা, লেনদেন হ্যাশ (যদি থাকে) এবং প্রাসঙ্গিক স্ক্রিনশট সহ [সাপোর্ট টিম](https://support.polygon.technology/support/home)-এর সাথে যোগাযোগ করুন।


## OpenSea বা Polygon ব্রিজ ব্যবহার করে এমন অন্য কোনো অ্যাপ্লিকেশনের সাথে আমার একটি টোকেন উইথড্র করার সমস্যা রয়েছে। {#i-have-a-token-withdrawal-issue-with-opensea-or-any-other-application-which-uses-polygon-bridge}

যদি আপনার উইথড্র করার লেনদেন আটকে থাকার একটি সমস্যা থাকে, তাহলে Polygon-এ আপনার বার্ন হ্যাশ থাকলে আপনাকে সাহায্য করার জন্য https://polygon-withdraw.matic.network/ এর সাথে উইথড্র করার ব্রিজ প্রদান করে। এই টুলের সাহায্যে, আপনি দ্রুত অনবোর্ড হয়ে গেছেন এবং সমস্যাটি সমাধান করা হবে। OpenSea এবং অন্যান্য dApps এর সাথে আপনার লেনদেনের বিষয়ে অন্যান্য প্রশ্ন অবশ্যই অ্যাপ্লিকেশনের টিমের দ্বারা পরিচালনা করা হবে।


## আমি কোথায় সরাসরি MATIC টোকেন পেতে পারি? {#where-can-i-get-matic-tokens-directly}

তাই MATIC টোকেন যেকোনো সেন্ট্রালাইজড ([Binance](https://www.binance.com/en), [Coinbase](https://www.coinbase.com/), ইত্যাদি) বা ডিসেন্ট্রালাইজড ([Uniswap](https://uniswap.org/), [QuickSwap](https://quickswap.exchange/#/swap)) এক্সচেঞ্জ থেকে কেনা যাবে। আপনি গবেষণা করতে পারেন এবং [Transak](https://transak.com/), [Ramp](https://ramp.network/) এর মতো কিছু অন-র‍্যাম্প ব্যবহার করতে পারেন।
আপনার MATIC কয়েন কেনার উদ্দেশ্যটিও নির্ধারণ করা উচিত যে আপনি সেগুলি কোথা থেকে এবং কোন নেটওয়ার্ক কিনবেন। আপনার অভিপ্রায় স্ট্যাকিং বা প্রতিনিধিত্বের ক্ষেত্রে Ethereum Main-net MATIC থাকা যুক্তিযুক্ত। আপনার অভিপ্রায় যদি Polygon মেইননেটে একটি লেনদেন হয়, তাহলে আপনাকে Polygon মেইননেটে MATIC হোল্ড করা এবং লেনদেন করা উচিত।


## আমি লেনদেন হ্যাশ পাচ্ছি না এবং আমার জমা হচ্ছে না? কী হচ্ছে? {#i-m-not-getting-a-transaction-hash-and-my-deposits-aren-t-going-through-what-is-happening}

আপনার সম্ভবত পূর্বের মুলতুবি লেনদেন রয়েছে, অনুগ্রহ করে প্রথমে বাতিল করুন বা তাদের গতি করুন। Ethereum-এ লেনদেন একের পর এক ঘটতে পারে।


## এটি দেখায় Polygon-এ উইথড্র করার জন্য কোনো চার্জ করে না, কিন্তু আমরা লেনদেনের সময় অর্থ প্রদান করতে পারি। {#it-shows-polygon-does-not-charge-any-amount-for-a-withdrawal-but-we-are-to-pay-during-the-transaction}

Plasma ব্রিজের সাথে একটি উইথড্র্র করা লেনদেন 3টি ধাপে বিভক্ত, একটি যা Polygon মেইননেটে হয় এবং দুটি ধাপ যা Ethereum মেইননেটে সম্পন্ন করা হয়। PoS ব্রিজে, উইথড্র্র করা লেনদেন দুইটি ধাপে ঘটে: Polygon নেটওয়ার্কে টোকেন বার্ন করা এবং Ethereum নেটওয়ার্কে প্রুফ জমা দেওয়া। প্রতিটি ক্ষেত্রে, Polygon মেইননেটে ঘটতে থাকা টোকেন বার্ন করার জন্য খুব কম খরচ হবে। Ethereum মেইননেটে ঘটতে থাকা অবশিষ্ট পদক্ষেপগুলি বর্তমান গ্যাসের মূল্যের উপর নির্ভর করে ETH-এ পেমেন্ট করতে হবে যা [এখান](https://ethgasstation.info/) থেকে যাচাই করা যেতে পারে।


## আমি কিভাবে Polygon নেটওয়ার্কে স্থাপন করা প্রধান অ্যাপ্লিকেশনগুলির সাথে যোগাযোগ করব? {#how-do-i-contact-major-applications-deployed-on-the-polygon-network}

Curve  [https://discord.gg/JnUFrsDF](https://discord.gg/JnUFrsDF) <br />
SushiSwap  [https://discord.gg/ApbE4Eau](https://discord.gg/ApbE4Eau) <br />
CREAM  [https://discord.gg/js8JpmFB](https://discord.gg/js8JpmFB) <br />
AAVE  [https://discord.gg/YYtp7N5d](https://discord.gg/YYtp7N5d) <br />
FuruCombo  [https://discord.gg/wJJ7PXAd](https://discord.gg/wJJ7PXAd) <br />
QuickSwap  [http://t.me/QuickSwapDEX](http://t.me/QuickSwapDEX) <br />

Beefy Finance - [https://discord.gg/egkEEAkC](https://discord.gg/egkEEAkC)


## Polygon নেটওয়ার্কে সমর্থিত হার্ডওয়্যার ওয়ালেট তালিকা। {#list-of-hardware-wallets-supported-on-polygon-network}

তাই Polygon নেটওয়ার্ক MetaMask এর সাথে সামঞ্জস্যপূর্ণ সমস্ত হার্ডওয়্যার ওয়ালেট সমর্থন করবে। MetaMask সম্পর্কে আরও জানতে এই [লিঙ্ক](https://metamask.zendesk.com/hc/en-us/articles/360020394612-How-to-connect-a-Trezor-or-Ledger-Hardware-Wallet) অনুসরণ করুন।


## আমাকে প্রতারণা করা হয়েছে। আমি কিভাবে আমার টোকেন পুনরুদ্ধার করব? {#i-have-been-scammed-how-will-i-retrieve-my-tokens}

দুর্ভাগ্যবশত, হারিয়ে যাওয়া কয়েনের কোনো পুনরুদ্ধার প্রক্রিয়া নেই। আমরা পরামর্শ দেই যে কোনো লেনদেন করার আগে আপনি চেক করুন এবং শুরু করার আগে ও সম্পন্ন করার সময় দুই বার চেক করুন। অনুগ্রহ করে মনে রাখবেন যে Polygon নেটওয়ার্ক এবং আমাদের অফিসিয়াল হ্যান্ডেল কোনো উপহার দেওয়া পোস্ট বা টোকেন দ্বিগুণ করার সাথে জড়িত নয় এবং আমরা কখনোই সংস্থার পক্ষ থেকে আপনার সাথে যোগাযোগ করব না। অনুগ্রহ করে সব প্রচেষ্টা বাদ দিন কারণ তারা সম্ভবত স্ক্যাম হয়ে থাকে। আমাদের সমস্ত যোগাযোগের মাধ্যম অফিসিয়াল
হ্যান্ডেল।


## তাই Ethereum Goerli এর টেস্ট নেটওয়ার্ক হিসেবে রয়েছে। Polygon নেটওয়ার্কের কি টেস্ট নেটওয়ার্ক রয়েছে। {#so-ethereum-has-goerli-as-its-test-network-does-polygon-network-have-a-test-network}

তাই Ethereum নেটওয়ার্ক Goerli এর টেস্ট নেটওয়ার্ক হিসেবে রয়েছে, Polygon মেইননেট মুম্বাই এ রয়েছে। এই টেস্ট নেটওয়ার্কে সমস্ত লেনদেন মুম্বাই এক্সপ্লোরার এ ইনডেক্স করা হবে।


## MetaMask এ আমার লেনদেনের গতি কিভাবে বৃদ্ধি করা যায়। {#how-can-speed-up-my-transaction-on-metamask}

MetaMask এর মাধ্যমে লেনদেন দ্রুত করার জন্য, অনুগ্রহ করে এই [লিঙ্কে](https://metamask.zendesk.com/hc/en-us/articles/360015489251-How-to-Speed-Up-or-Cancel-a-Pending-Transaction) যান।


## আমার টিকিট তৈরি করার সময় আমার কী সব তথ্য প্রদান করতে হবে? {#what-all-information-should-i-provide-when-i-create-a-ticket}

- ওয়ালেটের ঠিকানা
- লেনদেন হ্যাশ
- সঠিক পদক্ষেপের উদ্দেশ্য এবং ফলাফল, খুব বর্ণনামূলক
- স্ক্রিনশট বা পদক্ষেপের স্ক্রিন রেকর্ডিং

## আমি একটি জমা করার চেষ্টা করছিলাম কিন্তু লেনদেন অনুমোদন ধাপে বন্ধ হয়ে গেছে। {#i-was-trying-to-make-a-deposit-but-the-transaction-stopped-at-the-approve-step}

যদি লেনদেন এখনও **অনুমোদন** ধাপে থাকে তাহলে এটি এখনও সম্পূর্ণ হয়নি। এটি পূরণ করার জন্য, আপনাকে গ্যাসের ফি দিতে হবে এবং তারপরে এটি হয়ে যাবে।

## আমার উইথড্র করার লেনদেনের জন্য গ্যাসের ফি খুবই বেশি। {#the-gas-fee-for-my-withdrawal-transaction-is-too-high}

Polygon নেটওয়ার্কে গ্যাসের ফি সবসময় খুব কম, কিন্তু আমরা Ethereum মেইননেটের ফির জন্য একই বলতে পারি না।
যদি আপনি লেনদেন শুরু করেছেন, তবে এটি বাতিল করা উচিত নয়। পরিবর্তে, আপনি গ্যাসের ফি কম করার জন্য অপেক্ষা করতে পারেন বা আপনার অ্যাকাউন্টে আরও ETH যোগ করতে পারেন।

## আমার ওয়ালেটে কিছু অনুমোদিত নয় এমন লেনদেন রয়েছে। আমার ওয়ালেট কি হ্যাক হয়েছে? {#there-are-some-unauthorized-transactions-in-my-wallet-is-my-wallet-hacked}

দুর্ভাগ্যবশত, নেটওয়ার্ক অপ্রয়োজনীয় লেনদেন ফিরিয়ে দিতে পারে না।
আপনার ব্যক্তিগত কী-এর বিষয়ে সাবধান হওয়া গুরুত্বপূর্ণ এবং **এটি কারো সাথে শেয়ার করবেন না**।
আপনার যদি এখনও কিছু অবশিষ্ট ফান্ড থাকে, তবে অবিলম্বে একটি নতুন ওয়ালেটে সেগুলো ট্রান্সফার করুন।

## Polygon ওয়ালেট একটি 'ওহো আমাদের সার্ভার হোঁচট খেয়েছে' ত্রুটি মেসেজ দেখায়। {#polygon-wallet-shows-an-oops-our-server-stumbled-error-message}

সেই মেসেজের মানে হতে পারে আমাদের সার্ভার ডাউন। যাইহোক, যদি সবকিছু ঠিকঠাক কাজ করে, আমরা আপনাকে অন্য ব্রাউজার ব্যবহার করার পরামর্শ দিই।
যদি আপনি একটি উইথড্র করার চেষ্টা করছেন তাহলে আপনি এছাড়াও [Polygon উইথড্র করার টুল](https://polygon-withdraw.matic.network/) ব্যবহার করতে পারেন। সেখানে, আপনি আপনার ওয়ালেট সংযোগ করতে পারেন, আপনার লেনদেন হ্যাশ পেস্ট করতে পারেন এবং লেনদেন করায় এগিয়ে যেতে পারেন।

## Polygon ওয়ালেট 'ইউজারের অস্বীকৃত লেনদেন স্বাক্ষর' ত্রুটির মেসেজ দেখায়। {#polygon-wallet-shows-user-denied-transaction-signature-error-message}

এটি সাধারণত ঘটে কারণ ব্যবহারকারী MetaMask এর মাধ্যমে একটি লেনদেন স্বাক্ষর করতে বাতিল বা অস্বীকৃতি করে। MetaMask ওয়ালেট দ্বারা অনুরোধ করা হলে, বাতিল না করে অনুমোদনে ক্লিক করে লেনদেনে স্বাক্ষর করার সাথে এগিয়ে যান।

## আমি একটি এক্সচেঞ্জে ট্রান্সফার করা টোকেন পাইনি {#i-did-not-receive-the-tokens-i-transferred-to-an-exchange}
আপনি Binance এ কয়েন ট্রান্সফার করেছেন (Coinbase, Kucoin বা অন্য কোনো এক্সচেঞ্জ) কিন্তু এক্সচেঞ্জের দিক থেকে সেগুলি গ্রহণ করেননি। যদি এটি আপনার ক্ষেত্রে হয়ে থাকে, তবে এটা জানা গুরুত্বপূর্ণ যে আমরা বর্তমানে এক্সচেঞ্জের সাথে সরাসরি সংযোগ প্রদান করি না। বেশিরভাগ লেনদেন আসলে এক্সচেঞ্জে পৌঁছানোর আগে Ethereum মেইননেট দ্বারা পাস করবে। অনুগ্রহ করে, এক্সচেঞ্জের সাহায্যকারী টিমের সাথে যোগাযোগ করুন।

## আমার MetaMask ওয়ালেট Polygon ওয়ালেটের সাথে কানেক্ট করছে না {#my-metamask-wallet-is-not-connecting-with-polygon-wallet}

এটি অনেক কারণে হতে পারে। আমরা পরামর্শ দিচ্ছি যে আপনি **আরেক সময় চেষ্টা করুন**, **অন্য একটি ব্রাউজার ব্যবহার করুন** বা, যদি এর কোনোটিতে কাজ না হয় তাহলে, **আমাদের সাহায্যকারী টিমের সাথে যোগাযোগ করুন**।

## গ্যাসের জন্য অর্থ প্রদানের জন্য আমি কিভাবে MATIC টোকেন পেতে পারি? {#how-can-i-get-matic-tokens-to-pay-for-gas-fees}

আমরা [গ্যাস সোয়াপ](https://wallet.polygon.technology/gas-swap/) পরিষেবা প্রদান করি যেটি আপনার কাজে লাগতে পারে। আপনি নিজের লেনদেন সম্পূর্ণ করার জন্য প্রয়োজনীয় পরিমাণ MATIC বেছে নিন এবং আপনি এটিকে অন্যান্য টোকেন যেমন ইথার বা USDT-এর জন্য অদলবদল করতে পারেন। এটি **গ্যাস ছাড়া লেনদেনের জন্য** ব্যবহার করা যায় না।

## টোকেন অদলবদল খুব ধীরে হয়। {#token-swap-is-too-slow}

আপনি যদি টোকেন অদলবদল করার চেষ্টা করছেন এবং এটি খুব বেশি সময় নিচ্ছে, আপনি অন্য ব্রাউজারে একই লেনদেন চেষ্টা করতে পারেন। যদি এটি কাজ না করে এবং আপনি একটি ত্রুটির সম্মুখীন হন, অনুগ্রহ করে আমাদের সাহায্যকারী টিমকে একটি স্ক্রিনশট পাঠান৷
