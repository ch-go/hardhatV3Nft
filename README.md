项目介绍

---
本项目使用了hardhat v3的多个插件.包括使用configvariable获取环境变量,forge test做solidity的单元测试,hardhat igniton做deploy和verify,合约升级.
MetaNFTAuction由管理员开启拍卖,bidder必须固定使用eth或者usdc参与拍卖,如果不同拍卖者使用eth和usdc,使用chainlink的预言机统一转为法币dollar对比,最高的纪录highestbidder,拍卖结束时由管理员去转移nft,拍卖只记录最后的赢家.如果没有拍卖到或者多次叫价,拍卖结束时需要bidder主动去提款.
1. 合约升级参考文档地址为
合约升级
2. sepolia已部署合约地址参考igniton/deployments/deployed_addresses.json
3. sepolia使用configvarialbe设置环境变量SEPOLIA_RPC_URL,SEPOLIA_PRIVATE_KEY,SEPOLIA_ETHERSCAN_API_KEY参考
use configvariable
4. 测试合约
forge test --match-contract MetaNFTAuction --fork-url https://sepolia.infura.io/v3/123 -vvv   
5. 查看覆盖率
forge coverage --match-contract MetaNFTAuction --fork-url https://sepolia.infura.io/v3/123 -vvv
╭--------------------------------+-----------------+-----------------+----------------+---------------╮
| File                           | % Lines         | % Statements    | % Branches     | % Funcs       |
+=====================================================================================================+
| contracts/MetaNFT.sol          | 30.00% (3/10)   | 33.33% (2/6)    | 0.00% (0/4)    | 25.00% (1/4)  |
|--------------------------------+-----------------+-----------------+----------------+---------------|
| contracts/MetaNFTAuction.sol   | 81.48% (66/81)  | 80.52% (62/77)  | 60.00% (27/45) | 80.00% (8/10) |
|--------------------------------+-----------------+-----------------+----------------+---------------|
| contracts/MetaNFTAuctionV2.sol | 0.00% (0/89)    | 0.00% (0/87)    | 0.00% (0/46)   | 0.00% (0/11)  |
|--------------------------------+-----------------+-----------------+----------------+---------------|
| Total                          | 38.33% (69/180) | 37.65% (64/170) | 28.42% (27/95) | 36.00% (9/25) |
╰--------------------------------+-----------------+-----------------+----------------+---------------╯
6. 部署并验证
npx hardhat ignition deploy ignition/modules/MetaNFTAuctionProxyModule.ts --network sepolia --verify
npx hardhat ignition deploy ignition/modules/MetaNFTAuctionUpgradeModule.ts --network sepolia --verify

