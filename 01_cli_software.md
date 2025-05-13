# Download and verify the software
 
## Step 1. Check your OS

Run this one-line command:

```console
grep -s "^PRETTY_NAME=" /etc/os-release | sed 's/PRETTY_NAME=//;s/"//g' || cat /etc/*release 2>/dev/null | head -n1 || uname -sr
```

If you're on Ubuntu 22.04 you should see:

```console
Ubuntu 22.04.4 LTS
```

Otherwise, the one-liner script tries very hard to return a useful value, eg: 

```console
Ubuntu 20.04.6 LTS
CentOS Linux 7 (Core)
AlmaLinux 9.4 (Seafoam Ocelot)
Ubuntu 16.04.4 LTS
Raspbian GNU/Linux 10 (buster)
Ubuntu quantal (12.10)
```
  
These command line instructions might also help you with other recent Linux OSes, but for 
now we're concentratng on Ubunu 22.04

## Step 2. Create a top-level directory

Create an empty directory somewhere on your server and change directory there. We'll use the
name 'tar_cli' here, but call it anything that makes sense to you.

We'll then make a "bin" sub-directory. Don't forget this step.

```console
mkdir tari_cli
cd tari_cli
mkdir bin
```

## Step 2. Download tari-suite

Using your desktop browser, (or a browser in the Linux desktop if you have one), go to this page 
to see the latest offerings: https://github.com/tari-project/tari/releases

Note that any version with the string "-pre" in it, such as "v2.1.1-pre.0" is destined for a TestNet and
therefore is probably not what you're looking for. Similarly, any version containing "-rc", such as
"v2.1.0-rc.0" is the release candidate for the future StageNet/MainNet release.

So find the latest release without "-pre" or "-rc", (this is "v2.1.0" in my case). You can tell you're 
looking at the latest release because of the "Latest" text just to the right of the version number.

Now see the "Assets" section just under "Contributors". Go to the bottom of the Assets section and click on
the "Show all *nn* assets" link if it's there. In my case this link says "Show all 88 assets".

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

Now we'll get the sha256 check file and run 'shasum -c' on it to confirm that the zip file we've downloaded 
is the one prepared by the Tari project team.

```console
wget https://github.com/tari-project/tari/releases/download/v2.1.0/tari_suite-2.1.0-0df1ede-linux-x86_64.zip.sha256

shasum -c tari_suite-2.1.0-0df1ede-linux-x86_64.zip.sha256
```

You should see output like:

```console
tari_suite-2.1.0-0df1ede-linux-x86_64.zip: OK
```

At the end of this step, your top-level directory should contain just your 2 downloaded files and your empty 'bin'
directory:

```console
user@server:/workspace/tari_cli# ls -1
bin
tari_suite-2.1.0-0df1ede-linux-x86_64.zip
tari_suite-2.1.0-0df1ede-linux-x86_64.zip.sha256
```

## Step 3. Download glytex - a GPU based miner for Tari

Check out the the latest offerings at: https://github.com/tari-project/glytex/releases

In this example we'll be using v0.2.26, your version number might be different.

```console
wget -v https://github.com/tari-project/glytex/releases/download/v0.2.26/glytex-combined-macos-arm64-mainnet-0.2.26-78e833f.zip.sha256
wget -v https://github.com/tari-project/glytex/releases/download/v0.2.26/glytex-combined-macos-arm64-mainnet-0.2.26-78e833f.zip

shasum -c glytex-combined-macos-arm64-mainnet-0.2.26-78e833f.zip.sha256
```
You should see output like:

```console
TODO
```

At the end of this step, your top-level directory should contain just your 4 downloaded files and your empty 'bin'
directory:

```console
TODO
```

## Step 4. Extract files 

```console
cd bins
unzip ../glytex-combined-macos-arm64-mainnet-0.2.26-78e833f.zip.sha256
shasum -c glytex-combined-macos-arm64-mainnet-0.2.26-78e833f.sha256

./glytex --help

./glytex --detect=true --engine=opencl
```


We'll use "unzip" to extract the release files we want. Be sure to replace the "2.1.0" string with your 
release number:

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

Now we're getting somewhere.


[Return to the main README](README.md)
