---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: আপনার পরবর্তী ব্লকচেইন অ্যাপটি Polygon-এ তৈরি করুন।
keywords:
  - docs
  - matic
  - polygon
  - ethereum
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

# Ethereum ↔ Polygon {#ethereum-polygon}

আপনার এসেটগুলো Ethereum থেকে Polygon-এ এবং Polygon থেকে Ethereum-এ ট্রান্সফার করার Plasma সিকিউরড সলিউশন।
* Polygon Plasma চুক্তির সাথে ইন্টারেক্ট করার জন্য [matic.js](https://github.com/maticnetwork/matic.js) ব্যবহার করুন।

## ফ্লো {#flow}
Polygon-এ আপনার চুক্তি ডিপ্লয় করার এবং Ethereum↔Polygon সাপোর্টের ফ্লো এখানে দেয়া হয়েছে।

1. ব্যবহারকারী Ethereum - XToken-এ ERC-20 টোকেন ডিপ্লয় করে

2. এখন [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ)-এর সাথে আপনার চুক্তির ঠিকানা শেয়ার করুন। এখানে একটি অনুরোধের উদাহরণ দেওয়া হলো...

> হ্যালো, আমরা হলাম Polygon-এ ডিপ্লয় করা AwesomeDApp। আমার এসেটগুলো Ethereum থেকে Polygon-এ এবং Polygon থেকে Ethereum-এ ট্রান্সফার করার জন্য একটি সমাধান খুঁজছেন। <br/><br/>
> আমার AwesomeDApp-এ একটি সংক্ষিপ্ত বিবরণ...<br/><br/>
> Ropsten-এ Token_Address-> "0x.."<br/>
> Token_Name-> "XToken"<br/>
> Token_Symbol-> "X"<br/>
> Token_Decimals-> "18"<br/><br/>
> এই টোকেনগুলো Polygon টেস্টনেট সংস্করণে ম্যাপ করার জন্য আপনাকে অনুরোধ করা হচ্ছে।<br/>

আমরা আপনার জন্য Polygon-এ একটি চাইল্ড চুক্তি ডিপ্লয় করবো, যা আপনার চাহিদার উপর ভিত্তি করে নমনীয় হতে পারে এবং আপনার টোকেন Ethereum ↔ Polygon-এ ম্যাপ করা যাবে।( Polygon-এ ডিপ্লয় করার জন্য এর নেটিভ টোকেন, Polygon-এর প্রয়োজন হয়, যা Ethereum থেকে Polygon-এ জমা করা যাবে বা সেকেন্ডারি মার্কেটপ্লেস থেকে কেনা যেতে পারে।)

3. ব্যবহারকারী Xtokens মিন্ট করতে পারেন এবং Ethereum-এ ট্রান্সফার করতে পারেন। উদাহরণস্বরূপ, মনে করুন 100XToken মিন্ট করার পর অন্য একটি অ্যাকাউন্টে ট্রান্সফার করা হয়েছে।

4. Polygon চেইনে এই টোকেনগুলো এভেইল করতে, ডিপোজিট ফাংশনটি কল করুন, যা প্রথমে অনুমোদন এবং তারপর depositERC20 কল করবে।

5. এখন একই ঠিকানায় Polygon চেইনে 100XTokens পাওয়া যাবে।

6. আপনি 50টি XToken YourAddress থেকে NewAddress-এ ট্রান্সফার করতে পারবেন। এছাড়াও, Polygon-এ লেনদেন করার জন্য Ethereum-এর মতোই Polygon এর নিজস্ব নেটিভ টোকেন ব্যবহার করে।

7. যদি ব্যবহারকারী এই Xtoken Ethereum চেইনে ফিরে পেতে চান, তাহলে StartWithdraw কল করতে হবে, যা childTokenContract থেকে উইথড্র করবে এবং Polygon চেইনে এই টোকেনগুলো বার্ন করবে। কোনো খারাপ অংশগ্রহণ এড়িয়ে যাওয়ার জন্য, একগুচ্ছ ভ্যালিডেশন করা হবে। এটি সম্পন্ন হওয়ার পর টোকেনগুলো Ethereum চেইনে পাওয়া যাবে।

8. আপনার EOA-তে বা আপনার অ্যাকাউন্টের ঠিকানায় সেই টোকেনগুলো পেতে processExits() কল করুন।

9. আপনি আপনার অ্যাকাউন্টের ঠিকানায় Ethereum মেইননেটে 50টি XToken দেখতে পাবেন।
