# Smoke Network Node Setup

Note 1:  Requires running  Ubuntu 16.04.4 LTS (Xenial Xerus)

Note 2:  This document will use  ``$``   as the command prompt indicator and  `user`  for your username. Please use your correct username in place of  `user`.

Note 3:  Some single line commands are quite long and wrap in this document. Make sure they are entered into the terminal window as a single line command. You may need to copy to a local editor first.

## Node server install
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

6 - Download files.

```wget https://github.com/smokenetwork/smoked/releases/download/v0.0.4/smoked-0 .0.4-x86_64-linux.tar.gz
 wget https://github.com/smokenetwork/smoked/releases/download/v0.0.4/cli_wall et-0.0.4-x86_64-linux.tar.gz```

7 - Uncompress files.

```tar -xzf smoked-0.0.4-x86_64-linux.tar.gz
 tar -xzf cli_wallet-0.0.4-x86_64-linux.tar.gz```

8 - Remove compressed files.

``` rm *.gz ```

9 - Create p2p private key by starting the node twice.

``` ./smoked ```

10 - Press  control-C  (mac) or  Ctrl-C  (windows) to stop the node.

11 - Start node again.

```  ./smoked ```

12 - Press  control-C  (mac) or  Ctrl-C  (windows) to stop the node.

13 - Verify that  witness_node_data_dir/p2p/node_config.json  file was created. If not, start and
stop the Node again.

14 - Replace default p2p key in  config.ini  with your p2p key.  **NOTE:  This is a single line
command.**

```sed -i s/\"0000000000000000000000000000000000000000000000000000000000000000\"/$(jq .private_key witness_node_data_dir/p2p/node_config.json)/g witness_node_data_dir/config.ini```

15 - Update  config.ini  with seed nodes.

```  nano /home/ user/  smoke/witness_node_data_dir/config.ini ```

16 - Find  #seed-node =  and replace with:

```seed-node = 163.172.128.38:2001
 seed-node = 51.15.95.123:2001```

17 - Create a detachable session and start the Node.

```screen -S smoked
 cd /home/user/smoke
 ./smoked```

18 - Detach session but leave Node running by pressing  control-A-D  (mac) or  Ctrl-A-D (windows).

---
