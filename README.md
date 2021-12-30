# bridge-relayers

***KEEP THIS REPO PRIVATE***

----------------------------部署 ERC20----------------------------  
BSC -> PLGR: 0x22E6f32805d2AC7F787ca72b2F0bdbCE1693573b  
部署账号：  
0x8B8494cDAF423fAEB446F1a31697663eCA30690e  
d355ce1b91b16a0fc6953cc20ec75e19060487a1a157679819d68595bc1e7ca3  

---  

ETH(reposten) -> MPLGR: 0x550ea36E01Ada1d6dEd5fEfeA30E70aCA9275051  
部署账号：  
0xeBbA8791452310089D24DA37b64e57ab109D896e  
b11b48b81c7a3ef0b259e81cdbb36b9d3d5c4e377cbec6dba03dd5e03425b7c9  

---------------

truffle deploy --network bsc  
 
PledgerBridgeBSC:  
0xA7B8730296a218e96FB251A9B52f82D8c1Bc8bd4  

---

truffle deploy --network reposten  
PledgerBridgeETH:  
0xcEF309b52F3B35f1853b60aFad3825188c0CB9cB  


---- relayer 注册 ----  
PLGR=0x22E6f32805d2AC7F787ca72b2F0bdbCE1693573b  

RESOURCE_ID=0x000000000000000000000000000000c76ebe4a02bbc34786d860b355f5a5ce10  
SRC_GATEWAY=https://data-seed-prebsc-1-s1.binance.org:8545  
SRC_PK=d355ce1b91b16a0fc6953cc20ec75e19060487a1a157679819d68595bc1e7ca3  
SRC_BRIDGE=0x0D52858bc128D056570e0E73C695eeC0bb3d7E04  
GENERIC_HANDLER_ADDRESS=0x4E053d46122721b3Ec194b7248Cb4270c45e52eA  

注册 BSC   
```shell
cb-sol-cli --url $SRC_GATEWAY --privateKey $SRC_PK --gasPrice 10000000000 bridge register-generic-resource \
    --bridge $SRC_BRIDGE \
    --handler $GENERIC_HANDLER_ADDRESS \
    --resourceId $RESOURCE_ID \
    --execute 0x02c0ab3b \ // PledgerBridgeBSC的deposit_mplgr_bridge
    --targetContract 0xA7B8730296a218e96FB251A9B52f82D8c1Bc8bd4  // PledgerBridgeBSC 合约地址
```

注册 ETH  
```shell
DST_GATEWAY=https://ropsten.infura.io/v3/acb534b53d3a47b09d7886064f8e51b6
DST_PK=b11b48b81c7a3ef0b259e81cdbb36b9d3d5c4e377cbec6dba03dd5e03425b7c9
DST_BRIDGE=0x0C4DD68A014B58e0DDD590Bb014b0f7E71D2DaF4
DST_GENERIC_HANDLER=0x361F5886C42c631A241b1fE29f6BbfEf800B021f
RESOURCE_ID=0x000000000000000000000000000000c76ebe4a02bbc34786d860b355f5a5ce10

cb-sol-cli --url $DST_GATEWAY --privateKey $DST_PK --gasPrice 10000000000 bridge register-generic-resource \
    --bridge $DST_BRIDGE \
    --handler $DST_GENERIC_HANDLER \
    --resourceId $RESOURCE_ID \
    --execute 0x02c0ab3b \  // PledgerBridgeETH的deposit_mplgr_bridge
    --targetContract 0xcEF309b52F3B35f1853b60aFad3825188c0CB9cB  // PledgerBridgeETH 的合约地址
```

---

Done.
