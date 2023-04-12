
# bsc-snapshots


## Database after Ancient Data Prune:

Ancient Data Prune is a new feature in [bsc v1.1.8](https://github.com/binance-chain/bsc/releases/tag/v1.1.8)


### Endpoint


[geth-20230409.tar.lz4
](https://pub-c0627345c16f47ab858c9469133073a8.r2.dev/geth-20230409.tar.lz4)





## Snapshots Provided by Community

Special thanks to [BNB48Club](https://twitter.com/bnb48club) on contributing another dump of snapshot, you can also refer [here](https://github.com/BNB48Club/bsc-snapshots) to download.



### Usage 

Step 1: Preparation
- Make sure your hardware meets the [suggested requirement](https://docs.binance.org/smart-chain/developer/fullnode.html).
- A disk with enough free storage, at least twice the size of the snapshot.

Step 2: Download && Uncompress
- Copy the above snapshot URL.
- Download:  `wget -O geth.tar.lz4  "<paste snapshot URL here>"` . It will take one or two hours to download the snapshot, you can put it in the backgroud by `nohup wget -O geth.tar.gz  "<paste snapshot URL here?" &`


*If you need to speedup download, just use `aria2c`*
```
aria2c -o geth.tar.lz4 -s14 -x14 -k100M https://download.bsc-snapshot.workers.dev/{filename} -o geth.tar.lz4
```

Tips: if you do not have aria2c yet, you may install it by:
```
sudo su -
yum install -y gcc-c++
yum install -y openssl-devel
wget https://github.com/aria2/aria2/releases/download/release-1.36.0/aria2-1.36.0.tar.gz
tar -zxvf aria2-1.36.0.tar.gz
cd aria2-1.36.0
## some dependencies should be met before compile aria2c, such as gcc, g++
./configure ARIA2_STATIC=yes
make -j8
make install
```

But aria2c may fail sometimes, you need to rerun the download command. To make it easy, we provide a script: [aria2c_download.sh](script/aria2c_download.sh)
```
# download to the current folder:
aria2c_download.sh https://download.bsc-snapshot.workers.dev/{filename}
# download to a specific folder(/data):
aria2c_download.sh https://download.bsc-snapshot.workers.dev/{filename} /data
```


- Uncompress: `tar -I lz4 -xvf geth.tar.lz4`. It will take more than two hours to uncompress. You can put it in the backgroud by `nohup tar -I lz4 -xvf geth.tar.lz4 &`
- You can combine the above steps by running a script:
```
wget -O geth.tar.lz4  "<paste snapshot URL here>"
tar -I lz4 -xvf geth.tar.lz4
```


- If you do not need to store the archive for use with other nodes, you may also extract it while downloading to save time and disk space:
```
wget -q -O - <snapshot URL> | tar -I lz4 -xvf -
```


Step 3: Replace Data
- First, stop the running bsc client if you have one by `kill {pid}`, and make sure the client has shut down.
- Consider backing up the original data: `mv ${BSC_DataDir}/geth/chaindata ${BSC_DataDir}/geth/chaindata_backup; mv ${BSC_DataDir}/geth/triecache ${BSC_DataDir}/geth/triecache_backup`
- Replace the data: `mv server/data-seed/geth/chaindata ${BSC_DataDir}/geth/chaindata; mv server/data-seed/geth/triecache ${BSC_DataDir}/geth/triecache`
- Start the bsc client again and check the logs


## Erigon-BSC Snapshot

> erigon version [v2.40.0-dev-3da15fcb](https://github.com/node-real/bsc-erigon/releases/tag/v1.0.2)
### Endpoint
[erigon_data_20230410.tar.lz4](https://site4-dex-qa-logs.s3.amazonaws.com/erigon-0410.tar.lz4?AWSAccessKeyId=ASIA56JS342UEG5DKZHI&Expires=1681901120&x-amz-security-token=IQoJb3JpZ2luX2VjENP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaDmFwLW5vcnRoZWFzdC0xIkcwRQIgZhfhV8W5qD6CByUhlTL8%2BlDyQSRw9sxMhFi04CXhlTQCIQDX4SCfgbbhfEr%2B06SyuI%2BzpYe9Gdc4lMWGOq0f27ZyQyrTBQi8%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAIaDDk1ODQyMTI2NDA0MCIMUnfKhlyNlR7gUQ3%2FKqcFK0L3HYm9EsA2IbZag0J8nBrX%2FR5aiklVrIv7e7ZWhEtj7jQ1mBdsPZX0yWdwpqKAaHHGn9OUAC6gXVMSE8xO%2BKh5kuzP4uprtRbUzMu9E9NigtZWsBcQX2wnDcTwjY5o5gOPmf5uGqxLBC%2FuN99opGruymCqFlNBWkoe%2FoxS7nNX%2B5aXJssrcuFem3sP4%2FNcN8W5mqHg7vNT%2BYauG%2BHwqq6hqmjJYvb8bY2%2F1I7LKpapuKLbz4Mu58QMWE4rA5Po58JBfEJasNNvGRKDYeX8EgEkogRDyNTlqMEoZu99sBNEPO02APGGqC7F11tVk7sIPcfOd04YJkkdQq3TWgDY8t6n%2Ft5w1WjZDXiGKbMpbXKaE9MTjngdWSvaibyCuid3TLdW91Lp8S4wlmQ1C%2FJtletX384KLz7V%2FRkJXqTK18OKhzwUD6PwyYgqdbG62QsKmwmtpaH1NwK3OWXkBHTUcNNfE0wlWKGn6%2BQDT158yjTYHvrozauT%2B4LfJKgrbvtrCMZ%2F3vAcGoKngDcx9gG7eKWhywuuoUf1IgclZ8EHbXDEX9LD%2Ft28uTKmpXSK4D%2F%2Fm5swtQaXrWSHooe9eRUW7BGVdmUKoXx0cV4TVCpIpoLByTRbezkSIuRIH1KNKDXkp5qzD3mBu%2FXi%2FFkt0E8xWEU89IzjoFIlXXddGfroEgo3TNlVkjGsGxKQsUpVIfn7v0oqThJGlWMXOqPH2oYirl4eqFgCHbOr%2BQwdU7lwo4yNfJaQA4JS5pJr7A0LKBBdQpx6X18IqNGwLtuUBZT8Ca7WJXRKlqjSdd85SuoT%2BvHhQxO505dTBI7I96tE%2FWHInv%2FJp4rJzYya8VlEX53oXXS02Z6rHwSKcGzmbXOp8u6qMuQwhIob2puhMWM91ymhwNqfM%2BuhFTClldqhBjqxAYJCBPLxRktP4IVPCsrB4O5ypnAbwVApoiAe1zQqzoHlfFmHkhnBJptWS%2FpDfjLlDjj%2F4rIlTA3gDZ5uYVFD0sf9grCW8ki1vxoK1xYzj36Omd6HYN00CnMZrktkmaMDoo03XExBy62kFnSGgnRAPGoCPFJLt%2BRbPxcCS6WadV4JkDePXByRnoYDuSZX7EIBKh6HT%2F3CUwRM8js1zazRDmCJTRH9fHwAtvc24z6CF9xY3w%3D%3D&Signature=ak9Pg1IyNW535yWpIbvV5tqGjxY%3D
)

### Usage

Step 1: Preparation

- Make sure your hardware meets the [suggested requirement](https://github.com/ledgerwatch/erigon#system-requirements).
- BSC Archive: 7TB+. BSC Full: 1TB.

Step 2: Download && Uncompress

```
sudo yum install aria2c
aria2c -s14 -x14 -k100M https://pub-60a193f9bd504900a520f4f260497d1c.r2.dev/{filename} -o erigon.tar.lz4
tar -I lz4 -xvf {filename}
```
Step 3: Replace Data And Restart erigon
- Stop the running erigon client by `kill {pid}`
- Backing up the original data: `mv ${erigon_datadir}/ ${erigon_datadir_back}`
- Replace the data: `mv ${erigon_snapshot_dir}/data/ ${erigon_datadir}/`
- Start the erigon client again and check logs

shell command example:
```
nohup ${erigon_dir/}/build/bin/erigon --bodies.cache=214748364800 --batchSize=4096M --db.pagesize=16k --datadir ${erigon_dir/data}--private.api.addr=localhost:9090 --chain=bsc --metrics 2>&1 &
```


