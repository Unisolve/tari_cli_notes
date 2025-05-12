# Introduction
 
These notes cover mining Tari on the Linux command line. The setup documented here
is uses Ubuntu 22.04 with one or more GPUs. The notes assume you will be using the 
console wallet.

These notes don't assume that you have a Linux desktop available to you. The 
command line is all you need.

Please be aware that at present these notes are incomplete but I hope to address
more of the topic over time.

## Criticisms and corrections and ideas

I need them! Send criticisms, notes or ideas to: simon@unisolve.com.au

## Step 1 Check your OS

Run this one-line command:

```console
grep -s "^PRETTY_NAME=" /etc/os-release | sed 's/PRETTY_NAME=//;s/"//g' || cat /etc/*release 2>/dev/null | head -n1 || uname -sr
```

If you're on Ubuntu 22.04 you should see:

```console
Ubuntu 22.04.4 LTS
```

Otherwise, the one-liner script tries very hard to return as useful value, eg: 

```console
Ubuntu 20.04.6 LTS
CentOS Linux 7 (Core)
AlmaLinux 9.4 (Seafoam Ocelot)
Ubuntu 16.04.4 LTS
Raspbian GNU/Linux 10 (buster)
Ubuntu quantal (12.10)
```
  
These command line instructions might help you with other, recent Linux OSes, but for now we're concentratng 
on Ubunu 22.04

## Step 2. Download tari-suite

Using your desktop browser, (or a browser in the Linux desktop if you have one), go to this page to see the 
latest offerings: https://github.com/tari-project/tari/releases

Find the latest release (v2.1.0 in my case). You can tell you're looking at the latest release because of 
the "Latest" text just to the right of the version number.

See the "Assets" section just under "Contributors". Go to the bottom of the Assets section and click on
the "Show all nn assets" link if it's there. In my case this link says "Show all 88 assets".

Scroll down until you see the tari_suite-n.n.n zip file. In my case this is:

```console
tari_suite-2.1.0-0df1ede-linux-x86_64.zip
```

Right click on that URL in the "Assets" section of the releases page to copy the download link.

Now use the "wget" command on your Linux server to download tari_suite to that server using the link you
just copied. For me this looks like:

```console
wget https://github.com/tari-project/tari/releases/download/v2.1.0/tari_suite-2.1.0-0df1ede-linux-x86_64.zip
```

## Step 3. Extract files 

Replace the "2.1.0" string with your release number:

```console
unzip tari_suite-2.1.0-0df1ede-linux-x86_64.zip
```

You should see output like this:

```console
Archive:  tari_suite-2.1.0-0dflede-linux-x86_64.zip
  inflating: libminotari_mining_helper_ffi.so
  inflating: minotari_console_wallet
  inflating: minotari_merge_mining_proxy
  inflating: minotari_miner
  inflating: minotari_node
  inflating: minotari_node-metrics
  inflating: start_tor.sh
  inflating: tari_suite-2.1.0-0dflede-linux-x86_64.sha256
```

## Step 4. Start the console wallet

Create a new Linux window and start the console wallet:

```console
./minotari_console_wallet
```

```console
Initializing logging according to "/root/.tari/mainnet/config/wallet/log4rs.yml"
Node config does not exist.
Would you like to mine (Y/n)?
NOTE: this will enable additional gRPC methods that could be used to monitor and submit blocks from this node.
```

If you're asked "Would you like to mine", answer "Y"

Then you'll see:

```console
⠀⠀⠀⠀⠀⣠⣶⣿⣿⣿⣿⣶⣦⣀
⠀⢀⣤⣾⣿⡿⠋⠀⠀⠀⠀⠉⠛⠿⣿⣿⣶⣤⣀⠀⠀⠀⠀⠀⠀⢰⣿⣾⣾⣾⣾⣾⣾⣾⣾⣾⣿⠀⠀⠀⣾⣾⣾⡀⠀⠀⠀⠀⢰⣾⣾⣾⣾⣿⣶⣶⡀⠀⠀⠀⢸⣾⣿⠀
⠀⣿⣿⣿⣿⣿⣶⣶⣤⣄⡀⠀⠀⠀⠀⠀⠉⠛⣿⣿⠀⠀⠀⠀⠀⠈⠉⠉⠉⠉⣿⣿⡏⠉⠉⠉⠉⠀⠀⣰⣿⣿⣿⣿⠀⠀⠀⠀⢸⣿⣿⠉⠉⠉⠛⣿⣿⡆⠀⠀⢸⣿⣿⠀
⠀⣿⣿⠀⠀⠀⠈⠙⣿⡿⠿⣿⣿⣿⣶⣶⣤⣤⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⡇⠀⠀⠀⠀⠀⢠⣿⣿⠃⣿⣿⣷⠀⠀⠀⢸⣿⣿⣀⣀⣀⣴⣿⣿⠃⠀⠀⢸⣿⣿⠀
⠀⣿⣿⣤⠀⠀⠀⢸⣿⡟⠀⠀⠀⠀⠀⠉⣽⣿⣿⠟⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⡇⠀⠀⠀⠀⠀⣿⣿⣿⣤⣬⣿⣿⣆⠀⠀⢸⣿⣿⣿⣿⣿⡿⠟⠉⠀⠀⠀⢸⣿⣿⠀
⠀⠀⠙⣿⣿⣤⠀⢸⣿⡟⠀⠀⠀⣠⣾⣿⡿⠋⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⡇⠀⠀⠀⠀⣾⣿⣿⠿⠿⠿⢿⣿⣿⡀⠀⢸⣿⣿⠙⣿⣿⣿⣄⠀⠀⠀⠀⢸⣿⣿⠀
⠀⠀⠀⠀⠙⣿⣿⣼⣿⡟⣀⣶⣿⡿⠋⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⡇⠀⠀⠀⣰⣿⣿⠃⠀⠀⠀⠀⣿⣿⣿⠀⢸⣿⣿⠀⠀⠙⣿⣿⣷⣄⠀⠀⢸⣿⣿⠀
⠀⠀⠀⠀⠀⠀⠙⣿⣿⣿⣿⠛⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠙⠁⠀
Console Wallet

1. Create a new wallet.
2. Recover wallet from seed words or hardware device.
3. Create a read-only wallet using a view key.
>>
```

Create a new wallet by entering "1". You'll then be asked to enter and then confirm your wallet pasphrase.

The next question is:

```console
Would you like to use a connected hardware wallet? (Supported types: Ledger) (Y/n)
```

I'm choosing no, so I enter "n" here.

You are then asked to copy your seed words and type the word "confirm" to confirm that, yes,
you are never going to be shown these seed words again. Copy those seed words safely!

## Step 5. Start the local tari node

Create a new Linux window and start the node:

```console
./minotari_node
```

If you're asked:

```console
Node identity does not exist.
Would you like to create one (Y/n)?
```

answer "Y"

Once the node is running, you can enter control-c at any time to call up the command
prompt and enter commands. For example:

```console
version
```

or

```console
list-peers
```

or 
```console
help
```

## Step 6. Start the miner

Create a new Linux window and start the Sha3x miner:

```console
./minotari_miner
```

You should see:

```console
Initializing logging according to "/root/.tari/mainnet/config/miner/log4rs.yml"
04:21 INFO  Starting Minotari Miner version: 2.1.0-0df1ede27452e090cfa81c28338df390e9a11e6e-release

Please enter 'wallet-payment-address' ('quit' or 'exit' to quit) :
```

Locate the address in the console wallet as follows:

1. Use the left or right arrrow to move to the "Recieve" tab
2. Copy the "Tari Address interactive" address
 

Enter that address for the miner to use 
  
 
## Step 7.  RandomX/Monero Merge Mining ?

TODO
