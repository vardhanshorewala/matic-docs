---
id: secrets
title: In Band Secret Distribution
sidebar_label: In Band Secret Distribution
description: "A solution to encrypt secrets and ensure their decryption."
keywords:
  - docs
  - polygon
  - nightfall
  - secret
  - encryption
image: https://matic.network/banners/matic-network-16x9.png
---

## Overview

To ensure a recipient receives the secret information required to spend their commitments, the sender encrypts the secrets (salt, value, tokenId, ercAddress) of the commitment sent to the recipient and proves using ZKP that they encrypted this correctly with the recipient's public key. ElGamal encryption over elliptic curves is used for encryption.
