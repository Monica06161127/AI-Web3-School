---
timezone: UTC+8
---

# QingQiuGeek

**GitHub ID:** QingQiuGeek

**Telegram:** @qingqiugeek

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->
今天学了the graph。

\[官网\]([https://thegraph.com/docs/en/subgraphs/quick-start/](https://thegraph.com/docs/en/subgraphs/quick-start/))

\`\`\`bash

npm install -g @graphprotocol/graph-cli@latest

graph init

npm install

graph codegen

graph build

graph auth <DEPLOY\_KEY>

graph deploy <SUBGRAPH\_SLUG>

\`\`\`

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/QingQiuGeek/images/2026-05-19-1779196582805-image.png)

**\## 踩坑**

name中是下划线\\\_，但是在slug中则是-

![image-1.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/QingQiuGeek/images/2026-05-19-1779196568013-image-1.png)

  

本地graph init创建的name要和studio的一致，否则最后部署会出现

\`\`\`

× Failed to deploy to Graph node [https://api.studio.thegraph.com/deploy/](https://api.studio.thegraph.com/deploy/): Subgraph not found

\`\`\`

部署后  

![image-4.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/QingQiuGeek/images/2026-05-19-1779196542721-image-4.png)

deploy 后：自己已经可以查，也可以接应用做开发/演示

publish 后：别人也能把它当正式网络服务来用
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->

今天学了 foundry的模糊测试、不变量测试、差异测试

\## 模糊测试  
  
模糊测试让测试框架自动生成大量随机输入，反复运行测试函数，以发现边界条件下的 bug。  
  
\`\`\`solidity  
pragma solidity 0.8.10;  
  
import {Test} from "forge-std/Test.sol";  
  
contract Safe {  
receive() external payable {}  
  
function withdraw() external {  
payable(msg.sender).transfer(address(this).balance);  
}  
}  
  
contract SafeTest is Test {  
Safe safe;  
  
receive() external payable {}  
  
function setUp() public {  
safe = new Safe();  
}  
// 自动为 uint256 生成：0, 1, MAX\_UINT, 随机大数、小数等，任何一次运行 revert 或断言失败 → 整个测试失败，默认运行256次  
function testFuzz\_Withdraw(uint256 amount) public {  
payable(address(safe)).transfer(amount);  
uint256 preBalance = address(this).balance;  
safe.withdraw();  
uint256 postBalance = address(this).balance;  
assertEq(preBalance + amount, postBalance);  
}  
//testFuzz\_Withdraw测试结果是失败，因为测试合约的默认以太币数量是 2\*\*96 wei（在 DappTools 中），所以必须将 amount 类型限制为 uint96 ，以确保我们不会尝试发送超过uint96的值，如下：  
  
function testFuzz\_Withdraw(uint96 amount) public {  
payable(address(safe)).transfer(amount);  
uint256 preBalance = address(this).balance;  
safe.withdraw();  
uint256 postBalance = address(this).balance;  
assertEq(preBalance + amount, postBalance);  
}  
}  
  
\`\`\`  
  
\### 模糊测试固定  
  
当你想确保一组特定的值被用作模糊参数的输入时，可以定义模糊测试固定装置。这些固定装置可以在测试中被声明为：  
  
\- 以 fixture 为前缀的存储数组，后跟要进行模糊处理的参数名称。例如，要用于模糊处理 uint32 类型的参数 amount 的固定装置可以定义如下：  
  
\> uint32\[\] public fixtureAmount = \[1, 5, 555\];  
  
\- 以 fixture 为前缀命名的函数，后跟要进行模糊处理的参数名称。\*\*函数应返回一个（固定大小或动态的）数组\*\*，作为模糊处理所需的值。例如，要用于模糊处理名称为 owner 的 address 类型的参数的固定装置可以定义为具有以下签名的函数：  
\> function fixtureOwner() public returns (address\[\] memory)  
  
如果提供的固定值的类型与要进行模糊处理的命名参数的类型不一致，则会被拒绝并引发错误。  
  
\## 不变量测试  
  
无论系统如何变化（执行任意操作序列），某些“不变性质”必须始终成立。  
  
Foundry 会随机组合 transferToUser1, transferBetweenUsers, burnFromOwner 等操作（例如：先转 100，再 burn 50，再转 200...），每执行几步，就检查一次 invariant\_XXX 是否成立  
，如果任何一次不成立 → 测试失败，并输出导致失败的操作序列，如下:  
  
\`\`\`solidity  
// SPDX-License-Identifier: MIT  
pragma solidity ^0.8.13;  
  
import {Test} from "forge-std/Test.sol";  
import "./MyToken.sol"; // 假设这是 ERC20 合约  
  
contract TokenInvariantTest is Test {  
MyToken token;  
address owner = address(this);  
address user1 = makeAddr("user1");  
address user2 = makeAddr("user2");  
  
uint256 initialSupply = 10000 ether;  
  
function setUp() public {  
token = new MyToken("Test", "TST", initialSupply);  
vm.label(address(token), "Token");  
vm.label(user1, "User1");  
vm.label(user2, "User2");  
}  
  
// ===== 操作函数（Fork 的“动作”）=====  
function transferToUser1(uint256 amount) public {  
vm.assume(amount <= token.balanceOf(owner));  
token.transfer(user1, amount);  
}  
  
function transferBetweenUsers(uint256 amount) public {  
vm.assume(amount <= token.balanceOf(user1));  
vm.prank(user1);  
token.transfer(user2, amount);  
}  
  
function burnFromOwner(uint256 amount) public {  
vm.assume(amount <= token.balanceOf(owner));  
token.burn(amount);  
}  
  
// ===== 不变量断言（必须永远成立）=====  
  
// 不变量 1：总供应量 = 所有账户余额之和  
function invariant\_totalSupplyEqualsSumOfBalances() public {  
uint256 totalBalance = token.balanceOf(owner)  
\+ token.balanceOf(user1)  
\+ token.balanceOf(user2);  
assertEq(token.totalSupply(), totalBalance);  
}  
  
// 不变量 2：余额永不为负（Solidity 保证，但可显式检查）  
function invariant\_balancesNonNegative() public {  
assertGe(token.balanceOf(owner), 0);  
assertGe(token.balanceOf(user1), 0);  
assertGe(token.balanceOf(user2), 0);  
}  
}  
\`\`\`  
  
\## 差异测试  
  
对同一输入，两个不同实现（或不同环境）应产生相同输出。如果不一致，说明至少有一个实现有 bug。常用于：  
  
\- 验证新实现 vs 老实现  
  
\- 验证优化版 vs 原始版  
  
\- 验证 L2 合约 vs 主网行为  
  
Forge 用大量随机 x 值调用 testDifferential\_Sqrt，如果 MyMath.sqrt(100) = 10，但 Math.sqrt(100) = 9 → 立即失败  
  
\`\`\`solidity  
// SPDX-License-Identifier: MIT  
pragma solidity ^0.8.13;  
  
import {Test} from "forge-std/Test.sol";  
import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";  
  
// 自定义 sqrt 实现（可能有 bug）  
library MyMath {  
function sqrt(uint256 x) internal pure returns (uint256) {  
if (x == 0) return 0;  
uint256 z = (x + 1) / 2;  
uint256 y = x;  
while (z < y) {  
y = z;  
z = (x / z + z) / 2;  
}  
return y;  
}  
}  
  
contract DifferentialTest is Test {  
// 差异测试：比较 MyMath.sqrt 和 OpenZeppelin Math.sqrt  
function testDifferential\_Sqrt(uint256 x) public {  
// 限制输入范围（避免溢出或无效值）  
vm.assume(x <= type(uint128).max);  
  
uint256 result1 = MyMath.sqrt(x);  
uint256 result2 = Math.sqrt(x);  
  
// 关键：两者结果必须一致！  
assertEq(result1, result2, "sqrt implementations differ");  
}  
}  
\`\`\`
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
