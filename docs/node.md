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

6 - Download files. *Check for the latest versions [here](https://github.com/smokenetwork/smoked/releases)*

```wget https://github.com/smokenetwork/smoked/releases/download/v0.0.5/smoked-0.0.5-x86_64-linux.tar.gz
 wget https://github.com/smokenetwork/smoked/releases/download/v0.0.5/cli_wallet-0.0.5-x86_64-linux.tar.gz```

7 - Uncompress files.

```tar -xzf smoked-0.0.5-x86_64-linux.tar.gz
 tar -xzf cli_wallet-0.0.5-x86_64-linux.tar.gz```

8 - Remove compressed files.

``` rm *.gz ```

9 - Run ```Smoked``` to generate a config.ini file and then shut down node.

``` ./smoked ```

``` CTRL C ```

10 - Update  config.ini  with seed nodes.

```  nano /home/ user/  smoke/witness_node_data_dir/config.ini ```

11 - Find  #seed-node =  and replace with:

```seed-node = 51.15.223.10:2001
 seed-node = 51.15.120.228:2001```

12 - Find #rpc endpoint = , remove ```#``` and enter the value:

``` 51.158.79.144:8090 ```

13 - Create a detachable session and start the Node.

```screen -S smoked
 cd /home/user/smoke
 ./smoked```

14 - Detach session but leave Node running by pressing  control-A-D  (mac) or  Ctrl-A-D (windows).

---
