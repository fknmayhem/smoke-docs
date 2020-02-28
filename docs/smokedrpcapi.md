# Smoked API Calls

The Smoke Network runs on decentralized smoked server nodes which allow for numerous complex functions to be called depending on which API module is referenced.

This page lists various API calls for the smoked binary which acts as a backbone for the entire smoke network. It should be noted that smoked is different than the smoke wallet which is cli_wallet which is a completely different program that can be run alongside or independently of a smoked node. smoke is pretty complex and a number of API call rules apply.

## Before Attempting smoked RPC Calls

In order to access smoked calls you MUST have a full node running and listening to port 8092, on a local machine (or other server you have access to) or use the official https://pubrpc.smoke.io node.

### Call Format for smoked

The Smoke Network is built off of Graphene architecture meaning that RPC calls are state-less and can be accessed through regular JSON formatted RPC-HTTP.

The following structure should be used when calling the smoked client:

``` { "jsonrpc": "2.0", "method": "get_accounts", "params": [["smoke"]], "id": 1 } ```

Or

```
{
"jsonrpc": "2.0",
"method": "get_accounts",
"params": [["smoke"]],
"id": 1
} ```

In the example above the "get_accounts" function calls to the database_api module and would return information pertaining to the @smoke account.

```
{"id":1,"result":[{"id":24,"name":"smoke","owner":{"weight_threshold":1,"account_auths":[],"key_auths":[["SMK619jJm3VKrHRLbKaAkFXSCUBFwwv9d4yuTYM9KT6cjJV6zno1G",1]]},"active":{"weight_threshold":1,"account_auths":[],"key_auths":[["SMK619jJm3VKrHRLbKaAkFXSCUBFwwv9d4yuTYM9KT6cjJV6zno1G",1]]},"posting":{"weight_threshold":1,"account_auths":[],"key_auths":[["SMK619jJm3VKrHRLbKaAkFXSCUBFwwv9d4yuTYM9KT6cjJV6zno1G",1]]},"memo_key":"SMK619jJm3VKrHRLbKaAkFXSCUBFwwv9d4yuTYM9KT6cjJV6zno1G","json_metadata":"","proxy":"","last_owner_update":"1970-01-01T00:00:00","last_account_update":"1970-01-01T00:00:00","created":"1970-01-01T00:00:00","mined":true,"owner_challenged":false,"active_challenged":false,"last_owner_proved":"1970-01-01T00:00:00","last_active_proved":"1970-01-01T00:00:00","recovery_account":"","last_account_recovery":"1970-01-01T00:00:00","reset_account":"null","comment_count":0,"lifetime_vote_count":0,"post_count":0,"can_vote":true,"voting_power":10000,"last_vote_time":"1970-01-01T00:00:00","balance":"6536077.678 SMOKE","reward_steem_balance":"0.000 SMOKE","reward_vesting_balance":"0.000000 VESTS","reward_vesting_steem":"0.000 SMOKE","vesting_shares":"11.000000 VESTS","delegated_vesting_shares":"0.000000 VESTS","received_vesting_shares":"0.000000 VESTS","vesting_withdraw_rate":"0.000000 VESTS","next_vesting_withdrawal":"1969-12-31T23:59:59","withdrawn":0,"to_withdraw":0,"withdraw_routes":0,"curation_rewards":0,"posting_rewards":0,"proxied_vsf_votes":[0,0,0,0],"witnesses_voted_for":0,"average_bandwidth":"57950572844","lifetime_bandwidth":"765545000000","last_bandwidth_update":"2018-11-08T11:13:06","average_market_bandwidth":"24074464831","lifetime_market_bandwidth":"494470000000","last_market_bandwidth_update":"2018-11-08T07:57:42","last_post":"1970-01-01T00:00:00","last_root_post":"1970-01-01T00:00:00","vesting_balance":"0.000 SMOKE","reputation":0,"transfer_history":[],"post_history":[],"vote_history":[],"other_history":[],"witness_votes":[],"tags_usage":[],"guest_bloggers":[]}]}
```

## Using curl

A simple way to pass command to the same command to the smoked client is by with curl using the following format:

``` curl --data '{"jsonrpc": "2.0", "method": "get_accounts", "params": [["smoke"]], "id": 1 }' https://rpc.smoke.io ```

## Calls That Are a Success

When an API call is successful it will return a response JSON formatted. The returned response should also have a similar id number indicating it's from the call you've just put out:
```
{ "id":1, "result": "data" }
```

The output of the above curl call invoking the get_accounts function with the id of 1 & the @smoke username in the only parameter yields a response of:

```
{"id":1,"result":[{"id":24,"name":"smoke","owner":{"weight_threshold":1,"account_auths":[],"key_auths":[["SMK619jJm3VKrHRLbKaAkFXSCUBFwwv9d4yuTYM9KT6cjJV6zno1G",1]]},"active":{"weight_threshold":1,"account_auths":[],"key_auths":[["SMK619jJm3VKrHRLbKaAkFXSCUBFwwv9d4yuTYM9KT6cjJV6zno1G",1]]},"posting":{"weight_threshold":1,"account_auths":[],"key_auths":[["SMK619jJm3VKrHRLbKaAkFXSCUBFwwv9d4yuTYM9KT6cjJV6zno1G",1]]},"memo_key":"SMK619jJm3VKrHRLbKaAkFXSCUBFwwv9d4yuTYM9KT6cjJV6zno1G","json_metadata":"","proxy":"","last_owner_update":"1970-01-01T00:00:00","last_account_update":"1970-01-01T00:00:00","created":"1970-01-01T00:00:00","mined":true,"owner_challenged":false,"active_challenged":false,"last_owner_proved":"1970-01-01T00:00:00","last_active_proved":"1970-01-01T00:00:00","recovery_account":"","last_account_recovery":"1970-01-01T00:00:00","reset_account":"null","comment_count":0,"lifetime_vote_count":0,"post_count":0,"can_vote":true,"voting_power":10000,"last_vote_time":"1970-01-01T00:00:00","balance":"6536077.678 SMOKE","reward_steem_balance":"0.000 SMOKE","reward_vesting_balance":"0.000000 VESTS","reward_vesting_steem":"0.000 SMOKE","vesting_shares":"11.000000 VESTS","delegated_vesting_shares":"0.000000 VESTS","received_vesting_shares":"0.000000 VESTS","vesting_withdraw_rate":"0.000000 VESTS","next_vesting_withdrawal":"1969-12-31T23:59:59","withdrawn":0,"to_withdraw":0,"withdraw_routes":0,"curation_rewards":0,"posting_rewards":0,"proxied_vsf_votes":[0,0,0,0],"witnesses_voted_for":0,"average_bandwidth":"57950572844","lifetime_bandwidth":"765545000000","last_bandwidth_update":"2018-11-08T11:13:06","average_market_bandwidth":"24074464831","lifetime_market_bandwidth":"494470000000","last_market_bandwidth_update":"2018-11-08T07:57:42","last_post":"1970-01-01T00:00:00","last_root_post":"1970-01-01T00:00:00","vesting_balance":"0.000 SMOKE","reputation":0,"transfer_history":[],"post_history":[],"vote_history":[],"other_history":[],"witness_votes":[],"tags_usage":[],"guest_bloggers":[]}]}
```

As you can see a fair amount of data is given off by some of these calls which can easily be parsed or scraped for whatever intention a coder had for the information.

## Calls That Fail

If an API doesn't return a successful call the return output will show some details as shown below:

```
{
"id": 0
"error": {
"data": {
"code": error-code,
"name": " .. name of exception .."
"message": " .. message of exception ..",
"stack": [ .. stack trace .. ],
},
"code": 1,
},
}
```

Error handling will spit out some information pertaining to what went wrong. I've included an actual example of a response from a failed call below:


```
{"id": 177,"error": {"code": 1,"message": "7 bad_cast_exception: Bad Cast\nInvalid cast from string_type to Array\n {"type":"string_type"}\n th_a variant.cpp:537 get_array","data": {"code": 7,"name": "bad_cast_exception","message": "Bad Cast","stack": [{"context": {"level": "error","file": "variant.cpp","line": 537,"method": "get_array","hostname": "","thread_name": "th_a","timestamp": "2016-09-18T06:41:36"},"format": "Invalid cast from ${type} to Array","data" :{"type": "string_type"}}]}}}
```

## login_api functions

### login

Call example:

``` { "id": 1, "method": "login", "params": [["username", "password"]]} ```

Usage: login to accounts on the smoke network
get_api_by_name

## Accounts

### get_accounts

JSON example:

``` {"id":3,"method":"get_accounts","params":[["username"]]} ```

Usage: data pertaining to accounts included in call. Call multiples simply by adding a comma between the names.

Example: "params":[["usernamehere", "smoke"]]

### get_account_references

Call example:

``` {"id":5,"method":"lookup_account_names","params":[["username", "callback"]]} ```

Usage: information about the accounts. Call multiples simply by adding a comma between the names. example: "usernamehere", "smoke"

### lookup_accounts

Call example:

``` {"id":6,"method":"lookup_accounts","params":[["username", "limit"]]} ```

Usage: display usernames containing letters given in the first parameter.

### get_account_count

Call example:

``` {"id":7,"method":"get_account_count","params":[]} ```

Usage: number of smoke accounts on the network currently.

### get_conversion_requests

Call example:

``` {"id":8,"method":"get_conversion_requests","params":[["username"]]} ```

Usage: current conversion requests of the given account.

### get_account_history

Call example:

``` {"id": 9, method: 'get_account_history', 'params': [["username", "from", "limit"]]} ```

Usage: recall the history of given account on the smoke network.

### get_owner_history

Call example:

``` {"id": 10, method: 'get_owner_history', 'params': [["username"]]} ```

Usage: if the given account has changed ownership on the blockchain.

## Voting

### get_active_votes

Call example:

``` {"id": 12, method: 'get_active_votes', 'params': [[ "username", "permalink"]]} ```

Usage: if a post currently has any active votes on it.

### get_account_votes

Call example:

``` {"id": 13, method: 'get_account_votes', 'params': [[ "username"]]} ```

Usage: last 100+ votes on the given account.

## Content

### get_content

Call example:

``` {"id":19,"method":"get_content","params":["username","permalink"]} ```

Usage: information about the post given in second parameter.

### get_content_replies

Call example:
``` {"id":20,"method":"get_content_replies","params":["username","permalink"]} ```

Usage: all replies on the post given in second parameter.

### get_discussions_by_author_before_date

Call example:

``` {"id":21,"method":"get_content_replies","params":[["username", "startpermalink", "beforedate", "limit"]]} ```

Usage: discussions from the username given from a starting permalink or start date.

### get_replies_by_last_update

Call example:

``` {"id":22,"method":"get_content_replies","params":[["username", "startpermalink", "limit"]]}```

Usage: replies from the username given from a starting permalink.

## Block Info

### get_block

Call example:

``` {"id":23,"method":"get_block","params":["blocknumber"]} ```

Usage: various information about the particular block number given.

### get_block_header

Call example:

``` {"id":24,"method":"get_block_header","params":["blocknumber"]} ```

Usage: header and other brief info about the given block number.

### get_state

Call example:

``` {"id":25,"method":"get_block_header","params":["path"]} ```

Usage: current state of the smoke network. Leave path blank for

## current info

### get_trending_categories

Call example:

``` {"id":26,"method":"get_trending_categories","params":[["searchafter","limit"]]} ```

Usage: searching of trending categories both current and past.

## Transactions / Authority / Validation

### get_transaction_hex

Call example:

``` {"id":32,"method":"get_transaction_hex","params":["trx"]} ```

Usage: transaction hex digits from the given transaction.

### get_transaction

Call example:

``` {"id":33,"method":"get_transaction","params":["txid"]} ```

Usage: details a transaction from a given transactionID.

## Globals

### get_config

Call example:

``` {"id":38,"method":"get_config","params":[]} ```

Usage: current configuration of the smoked node.

### get_dynamic_global_properties

Call example:

``` {"id":39,"method":"get_dynamic_global_properties","params":[]} ```

Usage: overview of various information regarding the current state of the smoke network.

### get_chain_properties

Call example:

``` {"id":40,"method":"get_chain_properties","params":[]} ```

Usage: current account creation fee & maximum block size.

### get_hardfork_version

Call example:

``` {"id":40,"method":"get_hardfork_version","params":[]} ```

Usage: current version of smoke hardfork will be displayed.

### get_next_scheduled_hardfork

Call example:

``` {"id":42,"method":"get_hardfork_version","params":[]} ```

Usage: date and version as to when the next version of smoke is expected.

## Witnesses

### get_witnesses

Call example:

``` {"id":43,"method":"get_witnesses","params":["witnessid"]} ```


### get_witness_by_account

Call example:

``` {"id":44,"method":"get_witness_by_account","params":["username"]} ```

Usage: true if the username given is a witness or "result": null if not.

### get_witnesses_by_vote

Call example:

``` {"id":45,"method":"get_witnesses_by_vote","params":[["username/blank", "limit"]]} ```

Usage: list of the top witnesses by order of witness votes.

### lookup_witness_accounts

Call example:

``` {"id":46,"method":"lookup_witness_accounts","params":[["searchusername", "limit"]]} ```

Usage: list of every user that has declared their intent to run as witness.

### get_witness_count

Call example:

``` {"id":47,"method":"get_witness_count","params":[]} ```

Usage: total number of accounts that have shown intent to run for witness.

### get_active_witnesses

Call example:

``` {"id":48,"method":"get_active_witnesses","params":[]} ```

Usage: active witnesses (Top 21).

### get_miner_queue

Call example:

``` {"id":49,"method":"get_miner_queue","params":[]} ```

Usage: list of miners waiting to get into the DPOW line to create a block.


Tags


### get_trending_tags

Call example:

``` {"id":54,"method":"get_trending_tags","params":[["aftertag", "limit"]]} ```

Usage: list of tags containing the first parameter (almost as if parent and "spin-off" tags).

### get_discussions_by_trending

Call example:

``` {"id":55,"method":"get_discussions_by_trending","params":[{"tag":"tagnamehere", "limit":"10"}]} ```

Usage: list of tags containing the first parameter (almost as if parent and "spin-off" tags).

### get_discussions_by_created

Call example:

``` {"id":56,"method":"get_discussions_by_created","params":[{"tag":"tagnamehere","limit":"10"}]} ```

Usage: list of post from the start of the tags containing the first parameter.

### get_discussions_by_active

Call example:

``` {"id":57,"method":"get_discussions_by_active","params":[{"tag":"tagnamehere","limit":"10"}]} ```

Usage: list of active posts from tag contained the first parameter.

### get_discussions_by_cashout

Call example:

``` {"id":58,"method":"get_discussions_by_cashout","params":[{"tag":"tagnamehere","limit":"10"}]} ```

Usage: list of posts with outstanding payouts from the tag contained the first parameter.

### get_discussions_by_payout

Call example:

``` {"id":59,"method":"get_discussions_by_payout","params":[{"tag":"tagnamehere","limit":"10"}]} ```

### get_discussions_by_votes

Call example:

``` {"id":60,"method":"get_discussions_by_votes","params":[{"tag":"tagnamehere","limit":"10"}]} ```

Usage: list of posts sorted by votes from the tag contained the first parameter.

### get_discussions_by_children

Call example:

``` {"id":61,"method":"get_discussions_by_children","params":[{"tag":"tagnamehere","limit":"10"}]} ```

Usage: list of child posts from the tag contained the first parameter.

### get_discussions_by_hot

Call example:

``` {"id":62,"method":"get_discussions_by_hot","params":[{"tag":"tagnamehere","limit":"10"}]} ```

Usage: list of the hottest posts from the tag contained the first parameter.

### get_discussions_by_total_pending_payout

Call example:

``` {"id":63,"method":"get_discussions_by_total_pending_payout","params":[{"tag":"tagnamehere","limit":"10"}]} ```


## Keys


### get_key_references

Call example:

``` {"id":64,"method":"get_key_references","params":["key"]} ```
