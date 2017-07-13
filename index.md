## Quick run down to start mining Zen on linux with AMD cards.

First setup the AMD driver, open the terminal and just paste these commands.

```shell
cd ~
wget https://www2.ati.com/drivers/linux/ubuntu/amdgpu-pro-17.10-450821.tar.xz
tar -Jxvf amdgpu-pro-17.10-450821.tar.xz
cd amdgpu-pro-17.10-450821
./amdgpu-pro-install -y
sudo reboot
```

After it reboots, install the wallet.

```shell
cd ~
git clone https://github.com/zencashofficial/zen
cd zen
./zcutil/build.sh -j $(nproc)
mkdir -p ~/.zen
echo "addnode=dnsseed.zensystem.io" >~/.zen/zen.conf
echo "rpcuser=username" >>~/.zen/zen.conf
echo "rpcpassword=`head -c 32 /dev/urandom | base64`" >>~/.zcash/zcash.conf
```

Zend would be then installed `src/` in the `zen` folder. To run it. just do `./src/zend`

This would start it, to start it without it taking the entire terminal, just do `./zend -daemon` so you can still issue commands.

You don't need to sync it, so just do `./zen-cli getnewaddress`, this will generate an address for you, so you can log onto mining pools.

Now you need to download mining software, Optiminer is always a great choice and I prefer it over Claymore's miner. Like the wallet and driver, these instructions will just be copy and paste.
```shell
cd ~
git clone https://github.com/Optiminer/OptiminerZcash
cd OptiminerZcash
tar -xf optiminer-zcash-1.7.0.tar.gz
mv optiminer-zcash-1.7.0/optiminer-zcash ~/optiminer
cd ~
```

Now that we have optiminer, we have to find a good pool to mine, I like <a href="https://bitfire.one/"> Bitfire </a> so we'll use that. First we have to configure our miner to mine at bitfire.
```Shell
cd ~/optiminer
nano mine.sh
```
This will open up a commandline text editor, you can use the arrow keys to move up and down. replace `POOL=zstratum+tls://eu1-zcash.flypool.org:3443` with `zstratum+tls://pool.bitfire.one:3000`.

Then replace `USER=t1Yszagk1jBjdyPfs2GxXx1GWcfn6fdTuFJ.worker` with the zen address you created eariler with a worker name after a dot like `USER=znUg7EiY9R71gXMZC96k3naYiTegtD2enYC.rig1`.

After that, do ctrl+x, then hit y. This will save the script, to start mining do, `./mine.sh`.

Congrats, You have started mining and will recieve your payments, to use the commandline wallet, check out https://github.com/zcash/zcash/wiki/1.0-User-Guide 
