# Smoke Network Witness Setup

Note 1:  Requires running  Ubuntu 16.04.4 LTS (Xenial Xerus)

Note 2:  This document will use  ``$``   as the command prompt indicator and  `user`  for your username. Please use your correct username in place of  `user`.

Note 3:  Some single line commands are quite long and wrap in this document. Make sure they are entered into the terminal window as a single line command. You may need to copy to a local editor first.

## Witness server install
1 - Open a terminal window and remotely log into your server. Navigate to your home directory.

``` cd /home/ user ```

2 - Create a directory called smoke.

``` mkdir smoke ```

3 - Change to the smoke directory.

``` cd smoke ```

4 - Get updates.

``` apt-get update ```

5 - Install packages

``` apt-get -y install wget nano screen jq ```

6 - Download files. *Check for the latest versions [here](https://github.com/smokenetwork/smoked/releases)*

```wget https://github.com/smokenetwork/smoked/releases/download/v0.0.6/smoked_lm-0.0.6-x86_64-linux.tar.gz
 wget https://github.com/smokenetwork/smoked/releases/download/v0.0.6/cli_wallet-0.0.6-x86_64-linux.tar.gz```

7 - Uncompress files.

```tar -xzf smoked_lm-0.0.6-x86_64-linux.tar.gz
 tar -xzf cli_wallet-0.0.6-x86_64-linux.tar.gz```

8 - Remove compressed files.

``` rm *.gz ```

9 - Run ```Smoked``` to generate a config.ini file and then shut down node.

``` ./smoked ```

``` CTRL C ```

10 - Update  config.ini  with seed nodes.

```  nano witness_node_data_dir/config.ini ```

11 - Find shared-file-size = 1G and change :
   ```shared-file-size = 8G```

12 - Find  #seed-node =  and replace with:

```seed-node = 51.15.223.10:2001
 seed-node = 51.15.120.228:2001
 seed-node = 163.172.128.38:2001
seed-node = 51.15.95.123:2001```

13 - Find #rpc endpoint = , remove ```#``` and enter the value:

``` 127.0.0.1:8090 ```


14 - Create a detachable session and start the witness.

```screen -S smoked
 cd /home/user/smoke
 ./smoked```

15 - Detach session but leave witness running by pressing  control-A-D  (mac) or  Ctrl-A-D (windows).

---

## Client wallet configuration

1 - Create a detachable session for wallet.

```screen -S wallet```

2 - Navigate to smoke directory.

```cd /home/ user /smoke```

3 - Start the wallet.

``` ./cli_wallet -s https://rpc.smoke.io ```

4 - Set wallet password. Use a unique secure password.  **SAVE THESE IN A SAFE PLACE!**

new >>>  ``` set_password  "secure_password"```

5 - Unlock the wallet.

locked >>>  ```unlock  secure_password```

6 - Get your smoke.io keys.  Note:  You will need your smoke.io account name & password. All inputs in quotes.

unlocked >>>  ```get_private_key_from_password "account name" "active" "original_key"```

7 - This will return 2 keys. The 1st is your Public Active Key and the 2nd is your Private Active Key.

8 - Import Private Active Key. The ‘ private_active_key ’ is the 2nd key received from the previous step.  **No quotes!**

unlock >>>  ```import_key  private_active_key```

9 - Get brain keys1. (optional step but recommended)

unlock >>>  ```suggest_brain_key```

10 - This will generate 3 keys.  **SAVE THESE IN A SAFE PLACE!**

- brain_priv_key
- wif_priv_key
- pub_key

11 - Import ‘wif_priv_key’ into the wallet.  **No quotes!**

unlock >>>  ```import_key  wif_priv_key```

12 - Detach session but leave wallet running by pressing  control-A-D  (mac) or  Ctrl-A-D  (windows).

13 - Update config.ini with ‘wif_priv_key’.

```nano /home/ user/  smoke/witness_node_data_dir/config.ini```

14 -  Locate the  ‘#witness =’  line

- Uncomment the line by removing the ‘#’ at the beginning. - Add smoke.io account name in quotes.

```witness = " account_name"```

15 - Locate the ‘#private-key =’ line

- Uncomment the line by removing the ‘#’ at the beginning.
- Add the ‘wif_priv_key’ or if you did not create brain key you will use the ‘private_active_key’ that was previously imported into the cli_wallet.  **No quotes!**

```private-key =  wif_priv_key```

16 - Save updates and exit by pressing  Control-X  (mac) or  Ctrl-X  (windows), then  Y,  then  return (mac) or  Enter  (windows).

17 - Switch to witness session to invoke updates.

```screen -r smoked```

18 - Stop witness by pressing  control-c  (mac) or  Ctrl-C  (windows).

19 - Restart witness to pick up changes.

``` ./smoked ```

20 - Detach session but leave witness running by pressing  control-A-D  (mac) or  Ctrl-A-D (windows).

21 - Switch to wallet session for witness update.

```screen -r wallet```

22 - Send update for witness, all inputs in quotes. The ‘ witness_url’  will be used for the link in the witness voting list. It can be left blank, but the url of your witness testimonial is often used. The ‘ pub_key’  is from the brain keys you saved in a safe place earlier or if you did not create brain keys you will use the Public Active Key returned in step 6 .

unlock >>>  ```update_witness " account_name"  " witness_url"  " pub_key"  {} true```

---

Go to  https://smoke.io/~witnesses  and vote for yourself as a witness.

Make an announcement post and engage the community for voting support to make it into the top 21.


- If you need to shutdown your witness update with the null key ```SMK1111111111111111111111111111111114T1Anm``` before shutting down to avoid missing blocks.
