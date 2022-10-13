---
id: json-rpc-commands
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - json
  - rpc
  - commands
---


<div>
<div><pre className="json_rpc_terminal"></pre></div>
<div></div>
</div>

##  {#eth}

###  {#eth_chainid}



---

<h4></h4>

*

<h4></h4>

*

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_chainId","params":[],"id":1}'
````



###  {#eth_syncing}



---

<h4></h4>

*

<h4></h4>




  *
  *
  *

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_syncing","params":[],"id":1}'
````



###  {#eth_getblockbynumber}



---

<h4></h4>

*
*

<h4></h4>

*
*
*
*
*
*
*
*
*
*
*
*
*
*
*
*
*
*
*

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest", true],"id":1}'
````




###  {#eth_getblockbyhash}



---

<h4></h4>

*
*

<h4></h4>

*
*
*
*
*
*
*
*
*
*
*
*
*
*
*
*
*
*
*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockByHash","params":["0xdc0818cf78f21a8e70579cb46a43643f78291264dda342ae31049421c82d21ae",false],"id":1}'
````

###  {#eth_blocknumber}



---

<h4></h4>



<h4></h4>

*

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
````



###  {#eth_gasprice}



---

<h4></h4>



<h4></h4>

*

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":1}'
````



###  {#eth_getbalance}



---

<h4></h4>

*
*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1", "latest"],"id":1}'
````

###  {#eth_sendrawtransaction}



---

<h4></h4>

*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":["0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"],"id":1}'
````

###  {#eth_gettransactionbyhash}



---

<h4></h4>

*

<h4></h4>

*
*
*
*
*
*
*
*
*
*
*
*
*
*

<h4></h4>


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getTransactionByHash","params":["0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b"],"id":1}'
````

###  {#eth_gettransactionreceipt}





---

<h4></h4>

*

<h4></h4>

*
*
*
*
*
*
*
*
*
*
*



*
*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getTransactionReceipt","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}'
````

###  {#eth_gettransactioncount}



---

<h4></h4>

*
*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1","latest"],"id":1}'
````

###  {#eth_getblocktransactioncountbynumber}



---

<h4></h4>

*

<h4></h4>

*

<h4></h4>



````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByNumber","params":["latest"],"id":1}'
````



###  {#eth_getlogs}



---

<h4></h4>

*
*
*
*
*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getLogs","params":[{"topics": ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]}],"id":1}'
````


###  {#eth_getcode}



---

<h4></h4>

*
*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getCode","params":["0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b", "0x2"],"id":1}'
````

###  {#eth_call}



---

<h4></h4>

*
*
*
*
*
*
*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_call","params":[{see above}],"id":1}'
````

###  {#eth_getstorageat}



---

<h4></h4>

*
*
*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getStorageAt","params":["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x0", "latest"],"id":1}'
````

###  {#eth_estimategas}



---

<h4></h4>





*
*
*
*
*
*
*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_estimateGas","params":[{see above}],"id":1}'
````

###  {#eth_newfilter}



---

<h4></h4>

*
*
*
*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_newFilter","params":[{"topics":["0x12341234"]}],"id":1}'
````

###  {#eth_newblockfilter}



---

<h4></h4>



<h4></h4>

1.

<h4></h4>



````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_newBlockFilter","params":[],"id":1}'
````



###  {#eth_getfilterlogs}


:::caution

1.
2.
:::

<h4></h4>

*

<h4></h4>

*
    *
    *
    *
    *
    *
    *
    *
    *
    *

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getFilterLogs","params":["0x16"],"id":1}'
````


###  {#eth_getfilterchanges}



---

<h4></h4>

*

<h4></h4>

*
*
    *
    *
    *
    *
    *
    *
    *
    *
    *

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getFilterChanges","params":["0x16"],"id":1}'
````

###  {#eth_uninstallfilter}



---

<h4></h4>

*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_uninstallFilter","params":["0xb"],"id":1}'
````

###  {#eth_unsubscribe}



---

<h4></h4>

*

<h4></h4>

*

<h4></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_unsubscribe","params":["0x9cef478923ff08bf67fde6c64013158d"],"id":1}'
````

##  {#net}

###  {#net_version}



---

<h4></h4>



<h4></h4>

*

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_version","params":[],"id":83}'
````



###  {#net_listening}



---

<h4></h4>



<h4></h4>

*

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":83}'
````



###  {#net_peercount}



---

<h4></h4>



<h4></h4>

*

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}'
````



##  {#web3}

###  {#web3_clientversion}



---

<h4></h4>



<h4></h4>

*

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":1}'
````



###  {#web3_sha3}



---

<h4></h4>

*

<h4></h4>

*

<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"web3_sha3","params":["0x68656c6c6f20776f726c64"],"id":1}'
````



##  {#txpool}

###  {#txpool_content}



---

<h4></h4>




<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_content","params":[],"id":1}'
````



###  {#txpool_inspect}



---

<h4></h4>




<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_inspect","params":[],"id":1}'
````



###  {#txpool_status}



---

<h4></h4>



<h4></h4>




````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_status","params":[],"id":1}'
````

