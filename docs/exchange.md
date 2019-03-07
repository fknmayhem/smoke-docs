# Exchange Setup

## Setup a fullnode

Follow the [node](https://docs.smoke.io/#/node) instructions, and then in a trusted environment run:

``` ./smoked --rpc-endpoint=127.0.0.1:8092 ```

*You can also use the official smoke RPC:* https://rpc.smoke.io

## Checking Balance

Check the balance of exchange account using get_accounts api:

``` curl https://rpc.smoke.io --data '{"jsonrpc":"2.0", "id":0, "method":"call", "params":["database_api", "get_accounts", [["test"]]]}' ```

## Monitoring Deposit

### Blockchain Parameters and Last Block

The RPC call ``` get_config ``` will return the configuration of the blockchain which contains the block interval in seconds. By calling ``` get_dynamic_global_properties ``` , we obtain the current head block number as well as the last irreversible block number. The difference between both is that the last block is last block that has been produced by the network and has thus been confirmed by the block producer. The last irreversible block is that block that has been confirmed by sufficient many block producers so that it can no longer be modified without a hard fork. Every block older than the last reversible block is equivalent to a checkpoint in Bitcoin. They are about 15 blocks ( 45 seconds ) behind the head block.

A particular block can be obtained via the ``` get_block <blocknumber> ``` call and takes the form shown above.

### Processing Block Data

Since the content of a block is unencrypted, all it takes to monitor an account is processing of the content of each block.

#### Example

The following will show example implementations for monitoring a specific account.

##### NodeJS

```
  var rpc = require('node-json-rpc');

  var last_block = 160900;
  var watch_account = "world";
  var options = {
      port: 8092,
      host: '127.0.0.1',
      path: '/rpc',
      strict: false
  };


  var callrpc = function(name, params, cb) {
      client.call(
          {"jsonrpc": "2.0",
           "method": name,
           "params": params,
           "id": 0},
          function(err, res) {
             if (err) { cb(err, null) }
             else { cb(null, res["result"]) }
          }
      );
  }

  var process_transfer = function(op, block, blockid) {
      console.log(block);
      if (op["to"] == watch_account) {
          console.log(blockid + " | " +
                      block["timestamp"] + " | "+
                      op["from"] + " -> " +
                      op["to"] + ": " +
                      op["amount"] + " -- " +
                      op["memo"]
              );
      }
  }

  var process_block = function(block, blockid) {
      console.log(blockid);
      console.log(block["transactions"]);
      for (var tx in block["transactions"]) {
          for (var opObj in tx["operations"]) {
              var opType = opObj[0];
              var op = opObj[1];

              console.log(op);

              if (opType == "transfer") {
                  process_transfer(op, block, blockid);
              }
          }
      }
  }

  var start_loop = function() {
      callrpc("get_dynamic_global_properties", [], function(err, props) {
          var block_number = props["last_irreversible_block_num"];
          while ((block_number - last_block) > 0) {
              last_block += 1
              callrpc("get_block", [last_block], function(err, block) {
                  process_block(block, last_block);
              });
          }
      });
  }


  var client = new rpc.Client(options);

  var block_interval;

  callrpc("get_config", [],
          function (err, config) {
              if (err) { console.log(err); }
              else {
                  block_interval = config["STEEMIT_BLOCK_INTERVAL"]
                  start_loop();
              }
          }
         )
```

## Transfer Token

Transfers asset from one account to another. The memo is plain-text, any encryption on the memo is up to a higher level protocol.

Example:

```
let operations = [];
 operations.push([
   "transfer",
   {
     "from": "exchange_acc",
     "to": "user_account",
     "amount": amount,
     "memo": ""
   }
 ]);

const tx_smoke = await smokejs.broadcast.sendAsync({operations, extensions: []}, {"active": "active_key_here"});
```
