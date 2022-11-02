---
id: backup-restore
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - instance
  - restore
  - directory
  - node
---

##  {#overview}



##  {#base-folders}


*
*
*
*



##  {#create-backup-from-a-running-node-and-restore-for-new-node}



###  {#backup}



```bash
$ polygon-edge backup --grpc-address 127.0.0.1:9632 --out backup.dat [--from 0x0] [--to 0x100]
```

###  {#restore}



```bash
$ polygon-edge server --restore archive.dat
```

##  {#back-up-restore-whole-data}



###  {#step-1-stop-the-running-client}






*
*

###  {#step-2-backup-the-directory}



:::info

:::

##  {#restore-1}

###  {#step-1-stop-the-running-client-1}



###  {#step-2-copy-the-backed-up-data-directory-to-the-desired-folder}



###  {#step-3-run-the-polygon-edge-client-while-specifying-the-correct-data-directory}


