----------------------------部署 ERC20----------------------------
BSC -> PLGR: 0x22E6f32805d2AC7F787ca72b2F0bdbCE1693573b
部署账号：
0x8B8494cDAF423fAEB446F1a31697663eCA30690e
d355ce1b91b16a0fc6953cc20ec75e19060487a1a157679819d68595bc1e7ca3

---

ETH(reposten) -> MPLGR: 0xb7d51b050f2072C2855B21579bB61955Cb484a97
部署账号：
B-Ropsten
0x6e4f03a24CAec5D18fbA1c1eC78a5e1Ff6146028
0f6a853f71a5da0c4953de181283948f343e2f5e6471fbcd4e5d2606fa7af7fb

---

***部署chainbridge***
BSC
```shell
cb-sol-cli --url $SRC_GATEWAY --privateKey $SRC_PK --gasPrice 100000000000 deploy \
    --bridge --genericHandler \
    --relayers $SRC_ADDR \
    --relayerThreshold 3\
    --chainId 0
```

ETH(ropsten)
```shell
cb-sol-cli --url $DST_GATEWAY --privateKey $DST_PK --gasPrice 10000000000 deploy\
    --bridge --genericHandler \
    --relayers $SRC_ADDR \
    --relayerThreshold 3\
    --chainId 1
```

---

更新 config，启动docker
```shell
cd relayers
docker-compose up -d 
```

---------------------------------------以上内容不需要修改----------------------------------------------
***每次更新合约代码后，只要更新注册PledgerBridgeBSC/ETH 就可以。

***当前BRIDGE合约***
```shell

BSC Bridge: 0xd6169DF58c6886D354A2eA93391D1E0F222D5080
ETH Bridge: 0xe7f99495EAcC53d6B4bd5FC2B08387F4f32Af54a
```

代码如下：

***注册BSC***
RESOURCE_ID=0x000000000000000000000000000000c76ebe4a02bbc34786d860b355f5a5ce10
SRC_GATEWAY=https://data-seed-prebsc-1-s1.binance.org:8545
SRC_PK=d355ce1b91b16a0fc6953cc20ec75e19060487a1a157679819d68595bc1e7ca3
SRC_BRIDGE=0x0D52858bc128D056570e0E73C695eeC0bb3d7E04
SRC_HANDLER=0x4E053d46122721b3Ec194b7248Cb4270c45e52eA

```shell
cb-sol-cli --url $SRC_GATEWAY --privateKey $SRC_PK --gasPrice 10000000000 bridge register-generic-resource \
    --bridge $SRC_BRIDGE \
    --handler $SRC_HANDLER \
    --resourceId $RESOURCE_ID \
    --execute 0x02c0ab3b \
    --targetContract 0xd6169DF58c6886D354A2eA93391D1E0F222D5080
```


***注册ETH***

DST_GATEWAY=https://ropsten.infura.io/v3/9aa3d95b3bc440fa88ea12eaa4456161
DST_PK=0f6a853f71a5da0c4953de181283948f343e2f5e6471fbcd4e5d2606fa7af7fb
DST_BRIDGE=0x909882A2a12157148331957baC08eDbc06C1f4F2
DST_HANDLER=0x3629cCFf769D3A29886fdE4be3777287AAF31337
RESOURCE_ID=0x000000000000000000000000000000c76ebe4a02bbc34786d860b355f5a5ce10

```shell
cb-sol-cli --url $DST_GATEWAY --privateKey $DST_PK --gasPrice 10000000000 bridge register-generic-resource \
    --bridge $DST_BRIDGE \
    --handler $DST_HANDLER \
    --resourceId $RESOURCE_ID \
    --execute 0x02c0ab3b \
    --targetContract 0xe7f99495EAcC53d6B4bd5FC2B08387F4f32Af54a
```



