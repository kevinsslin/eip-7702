---
timezone: UTC+8
---

> 请在上边的 timezone 添加你的当地时区(UTC)，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区

# Tofu

1. 自我介绍：本人拥有半年的区块链资金追踪工作经验。
2. 你认为你会完成本次残酷学习吗？会
3. 你的联系方式（推荐 Telegram）：@blahole

## Notes

<!-- Content_START -->

### 2025.05.14
#### 账户抽象的背景和动机
1. 外部拥有账户（Externally Owned Accounts, EOAs）是以太坊区块链中最基础的账户类型，由用户通过私钥直接控制。与智能合约账户（Contract Accounts, 
CAs）不同，EOAs的功能较为简单，主要用于发起交易、转账以太币（ETH）以及与智能合约交互。
2. 智能合约账户（Contract Accounts, CAs）是以太坊区块链中的一种账户类型，与外部拥有账户（Externally Owned Accounts, EOAs）相对。与EOAs由私钥控制不同，CAs由部署在区块链上的智能合约代码控制，具备高度的可编程性和灵活性，能够实现复杂的逻辑和自动化操作。
3. 账户抽象（Account Abstraction）  
   * 账户抽象是以太坊生态系统中的一个重要概念，旨在通过改进账户模型，增强以太坊的灵活性、安全性和用户体验。它试图模糊以太坊中外部拥有账户（Externally Owned Accounts,
   EOAs）和智能合约账户（Contract Accounts, CAs）之间的界限，使所有账户都具有可编程性，从而实现更复杂的交易逻辑、更低的使用门槛和更强的安全性。  
   * 以太坊账户抽象通过赋予所有账户可编程性，重塑了用户体验、安全性和开发者灵活性。ERC-4337和EIP-7702
   作为核心实现路径，分别通过链下基础设施和协议级修改推动了这一目标。账户抽象的优势包括简化操作、增强安全性、支持创新和金融包容性，但也面临安全风险、Gas成本和生态迁移等挑战。  
   * 账户抽象被认为是实现以太坊“终极账户抽象”（Endgame Account Abstraction）的关键步骤，最终目标是让所有账户默认具备智能合约功能，同时保持简单性和低成本。

### 2025.05.15
#### 深入了解账户抽象
1. 账户抽象的核心概念  
账户抽象的核心是将账户的验证逻辑和执行逻辑从协议层面下放到用户定义的智能合约层面。具体来说，它允许用户自定义以下方面：

   - 验证逻辑（Signature Verification）  
传统EOAs依赖ECDSA签名验证，账户抽象允许用户定义任意验证机制，例如：  
多重签名（Multi-Sig）：需多个密钥持有人同意。  
替代签名方案：如Schnorr签名、WebAuthn、手机通行密钥。  
无私钥验证：如基于生物识别或零知识证明（ZKP）。  
这种灵活性提高了安全性和用户体验，支持量子抗性签名等未来技术。  

   - 执行逻辑（Execution Logic）  
账户抽象允许用户定义交易的执行方式，例如：  
批量交易（Batching）：将多个操作（如授权、转账）合并为单笔交易，减少Gas费用和用户交互。  
权限控制（Spending Controls）：设置交易限制，如每日转账上限或特定DApp的代币支出额度。  
自动化操作：支持订阅支付、定投（DCA）、自动申领空投等。  

   - Gas支付灵活性  
传统EOAs要求用户支付Gas费用（需持有ETH），账户抽象允许：
Gas赞助（Gas Sponsorship）：第三方（如DApp或钱包提供商）支付Gas费用。
支付代币多样化：允许用ERC-20代币（如USDC）支付Gas。
这降低了新用户进入门槛，提升了金融包容性。

   - 社交恢复（Social Recovery）  
账户抽象支持用户指定“守护者”（如朋友、家人）或恢复机制（如多签），在私钥丢失时恢复账户。无需创建新地址或迁移资产，简化了恢复流程。  

   - 协议级抽象  
账户抽象将账户逻辑从以太坊协议（EVM）中解耦，交给智能合约处理，减少对核心协议的修改，保持兼容性。  
     

2. 账户抽象的实现路径  
以太坊社区通过多个提案和标准推动账户抽象，主要包括ERC-4337、EIP-7702（替代EIP-3074）等。以下是详细介绍：  
   
   - EIP-2938：提议将账户抽象直接集成到以太坊协议，引入原生支持（需重大协议修改，短期内未采纳）。

   - EIP-3074（2020年提出，已被EIP-7702替代）：引入AUTH和AUTHCALL操作码，允许EOAs授权智能合约执行交易。

   - ERC-4337（2023年发布）：ERC-4337是一种通过链下基础设施实现账户抽象的标准，无需修改以太坊协议。引入“用户操作”（User Operations, UserOps）：用户发送包含自定义逻辑的交易请求。

   - ERC-7201：定义命名空间标准，防止存储冲突。

   - EIP-7702（2024年提出，替代EIP-3074）：EIP-7702是账户抽象的最新进展，旨在通过协议级修改增强EOAs功能，已纳入Pectra升级（预计2025年5月上线）。

   - ERC-7779（草案）：标准化重新委托流程，优化EIP-7702实现。


3. 账户抽象的优势  
   - 用户体验提升：
批量交易和Gas赞助简化操作，降低Gas费用。
无需持有ETH即可交易，吸引新用户。
社交恢复和权限控制降低资产丢失风险。

   - 安全性增强：
自定义验证逻辑支持多签、WebAuthn等，减少私钥依赖。
权限控制防范钓鱼攻击和未经授权的支出。
未来可支持量子抗性签名。

   - 开发者灵活性：
开发者可设计复杂交互逻辑，如自动化的DeFi策略、NFT竞标、链上游戏。
支持AI代理操作，如自动优化投资组合。

   - 生态整合：
EIP-7702和ERC-4337的兼容性减少了生态碎片化。
支持跨链统一余额和与传统金融系统的整合。

   - 金融包容性：
Gas赞助和支付代币多样化降低了使用门槛，吸引新兴市场用户。


4. 账户抽象的挑战与风险
   - 安全风险：
恶意合约：授权的智能合约可能包含漏洞或恶意逻辑，需严格审计。
钓鱼攻击：用户可能被诱导签名恶意授权，导致资金全损。
存储冲突：重新委托时，合约存储结构不兼容可能导致账户锁定（可通过ERC-7201缓解）。

   - Gas成本：
对于简单转账，账户抽象的Gas成本高于传统EOA（EIP-7702约增加50%）。
复杂逻辑（如权限检查）可能显著增加Gas费用。

   - 基础设施依赖：
ERC-4337依赖打包者和中继者，可能引入中心化风险或单点故障。
需开发者和钱包广泛支持新交易类型（如EIP-7702）。

   - 用户教育：
普通用户可能难以理解授权签名和智能合约的风险。
需钱包提供直观的界面和安全提示。

   - 生态迁移：
现有DApp和钱包需更新以支持账户抽象，短期内可能面临兼容性问题。
社区需协调标准（如ERC-7201、ERC-7779）以确保一致性。
     

5. 账户抽象的未来  
账户抽象是以太坊迈向主流采用的关键技术，其未来发展方向包括：

   - Pectra升级（2025年5月）：
EIP-7702将作为核心组件上线，预计显著提升EOA功能。
其他提案（如EIP-7251）可能进一步优化账户逻辑。

   - 标准化与互操作性：
ERC-7201、ERC-7779等标准将确保存储安全和重新委托的可靠性。
跨链签名标准可能进一步统一多链生态。

   - 用户教育与安全：
钱包需开发直观的界面，提示授权风险。
社区需推广合约审计和安全最佳实践。

   - AI与链上自治：
账户抽象将推动AI驱动的链上代理，开启去中心化自治组织（DAO）的新篇章。

   - 量子抗性：
账户抽象支持的自定义签名方案为以太坊应对量子计算威胁提供了基础。
     

### 2025.05.16
#### ERC-4337

ERC-4337 是一个以太坊标准，旨在通过链下基础设施实现账户抽象（Account Abstraction, AA），无需修改以太坊核心协议。它于 2023 年 3 月正式部署到以太坊主网，通过引入“用户操作”（User Operations, UserOps）、入口点（EntryPoint）合约和打包者（Bundlers）等机制，赋予账户可编程性，提升用户体验、安全性和开发者灵活性。ERC-4337 被视为以太坊账户抽象的重要里程碑，与 EIP-7702 一起推动了“终极账户抽象”（Endgame Account Abstraction）的实现。
在 ERC-4337 之前，账户抽象的尝试（如 EIP-3074）因需要修改以太坊协议或引入新操作码（如 AUTH 和 AUTHCALL）而受阻。ERC-4337 的创新在于通过链上智能合约和链下基础设施实现账户抽象，无需硬分叉或协议变更，部署迅速，已在主网广泛应用。

1. ERC-4337 的核心机制  
   
   - 核心组件

     - 用户操作（User Operations, UserOps）：  
         * UserOp 是一个数据结构，包含用户的交易意图（如调用数据、Gas 限制、签名）。它不是标准的以太坊交易，而是通过链下网络提交。  
         - 格式：sender, nonce, initCode, callData, callGasLimit, verificationGasLimit, preVerificationGas, maxFeePerGas, 
       maxPriorityFeePerGas, paymasterAndData, signature。  
         - 作用：定义账户的执行逻辑（如转账、合约调用）和验证方式。    
     - 打包者（Bundlers）：  
         - 链下节点，负责收集 UserOps，验证其有效性（如签名和 Gas 可用性），并将其打包为标准以太坊交易，提交到入口点合约。
         - 类似矿工或验证者，需运行以太坊全节点或 RPC 节点。  
         - 激励：通过 Gas 费用或支付者合约的奖励获利。  
     - 入口点（EntryPoint）合约：  
         一个全局的智能合约，地址固定（如主网为 0x5FF137D4b0FDCD49DcA30c7CF57E578a026d2789），负责处理 UserOps 的验证和执行。  
         功能：
         - 验证 UserOp 的签名和支付者逻辑。
         - 执行 UserOp 的调用数据（callData）。
         - 处理 Gas 支付和退款。
         入口点标准化了账户抽象流程，确保钱包和 DApp 的互操作性。  
     - 支付者（Paymasters）：  
         智能合约，负责支付 UserOp 的 Gas 费用，支持 Gas 赞助。  
         类型：  
         - DApp 提供的支付者，为用户补贴 Gas。  
         - 代币支付者，允许用户用 ERC-20 代币（如 USDC）支付 Gas。  
         - 第三方支付者，如钱包服务商。  
         支付者需验证 UserOp 的合法性，并与入口点交互完成 Gas 支付。  
     - 智能合约账户（Smart Contract Wallets）：  
       - 用户部署的智能合约，定义账户的验证逻辑（如多重签名、时间锁）和执行逻辑。
       - 与传统 EOA 不同，智能合约账户由代码控制，支持复杂功能。
     - 聚合器（Aggregators）：  
       - 可选组件，优化签名验证。例如，多个 UserOps 的签名可以通过聚合器批量验证，降低 Gas 成本。
       - 常见实现：基于 BLS 签名的聚合。
   
   - 执行流程

     - 用户生成 UserOp：    
      用户通过钱包（如 MetaMask、Safe）创建 UserOp，指定调用数据、Gas 限制和签名。  
      如果是新账户，UserOp 包含 initCode 用于部署智能合约账户。  

     - UserOp 提交：  
      UserOp 通过链下网络（如 P2P 或 RPC）发送到打包者。  
      打包者验证 UserOp 的签名、Gas 可用性和支付者逻辑。  

     - 打包与提交：  
      打包者将多个 UserOps 合并为一个以太坊交易，调用入口点合约的 handleOps 函数。  
      交易格式：from: Bundler, to: EntryPoint, data: handleOps(UserOps[])。  

     - 入口点处理：  
      入口点合约验证每个 UserOp 的签名和支付者逻辑。  
      执行 UserOp 的 callData，触发智能合约账户或其他目标合约。  
      处理 Gas 支付，可能从支付者合约扣款。  

     - 链上记录：  
      链上记录显示为打包者调用入口点合约，资金流和操作细节隐藏在 UserOp 的 callData 中。  

   - Gas 模型  
      - ERC-4337 引入了多层次 Gas 机制：  
        - callGasLimit：执行 UserOp 的调用数据所需的 Gas。  
        - verificationGasLimit：验证签名和支付者逻辑的 Gas。  
        - preVerificationGas：链下预验证和打包的 Gas（如网络传输成本）。  
      - 支付者或用户需预存 ETH 或代币，确保 Gas 支付。入口点合约退还多余 Gas。  

2. 功能

   - 可编程验证：
支持自定义签名方案，如多重签名、WebAuthn、硬件安全模块（HSM）或生物识别。
例如，一个账户可以要求 3 个签名中的 2 个同意，或结合面部识别和密码。

   - 批量交易：
多个操作（如授权、转账、兑换）合并为单笔 UserOp，减少 Gas 成本和用户交互。
示例：用户可以在一次签名中完成 ERC-20 的 approve 和 Uniswap 的 swap。

   - Gas 赞助：
支付者合约允许 DApp 或第三方支付 Gas 费用，用户无需持有 ETH。
支持代币支付 Gas（如 USDC），支付者合约处理兑换。

   - 社交恢复：
账户可以通过信任人或多重签名恢复，无需迁移到新地址。
示例：用户丢失私钥后，3 个信任人中的 2 个可以授权恢复。

   - 权限控制：
设置代币支出限额、时间限制或应用白名单，防范钓鱼攻击。
示例：限制某 DApp 每日最多转账 100 USDC。

   - 自动化操作：
支持定投（DCA）、订阅支付或自动申领空投。
示例：智能合约账户定期将 USDC 兑换为 ETH 并存入 DeFi 协议。

   - 跨链兼容性：
UserOps 可以在 L2 网络（如 Arbitrum）上执行，通过跨链桥与主网交互。
支付者机制支持跨链 Gas 支付。

### 2025.05.17
#### EIP-7702

### 2025.05.18
#### EIP-7702对资金追踪的影响

<!-- Content_END -->
